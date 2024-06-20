在 AOSP 项目中，“开发者选项”中的“Open Net ADB”选项对应的是 Android 设置应用的源码。这部分功能主要涉及 `Settings` 应用中的开发者选项相关的代码。具体地，这个功能是通过设置系统属性来控制的。

以下是如何找到对应的源码文件和函数的步骤：

### 1. 查找相关的属性

`adb` 网络调试通常是通过设置系统属性 `persist.adb.tcp.port` 来实现的。我们可以在 AOSP 的 `Settings` 源码中搜索该属性。

### 2. 查找属性的设置位置

进入 AOSP 源码目录后，可以使用 `grep` 命令查找 `persist.adb.tcp.port` 的位置：

```sh
cd path/to/aosp
grep -r "persist.adb.tcp.port" .
```

你应该能找到以下结果：

```sh
./packages/apps/Settings/src/com/android/settings/development/WirelessDebuggingPreferenceController.java:...
```

### 3. 找到对应的 Java 类和函数

根据搜索结果，`WirelessDebuggingPreferenceController.java` 文件中包含对 `persist.adb.tcp.port` 的操作。在 `Settings` 应用中，开发者选项通常由 `PreferenceController` 来控制。

### 4. 查看具体实现

打开 `WirelessDebuggingPreferenceController.java` 文件，可以看到设置网络 ADB 的代码：

```java
package com.android.settings.development;

import android.content.Context;
import android.os.SystemProperties;
import android.provider.Settings;

import androidx.preference.Preference;

import com.android.settings.core.TogglePreferenceController;

public class WirelessDebuggingPreferenceController extends TogglePreferenceController {

    private static final String PREF_KEY = "enable_adb_over_network";

    public WirelessDebuggingPreferenceController(Context context, String key) {
        super(context, key);
    }

    @Override
    public boolean isChecked() {
        return SystemProperties.getInt("persist.adb.tcp.port", -1) > 0;
    }

    @Override
    public boolean setChecked(boolean isChecked) {
        SystemProperties.set("persist.adb.tcp.port", isChecked ? "5555" : "-1");
        return true;
    }

    @Override
    public int getAvailabilityStatus() {
        return AVAILABLE;
    }
}
```

### 5. 解释代码

这个控制器类管理 “Open Net ADB” 选项的状态：

- `isChecked()` 方法：检查 `persist.adb.tcp.port` 属性是否大于 0，以确定网络 ADB 是否开启。
- `setChecked(boolean isChecked)` 方法：根据 `isChecked` 的值设置 `persist.adb.tcp.port` 属性，启用（5555）或禁用（-1）网络 ADB。
- `getAvailabilityStatus()` 方法：返回此选项的可用状态。

综上所述，AOSP 项目中“开发者选项”的“Open Net ADB”功能对应的文件是 `WirelessDebuggingPreferenceController.java`，对应的主要函数是 `isChecked()` 和 `setChecked(boolean isChecked)`。你可以在 `packages/apps/Settings/src/com/android/settings/development/` 路径下找到这个文件。

希望这能帮到你，如果有更多问题，请随时问！




















### 触发器


是的，只要系统在运行，改变 `s9.adbd.auto_start` 的值依然会触发相应的指令。因为 `sys.boot_completed=1` 是一个持久的属性，它在系统启动完成后不会改变，因此在系统运行期间，只要 `s9.adbd.auto_start` 属性发生变化，相应的 `start adbd` 或 `stop adbd` 动作仍会被触发。

具体来说：

- 如果 `sys.boot_completed` 已经被设置为 `1`（这通常在系统启动完成后就会被设置），那么该属性不会再改变。
- 因此，每当 `s9.adbd.auto_start` 的值发生变化时，条件 `sys.boot_completed=1` 仍然成立，触发器就会响应相应的操作。

### 实际行为举例

假设系统已经启动完成且 `sys.boot_completed=1`：

1. 如果你设置 `s9.adbd.auto_start=1`：

   ```sh
   setprop s9.adbd.auto_start 1
   ```

   这将触发以下触发器：

   ```rc
   on property:sys.boot_completed=1 && property:s9.adbd.auto_start=1
       start adbd
   ```

   结果：`adbd` 服务被启动。
2. 如果你设置 `s9.adbd.auto_start=0`：

   ```sh
   setprop s9.adbd.auto_start 0
   ```

   这将触发以下触发器：

   ```rc
   on property:sys.boot_completed=1 && property:s9.adbd.auto_start=0
       stop adbd
   ```

   结果：`adbd` 服务被停止。

### 结论

在系统运行期间，改变 `s9.adbd.auto_start` 的值会触发相应的指令，前提是 `sys.boot_completed` 已经被设置为 `1`。这意味着，只要系统还在运行并且 `sys.boot_completed` 处于 `1` 的状态，`s9.adbd.auto_start` 的变化仍然会导致 `adbd` 服务的启动或停止。
