





```kotlin
//com/topjohnwu/magisk/ui/flash/FlashViewModel.kt
fun startFlashing() {
    val (action, uri) = args

    viewModelScope.launch {
        val result = when (action) {
            Const.Value.FLASH_ZIP -> {
                uri ?: return@launch
                FlashZip(uri, outItems, logItems).exec()
            }
            Const.Value.UNINSTALL -> {
                showReboot = false
                MagiskInstaller.Uninstall(outItems, logItems).exec()
            }
            Const.Value.FLASH_MAGISK -> {
                if (Info.isEmulator)
                MagiskInstaller.Emulator(outItems, logItems).exec()
                else
                MagiskInstaller.Direct(outItems, logItems).exec()
            }
            Const.Value.FLASH_INACTIVE_SLOT -> {
                MagiskInstaller.SecondSlot(outItems, logItems).exec()
            }
            Const.Value.PATCH_FILE -> {
                uri ?: return@launch
                showReboot = false
                MagiskInstaller.Patch(uri, outItems, logItems).exec()
            }
            else -> {
                back()
                return@launch
            }
        }
        onResult(result)
    }
}

//com/topjohnwu/magisk/core/tasks/MagiskInstaller.kt
protected fun fixEnv() = extractFiles() && "fix_env $installDir".sh().isSuccess
protected fun direct() = findImage() && extractFiles() && patchBoot() && flashBoot()

private fun findImage(): Boolean {
    val bootPath = "RECOVERYMODE=${Config.recovery} find_boot_image; echo \"\$BOOTIMAGE\"".fsh()
    if (bootPath.isEmpty()) {
        console.add("! Unable to detect target image")
        return false
    }
    srcBoot = rootFS.getFile(bootPath)
    console.add("- Target image: $bootPath")
    return true
}

private fun extractFiles(): Boolean {
    console.add("- Device platform: ${Const.CPU_ABI}")
    console.add("- Installing: ${BuildConfig.VERSION_NAME} (${BuildConfig.VERSION_CODE})")

    installDir = localFS.getFile(context.filesDir.parent, "install")
    installDir.deleteRecursively()
    installDir.mkdirs()

    try {
        // Extract binaries
        if (isRunningAsStub) {
            val zf = ZipFile(StubApk.current(context))

            // Also extract magisk32 on non 64-bit only 64-bit devices
            val is32lib = Const.CPU_ABI_32?.let {
                { entry: ZipEntry -> entry.name == "lib/$it/libmagisk32.so" }
            } ?: { false }

            zf.entries().asSequence().filter {
                !it.isDirectory && (it.name.startsWith("lib/${Const.CPU_ABI}/") || is32lib(it))
            }.forEach {
                val n = it.name.substring(it.name.lastIndexOf('/') + 1)
                val name = n.substring(3, n.length - 3)
                val dest = File(installDir, name)
                zf.getInputStream(it).writeTo(dest)
                dest.setExecutable(true)
            }
            zf.close()
        } else {
            val info = context.applicationInfo
            var libs = File(info.nativeLibraryDir).listFiles { _, name ->
                                                              name.startsWith("lib") && name.endsWith(".so")
                                                             } ?: emptyArray()

            // Also symlink magisk32 on non 64-bit only 64-bit devices
            val lib32 = info.javaClass.getDeclaredField("secondaryNativeLibraryDir")
            .get(info) as String?
            if (lib32 != null) {
                libs += File(lib32, "libmagisk32.so")
            }

            for (lib in libs) {
                val name = lib.name.substring(3, lib.name.length - 3)
                Os.symlink(lib.path, "$installDir/$name")
            }
        }

        // Extract scripts
        for (script in listOf("util_functions.sh", "boot_patch.sh", "addon.d.sh", "stub.apk")) {
            val dest = File(installDir, script)
            context.assets.open(script).writeTo(dest)
        }
        // Extract chromeos tools
        File(installDir, "chromeos").mkdir()
        for (file in listOf("futility", "kernel_data_key.vbprivk", "kernel.keyblock")) {
            val name = "chromeos/$file"
            val dest = File(installDir, name)
            context.assets.open(name).writeTo(dest)
        }
    } catch (e: Exception) {
        console.add("! Unable to extract files")
        Timber.e(e)
        return false
    }

    if (useRootDir) {
        // Move everything to tmpfs to workaround Samsung bullshit
        rootFS.getFile(Const.TMPDIR).also {
            arrayOf(
                "rm -rf $it",
                "mkdir -p $it",
                "cp_readlink $installDir $it",
                "rm -rf $installDir"
            ).sh()
            installDir = it
        }
    }

    return true
}

private fun patchBoot(): Boolean {
    val newBoot = installDir.getChildFile("new-boot.img")
    if (!useRootDir) {
        // Create output files before hand
        newBoot.createNewFile()
        File(installDir, "stock_boot.img").createNewFile()
    }

    val cmds = arrayOf(
        "cd $installDir",
        "KEEPFORCEENCRYPT=${Config.keepEnc} " +
        "KEEPVERITY=${Config.keepVerity} " +
        "PATCHVBMETAFLAG=${Info.patchBootVbmeta} " +
        "RECOVERYMODE=${Config.recovery} " +
        "LEGACYSAR=${Info.legacySAR} " +
        "sh boot_patch.sh $srcBoot")
    val isSuccess = cmds.sh().isSuccess

    shell.newJob().add("./magiskboot cleanup", "cd /").exec()

    return isSuccess
}

private fun flashBoot() = "direct_install $installDir $srcBoot".sh().isSuccess


```



shell

```yaml
fixEnv：
	fix_env $installDir".sh()

patchBoot：
        "cd $installDir",
        "KEEPFORCEENCRYPT=${Config.keepEnc} " +
        "KEEPVERITY=${Config.keepVerity} " +
        "PATCHVBMETAFLAG=${Info.patchBootVbmeta} " +
        "RECOVERYMODE=${Config.recovery} " +
        "LEGACYSAR=${Info.legacySAR} " +
        "sh boot_patch.sh $srcBoot")
        
       ./magiskboot cleanup", "cd /"

flashBoot：
       direct_install $installDir $srcBoot
```



```
//app/src/main/res/raw/manager.sh
fix_env() {
  # Cleanup and make dirs
  rm -rf $MAGISKBIN/*
  mkdir -p $MAGISKBIN 2>/dev/null
  chmod 700 $NVBASE
  cp_readlink $1 $MAGISKBIN
  rm -rf $1
  chown -R 0:0 $MAGISKBIN
}
```



```shell
//scripts/boot_patch.sh

# Pure bash dirname implementation
getdir() {
  case "$1" in
    */*)
      dir=${1%/*}
      if [ -z $dir ]; then
        echo "/"
      else
        echo $dir
      fi
    ;;
    *) echo "." ;;
  esac
}

#################
# Initialization
#################

if [ -z $SOURCEDMODE ]; then
  # Switch to the location of the script file
  cd "$(getdir "${BASH_SOURCE:-$0}")"
  # Load utility functions
  . ./util_functions.sh
  # Check if 64-bit
  api_level_arch_detect
fi

BOOTIMAGE="$1"
[ -e "$BOOTIMAGE" ] || abort "$BOOTIMAGE does not exist!"

# Dump image for MTD/NAND character device boot partitions
if [ -c "$BOOTIMAGE" ]; then
  nanddump -f boot.img "$BOOTIMAGE"
  BOOTNAND="$BOOTIMAGE"
  BOOTIMAGE=boot.img
fi

# Flags
[ -z $KEEPVERITY ] && KEEPVERITY=false
[ -z $KEEPFORCEENCRYPT ] && KEEPFORCEENCRYPT=false
[ -z $PATCHVBMETAFLAG ] && PATCHVBMETAFLAG=false
[ -z $RECOVERYMODE ] && RECOVERYMODE=false
[ -z $LEGACYSAR ] && LEGACYSAR=false
export KEEPVERITY
export KEEPFORCEENCRYPT
export PATCHVBMETAFLAG

chmod -R 755 .

#########
# Unpack
#########

CHROMEOS=false

ui_print "- Unpacking boot image"
./magiskboot unpack "$BOOTIMAGE"

case $? in
  0 ) ;;
  1 )
    abort "! Unsupported/Unknown image format"
    ;;
  2 )
    ui_print "- ChromeOS boot image detected"
    CHROMEOS=true
    ;;
  * )
    abort "! Unable to unpack boot image"
    ;;
esac

###################
# Ramdisk Restores
###################

# Test patch status and do restore
ui_print "- Checking ramdisk status"
if [ -e ramdisk.cpio ]; then
  ./magiskboot cpio ramdisk.cpio test
  STATUS=$?
  SKIP_BACKUP=""
else
  # Stock A only legacy SAR, or some Android 13 GKIs
  STATUS=0
  SKIP_BACKUP="#"
fi
case $((STATUS & 3)) in
  0 )  # Stock boot
    ui_print "- Stock boot image detected"
    SHA1=$(./magiskboot sha1 "$BOOTIMAGE" 2>/dev/null)
    cat $BOOTIMAGE > stock_boot.img
    cp -af ramdisk.cpio ramdisk.cpio.orig 2>/dev/null
    ;;
  1 )  # Magisk patched
    ui_print "- Magisk patched boot image detected"
    ./magiskboot cpio ramdisk.cpio \
    "extract .backup/.magisk config.orig" \
    "restore"
    cp -af ramdisk.cpio ramdisk.cpio.orig
    rm -f stock_boot.img
    ;;
  2 )  # Unsupported
    ui_print "! Boot image patched by unsupported programs"
    abort "! Please restore back to stock boot image"
    ;;
esac

# Workaround custom legacy Sony /init -> /(s)bin/init_sony : /init.real setup
INIT=init
if [ $((STATUS & 4)) -ne 0 ]; then
  INIT=init.real
fi

if [ -f config.orig ]; then
  # Read existing configs
  chmod 0644 config.orig
  SHA1=$(grep_prop SHA1 config.orig)
  if ! $BOOTMODE; then
    # Do not inherit config if not in recovery
    PREINITDEVICE=$(grep_prop PREINITDEVICE config.orig)
  fi
  rm config.orig
fi

##################
# Ramdisk Patches
##################

ui_print "- Patching ramdisk"

# Compress to save precious ramdisk space
SKIP32="#"
SKIP64="#"
if [ -f magisk64 ]; then
  $BOOTMODE && [ -z "$PREINITDEVICE" ] && PREINITDEVICE=$(./magisk64 --preinit-device)
  ./magiskboot compress=xz magisk64 magisk64.xz
  unset SKIP64
fi
if [ -f magisk32 ]; then
  $BOOTMODE && [ -z "$PREINITDEVICE" ] && PREINITDEVICE=$(./magisk32 --preinit-device)
  ./magiskboot compress=xz magisk32 magisk32.xz
  unset SKIP32
fi
./magiskboot compress=xz stub.apk stub.xz

echo "KEEPVERITY=$KEEPVERITY" > config
echo "KEEPFORCEENCRYPT=$KEEPFORCEENCRYPT" >> config
echo "RECOVERYMODE=$RECOVERYMODE" >> config
if [ -n "$PREINITDEVICE" ]; then
  ui_print "- Pre-init storage partition: $PREINITDEVICE"
  echo "PREINITDEVICE=$PREINITDEVICE" >> config
fi
[ -n "$SHA1" ] && echo "SHA1=$SHA1" >> config

./magiskboot cpio ramdisk.cpio \
"add 0750 $INIT magiskinit" \
"mkdir 0750 overlay.d" \
"mkdir 0750 overlay.d/sbin" \
"$SKIP32 add 0644 overlay.d/sbin/magisk32.xz magisk32.xz" \
"$SKIP64 add 0644 overlay.d/sbin/magisk64.xz magisk64.xz" \
"add 0644 overlay.d/sbin/stub.xz stub.xz" \
"patch" \
"$SKIP_BACKUP backup ramdisk.cpio.orig" \
"mkdir 000 .backup" \
"add 000 .backup/.magisk config" \
|| abort "! Unable to patch ramdisk"

rm -f ramdisk.cpio.orig config magisk*.xz stub.xz

#################
# Binary Patches
#################

for dt in dtb kernel_dtb extra; do
  if [ -f $dt ]; then
    if ! ./magiskboot dtb $dt test; then
      ui_print "! Boot image $dt was patched by old (unsupported) Magisk"
      abort "! Please try again with *unpatched* boot image"
    fi
    if ./magiskboot dtb $dt patch; then
      ui_print "- Patch fstab in boot image $dt"
    fi
  fi
done

if [ -f kernel ]; then
  PATCHEDKERNEL=false
  # Remove Samsung RKP
  ./magiskboot hexpatch kernel \
  49010054011440B93FA00F71E9000054010840B93FA00F7189000054001840B91FA00F7188010054 \
  A1020054011440B93FA00F7140020054010840B93FA00F71E0010054001840B91FA00F7181010054 \
  && PATCHEDKERNEL=true

  # Remove Samsung defex
  # Before: [mov w2, #-221]   (-__NR_execve)
  # After:  [mov w2, #-32768]
  ./magiskboot hexpatch kernel 821B8012 E2FF8F12 && PATCHEDKERNEL=true

  # Force kernel to load rootfs for legacy SAR devices
  # skip_initramfs -> want_initramfs
  $LEGACYSAR && ./magiskboot hexpatch kernel \
  736B69705F696E697472616D667300 \
  77616E745F696E697472616D667300 \
  && PATCHEDKERNEL=true

  # If the kernel doesn't need to be patched at all,
  # keep raw kernel to avoid bootloops on some weird devices
  $PATCHEDKERNEL || rm -f kernel
fi

#################
# Repack & Flash
#################

ui_print "- Repacking boot image"
./magiskboot repack "$BOOTIMAGE" || abort "! Unable to repack boot image"

# Sign chromeos boot
$CHROMEOS && sign_chromeos

# Restore the original boot partition path
[ -e "$BOOTNAND" ] && BOOTIMAGE="$BOOTNAND"

# Reset any error code
true


```

```shell
//scripts/boot_patch.sh
direct_install() {
  echo "- Flashing new boot image"
  flash_image $1/new-boot.img $2
  case $? in
    1)
      echo "! Insufficient partition size"
      return 1
      ;;
    2)
      echo "! $2 is read only"
      return 2
      ;;
  esac

  rm -f $1/new-boot.img
  fix_env $1
  run_migrations
  copy_preinit_files

  return 0
}
```

