packages/modules/adb/sockets.cpp

```cpp
#if !ADB_HOST
    if ((name.starts_with("root:") && getuid() != 0 && __android_log_is_debuggable()) ||
        (name.starts_with("unroot:") && getuid() == 0) || name.starts_with("usb:") ||
        name.starts_with("tcpip:")) {
        D("LS(%d): enabling exit_on_close", s->id);
        s->exit_on_close = 1;
    }
#endif
```



adb root追踪

```cpp
//packages/modules/adb/client/commandline.cpp
static bool adb_root(const char* command){
	adb_connect(&transport_id, android::base::StringPrintf("%s:", command), &error)
    adb_get_transport(&previous_type, &previous_serial, &previous_id);
    adb_set_transport(kTransportAny, nullptr, transport_id);
}
```



"adbd cannot run as root in production builds"

```cpp
//packages/modules/adb/daemon/restart_service.cpp
void restart_root_service(unique_fd fd) {
    if (getuid() == 0) {
        WriteFdExactly(fd.get(), "adbd is already running as root\n");
        return;
    }
    if (!__android_log_is_debuggable()) {
        WriteFdExactly(fd.get(), "adbd cannot run as root in production builds\n");
        return;
    }

    LOG(INFO) << "adbd restarting as root";
    android::base::SetProperty("service.adb.root", "1");
    WriteFdExactly(fd.get(), "restarting adbd as root\n");
}
```



packages/modules/adb/daemon/main.cpp

```cpp
static bool should_drop_privileges() {
    // The properties that affect `adb root` and `adb unroot` are ro.secure and
    // ro.debuggable. In this context the names don't make the expected behavior
    // particularly obvious.
    //
    // ro.debuggable:
    //   Allowed to become root, but not necessarily the default. Set to 1 on
    //   eng and userdebug builds.
    //
    // ro.secure:
    //   Drop privileges by default. Set to 1 on userdebug and user builds.
    bool ro_secure = android::base::GetBoolProperty("ro.secure", true);
    bool ro_debuggable = __android_log_is_debuggable();

    // Drop privileges if ro.secure is set...
    bool drop = ro_secure;

    // ... except "adb root" lets you keep privileges in a debuggable build.
    std::string prop = android::base::GetProperty("service.adb.root", "");
    bool adb_root = (prop == "1");
    bool adb_unroot = (prop == "0");
    if (ro_debuggable && adb_root) {
        drop = false;
    }
    // ... and "adb unroot" lets you explicitly drop privileges.
    if (adb_unroot) {
        drop = true;
    }

    return drop;
}
static void drop_privileges(int server_port) {
    ScopedMinijail jail(minijail_new());

    // Add extra groups:
    // AID_ADB to access the USB driver
    // AID_LOG to read system logs (adb logcat)
    // AID_INPUT to diagnose input issues (getevent)
    // AID_INET to diagnose network issues (ping)
    // AID_NET_BT and AID_NET_BT_ADMIN to diagnose bluetooth (hcidump)
    // AID_SDCARD_R to allow reading from the SD card
    // AID_SDCARD_RW to allow writing to the SD card
    // AID_NET_BW_STATS to read out qtaguid statistics
    // AID_READPROC for reading /proc entries across UID boundaries
    // AID_UHID for using 'hid' command to read/write to /dev/uhid
    // AID_EXT_DATA_RW for writing to /sdcard/Android/data (devices without sdcardfs)
    // AID_EXT_OBB_RW for writing to /sdcard/Android/obb (devices without sdcardfs)
    gid_t groups[] = {AID_ADB,          AID_LOG,          AID_INPUT,    AID_INET,
                      AID_NET_BT,       AID_NET_BT_ADMIN, AID_SDCARD_R, AID_SDCARD_RW,
                      AID_NET_BW_STATS, AID_READPROC,     AID_UHID,     AID_EXT_DATA_RW,
                      AID_EXT_OBB_RW};
    minijail_set_supplementary_gids(jail.get(), arraysize(groups), groups);

    // Don't listen on a port (default 5037) if running in secure mode.
    // Don't run as root if running in secure mode.
    if (should_drop_privileges()) {
        const bool should_drop_caps = !__android_log_is_debuggable();

        if (should_drop_caps) {
            minijail_use_caps(jail.get(), CAP_TO_MASK(CAP_SETUID) | CAP_TO_MASK(CAP_SETGID));
        }

        minijail_change_gid(jail.get(), AID_SHELL);
        minijail_change_uid(jail.get(), AID_SHELL);
        // minijail_enter() will abort if any priv-dropping step fails.
        minijail_enter(jail.get());

        // Whenever ambient capabilities are being used, minijail cannot
        // simultaneously drop the bounding capability set to just
        // CAP_SETUID|CAP_SETGID while clearing the inheritable, effective,
        // and permitted sets. So we need to do that in two steps.
        using ScopedCaps =
            std::unique_ptr<std::remove_pointer<cap_t>::type, std::function<void(cap_t)>>;
        ScopedCaps caps(cap_get_proc(), &cap_free);
        if (cap_clear_flag(caps.get(), CAP_INHERITABLE) == -1) {
            PLOG(FATAL) << "cap_clear_flag(INHERITABLE) failed";
        }
        if (cap_clear_flag(caps.get(), CAP_EFFECTIVE) == -1) {
            PLOG(FATAL) << "cap_clear_flag(PEMITTED) failed";
        }
        if (cap_clear_flag(caps.get(), CAP_PERMITTED) == -1) {
            PLOG(FATAL) << "cap_clear_flag(PEMITTED) failed";
        }
        if (cap_set_proc(caps.get()) != 0) {
            PLOG(FATAL) << "cap_set_proc() failed";
        }

        D("Local port disabled");
    } else {
        // minijail_enter() will abort if any priv-dropping step fails.
        minijail_enter(jail.get());

        if (root_seclabel != nullptr) {
            if (selinux_android_setcon(root_seclabel) < 0) {
                LOG(FATAL) << "Could not set SELinux context";
            }
        }
    }
}
```

#### 1. `static bool should_drop_privileges()`

这个函数用于决定是否需要降低权限（drop privileges）。它通过检查系统属性和配置来确定是否需要以非 root 权限运行 ADB（Android Debug Bridge）。

##### 关键逻辑：

1. **系统属性检查**：
   - `ro.secure`：如果为 `true`，表示系统是安全模式，默认需要降低权限。
   - `ro.debuggable`：如果为 `true`，表示系统是可调试的（如 `eng` 或 `userdebug` 版本），允许以 root 权限运行。
   - `lyt.adbd.root_required`：这是一个自定义属性，如果为 `true`，表示需要强制以 root 权限运行。
2. **ADB 特定配置**：
   - `service.adb.root`：如果为 `"1"`，表示用户明确要求以 root 权限运行 ADB。
   - `service.adb.unroot`：如果为 `"0"`，表示用户明确要求降低权限。
3. **返回值**：
   - 如果 `lyt.adbd.root_required` 为 `true`，则返回 `true`，表示需要降低权限。
   - 否则，根据 `ro.secure`、`ro.debuggable` 和 `service.adb.root` 的值决定是否降低权限。











```

root@snowrepo:/snow/android12-rk3588/frameworks# jgrep com.android.internal.space
./base/core/java/android/app/ActivityThread.java:249:import com.android.internal.space.GoogleWrapper;
./base/core/java/android/app/SystemServiceRegistry.java:237:import com.android.internal.space.NineDSpaceManager;
./base/core/java/android/bluetooth/BluetoothAdapter.java:88:import com.android.internal.space.api.BluetoothMock;
./base/core/java/com/android/internal/space/ConfigProperty.java:1:package com.android.internal.space;
./base/core/java/com/android/internal/space/api/AmMock.java:1:package com.android.internal.space.api;
./base/core/java/com/android/internal/space/api/AmMock.java:8:import com.android.internal.space.NineDSpaceManager;
./base/core/java/com/android/internal/space/api/BatteryMock.java:1:package com.android.internal.space.api;
./base/core/java/com/android/internal/space/api/BatteryMock.java:5:import com.android.internal.space.NineDSpaceManager;
./base/core/java/com/android/internal/space/api/BluetoothMock.java:1:package com.android.internal.space.api;
./base/core/java/com/android/internal/space/api/BluetoothMock.java:10:import com.android.internal.space.INineDSpace;
./base/core/java/com/android/internal/space/api/BluetoothMock.java:11:import com.android.internal.space.NineDSpaceManager;
./base/core/java/com/android/internal/space/api/ConnectivityMockCallback.java:1:package com.android.internal.space.api;
./base/core/java/com/android/internal/space/api/ConnectivityMockCallback.java:5:import com.android.internal.space.NineDSpaceManager;
./base/core/java/com/android/internal/space/api/GPSMock.java:1:package com.android.internal.space.api;
./base/core/java/com/android/internal/space/api/GPSMock.java:8:import com.android.internal.space.INineDSpace;
./base/core/java/com/android/internal/space/api/GPSMock.java:9:import com.android.internal.space.NineDSpaceManager;
./base/core/java/com/android/internal/space/api/VpnMock.java:1:package com.android.internal.space.api;
./base/core/java/com/android/internal/space/api/VpnMock.java:10:import com.android.internal.space.NineDSpaceManager;
./base/core/java/com/android/internal/space/api/WifiMockCallback.java:1:package com.android.internal.space.api;
./base/core/java/com/android/internal/space/api/WifiMockCallback.java:5:import com.android.internal.space.NineDSpaceManager;
./base/core/java/com/android/internal/space/NineDSpaceManager.java:1:package com.android.internal.space;
./base/core/java/com/android/internal/space/NineDSpaceManager.java:11:import com.android.internal.space.INineDSpace;
./base/core/java/com/android/internal/space/NineDSpaceManager.java:12:import com.android.internal.space.api.ConnectivityMockCallback;
./base/core/java/com/android/internal/space/NineDSpaceManager.java:13:import com.android.internal.space.api.IMockCallback;
./base/core/java/com/android/internal/space/NineDSpaceManager.java:14:import com.android.internal.space.api.WifiMockCallback;
./base/core/java/com/android/internal/space/GoogleWrapper.java:1:package com.android.internal.space;
./base/packages/SettingsProvider/src/com/android/providers/settings/SettingsProvider.java:110:import com.android.internal.space.ConfigProperty;
./base/packages/SettingsProvider/src/com/android/providers/settings/SettingsProvider.java:111:import com.android.internal.space.NineDSpaceManager;
./base/packages/SettingsProvider/src/com/android/providers/settings/SettingsProvider.java:142:import com.android.internal.space.NineDSpaceManager;
./base/packages/SettingsProvider/src/com/android/providers/settings/SettingsProvider.java:143:import com.android.internal.space.ConfigProperty;
./base/services/core/java/com/android/server/inputmethod/InputMethodManagerService.java:212:import com.android.internal.space.NineDSpaceManager;
./base/services/core/java/com/android/server/pm/PackageManagerService.java:477:import com.android.internal.space.GoogleWrapper;
./base/services/core/java/com/android/server/pm/permission/PermissionManagerService.java:138:import com.android.internal.space.GoogleWrapper;
./base/services/core/java/com/android/server/space/AppFilter.java:13:import com.android.internal.space.NineDSpaceManager;
./base/services/core/java/com/android/server/space/BatteryPolicy.java:17:import com.android.internal.space.api.BatteryMock;
./base/services/core/java/com/android/server/space/SystemTracking.java:7:import com.android.internal.space.NineDSpaceManager;
root@snowrepo:/snow/android12-rk3588/frameworks# 
```

