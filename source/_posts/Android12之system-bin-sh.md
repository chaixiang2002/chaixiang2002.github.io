external/mksh/Android.bp

```yaml
cc_binary {
    name: "sh",
    defaults: ["sh-defaults"],
    recovery_available: true,
    vendor_ramdisk_available: true,
}

cc_defaults {
    name: "sh-defaults",

    srcs: [
        "src/lalloc.c",
        "src/edit.c",
        "src/eval.c",
        "src/exec.c",
        "src/expr.c",
        "src/funcs.c",
        "src/histrap.c",
        "src/jobs.c",
        "src/lex.c",
        "src/main.c",
        "src/misc.c",
        "src/shf.c",
        "src/syn.c",
        "src/tree.c",
        "src/var.c",
    ],

    local_include_dirs: ["src"],

    cflags: [
        // Compiler flags...
        "-Wall",
        "-Werror",
        "-Wno-deprecated-declarations",
        "-fno-asynchronous-unwind-tables",
        "-fno-strict-aliasing",
        "-fwrapv",

        // ...various options we choose
        "-DDEBUG_LEAKS",
        "-DMKSH_ASSUME_UTF8",
        "-DMKSH_DONT_EMIT_IDSTRING",
        "-DKSH_VERSIONNAME_VENDOR_EXT=\" Android\"",

        // ...and the defines from Build.sh.
        "-DMKSH_BUILDSH",
        "-D_GNU_SOURCE",
        "-DSETUID_CAN_FAIL_WITH_EAGAIN",
        "-DHAVE_STRING_POOLING=1",
        "-DHAVE_ATTRIBUTE_BOUNDED=1",
        "-DHAVE_ATTRIBUTE_FORMAT=1",
        "-DHAVE_ATTRIBUTE_NORETURN=1",
        "-DHAVE_ATTRIBUTE_PURE=1",
        "-DHAVE_ATTRIBUTE_UNUSED=1",
        "-DHAVE_ATTRIBUTE_USED=1",
        "-DHAVE_SYS_TIME_H=1",
        "-DHAVE_TIME_H=1",
        "-DHAVE_BOTH_TIME_H=1",
        "-DHAVE_SYS_BSDTYPES_H=0",
        "-DHAVE_SYS_FILE_H=1",
        "-DHAVE_SYS_MKDEV_H=0",
        "-DHAVE_SYS_MMAN_H=1",
        "-DHAVE_SYS_PARAM_H=1",
        "-DHAVE_SYS_RESOURCE_H=1",
        "-DHAVE_SYS_SELECT_H=1",
        "-DHAVE_SYS_SYSMACROS_H=1",
        "-DHAVE_BSTRING_H=0",
        "-DHAVE_GRP_H=1",
        "-DHAVE_IO_H=0",
        "-DHAVE_LIBGEN_H=1",
        "-DHAVE_LIBUTIL_H=0",
        "-DHAVE_PATHS_H=1",
        "-DHAVE_STDINT_H=1",
        "-DHAVE_STRINGS_H=1",
        "-DHAVE_TERMIOS_H=1",
        "-DHAVE_ULIMIT_H=0",
        "-DHAVE_VALUES_H=0",
        "-DHAVE_CAN_INTTYPES=1",
        "-DHAVE_CAN_UCBINTS=1",
        "-DHAVE_CAN_INT8TYPE=1",
        "-DHAVE_CAN_UCBINT8=1",
        "-DHAVE_RLIM_T=1",
        "-DHAVE_SIG_T=1",
        "-DHAVE_SYS_ERRLIST=0",
        "-DHAVE_SYS_SIGNAME=1",
        "-DHAVE_SYS_SIGLIST=1",
        "-DHAVE_FLOCK=1",
        "-DHAVE_LOCK_FCNTL=1",
        "-DHAVE_GETRUSAGE=1",
        "-DHAVE_GETSID=1",
        "-DHAVE_GETTIMEOFDAY=1",
        "-DHAVE_KILLPG=1",
        "-DHAVE_MEMMOVE=1",
        "-DHAVE_MKNOD=0",
        "-DHAVE_MMAP=1",
        "-DHAVE_FTRUNCATE=1",
        "-DHAVE_NICE=1",
        "-DHAVE_REVOKE=0",
        "-DHAVE_SETLOCALE_CTYPE=1",
        "-DHAVE_LANGINFO_CODESET=1",
        "-DHAVE_SELECT=1",
        "-DHAVE_SETRESUGID=1",
        "-DHAVE_SETGROUPS=1",
        "-DHAVE_STRERROR=1",
        "-DHAVE_STRSIGNAL=0",
        "-DHAVE_STRLCPY=1",
        "-DHAVE_FLOCK_DECL=1",
        "-DHAVE_REVOKE_DECL=1",
        "-DHAVE_SYS_ERRLIST_DECL=0",
        "-DHAVE_SYS_SIGLIST_DECL=1",
        "-DHAVE_PERSISTENT_HISTORY=0",
        "-DMKSH_BUILD_R=592",

        // Additional flags
        "-DMKSH_DEFAULT_PROFILEDIR=\"/system/etc\"",
        "-DMKSHRC_PATH=\"/system/etc/mkshrc\"",
        "-DMKSH_DEFAULT_EXECSHELL=\"/system/bin/sh\"",
        "-DMKSH_DEFAULT_TMPDIR=\"/data/local\"",
    ],

    stl: "none",
    system_shared_libs: ["libc"],
}
```







解决方法

改动
/etc/mkshrc  例如：

```shell
4ec1c7616de5:/ # cat /etc/mkshrc
# Copyright (c) 2010, 2012, 2013, 2014
#       Thorsten Glaser <tg@mirbsd.org>
# This file is provided under the same terms as mksh.
#-
# Minimal /system/etc/mkshrc for Android
#
# Support: https://launchpad.net/mksh

set +o nohup

if (( USER_ID )); then PS1='$'; else PS1='#'; fi
PS4='[$EPOCHREALTIME] '; PS1='${|
        local e=$?

        (( e )) && REPLY+="$e|"

        return $e
}$HOSTNAME:${PWD:-?} '"$PS1 "


alias ll='ls -l'
export PATH=$PATH:/data/local/bin
export PATH=$PATH:/vendor/bin


alias ll='ls -l'
export PATH=$PATH:/data/local/bin
export PATH=$PATH:/vendor/bin

# Additional Environment Variables
export ANDROID_DATA=/data
export RK_ADEPT_ACTIVATION_FILE=/mnt/sdcard/.adobe-digital-editions/activation.xml
export RK_ADOBE_DE_DOC_FOLDER=/mnt/sdcard/Digital Editions
export ADOBE_FONTS_DIR=/system/fonts/adobefonts/
export RK_ADEPT_DEVICE_TYPE=mobile
export RK_ADEPT_DEVICE_SALT_FILE=/mnt/sdcard/.adobe-digital-editions/devicesalt
export ANDROID_RUNTIME_ROOT=/apex/com.android.runtime
export ANDROID_TZDATA_ROOT=/apex/com.android.tzdata
export HOME=/
export EBOOK_PAGE_VISIBLE_NUMBER=2
export ANDROID_ASSETS=/system/app
export BOOTCLASSPATH=/apex/com.android.runtime/javalib/core-oj.jar:/apex/com.android.runtime/javalib/core-libart.jar:/apex/com.android.runtime/javalib/okhttp.jar:/apex/com.android.runtime/javalib/bouncycastle.jar:/apex/com.android.runtime/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/android.test.base.jar:/apex/com.android.conscrypt/javalib/conscrypt.jar:/apex/com.android.media/javalib/updatable-media.jar
export ANDROID_BOOTLOGO=1
export ANDROID_STORAGE=/storage
export DOWNLOAD_CACHE=/data/cache
export LOGNAME=shell
export SYSTEMSERVERCLASSPATH=/system/framework/services.jar:/system/framework/ethernet-service.jar:/system/framework/wifi-service.jar:/system/framework/com.android.location.provider.jar
export DEX2OATBOOTCLASSPATH=/apex/com.android.runtime/javalib/core-oj.jar:/apex/com.android.runtime/javalib/core-libart.jar:/apex/com.android.runtime/javalib/okhttp.jar:/apex/com.android.runtime/javalib/bouncycastle.jar:/apex/com.android.runtime/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/android.test.base.jar
export EXTERNAL_STORAGE=/sdcard
export SHELL=/system/bin/sh
export RK_ADOBE_DE_MOBILE=1
export RK_ADEPT_DEVICE_FILE=/mnt/sdcard/.adobe-digital-editions/device.xml
export ASEC_MOUNTPOINT=/mnt/asec
export USER=shell
export PATH=/sbin:/system/sbin:/product/bin:/apex/com.android.runtime/bin:/system/bin:/system/xbin:/odm/bin:/vendor/bin:/vendor/xbin:/data/misc/overlay_misc/upper
export ANDROID_ROOT=/system
export CURL_CA_BUNDLE=/system/etc/cacert.pem
```



修改external/mksh/mkshrc即可