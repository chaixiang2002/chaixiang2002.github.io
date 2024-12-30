```c++
frameworks/av/media/libmediaplayerservice/MediaPlayerFactory.cpp	//陈敏--游戏--夜鸦进游戏黑屏？？？
frameworks/av/services/camera/libcameraservice/CameraService.cpp	//孔祥巧--摄像头--摄像头等待驱动
frameworks/base/Android.bp	//nop-Space-**构建文件（Android.bp）** 中添加 AIDL 的路径
frameworks/base/api/current.txt//nop-Space-系统上下文加入Space服务
frameworks/base/core/java/android/app/ActivityManager.java//柴祥-内存模拟-
frameworks/base/core/java/android/app/ActivityThread.java//nop-谷歌服务-指纹
frameworks/base/core/java/android/app/SystemServiceRegistry.java//nop-Space-注册Space服务
frameworks/base/core/java/android/bluetooth/BluetoothAdapter.java//柴祥-蓝牙Mock
frameworks/base/core/java/android/content/Context.java//nop-Space-定义新的服务标识
frameworks/base/core/java/android/os/Build.java//柴祥-硬件模拟-ro.hardware
frameworks/base/core/java/android/os/FileUtils.java//柴祥-存储模拟-更准确的存储大小
frameworks/base/core/java/android/os/SystemProperties.java//柴祥-系统属性拦截
frameworks/base/core/java/android/os/storage/StorageManager.java//柴祥-存储模拟-更准确的存储大小
frameworks/base/core/java/android/util/S9Helper.java//柴祥-工具
frameworks/base/core/java/android/util/S9Logger.java//柴祥-工具
frameworks/base/core/java/android/widget/TextView.java//柴祥-剪切板-标识剪切复制
frameworks/base/core/java/com/android/internal/space/ConfigProperty.aidl//nop-Space-配置属性
frameworks/base/core/java/com/android/internal/space/ConfigProperty.java//nop-Space-配置属性
frameworks/base/core/java/com/android/internal/space/GoogleWrapper.java//nop-谷歌服务
frameworks/base/core/java/com/android/internal/space/INineDSpace.aidl//nop-Space
frameworks/base/core/java/com/android/internal/space/NineDSpaceManager.java//nop-Space
frameworks/base/core/java/com/android/internal/space/api/AmMock.java//陈敏-应用保活
frameworks/base/core/java/com/android/internal/space/api/BatteryMock.java//陈敏-电池模拟
frameworks/base/core/java/com/android/internal/space/api/BluetoothMock.java//柴祥-蓝牙模拟
frameworks/base/core/java/com/android/internal/space/api/ConnectivityMock.java//柴祥-网络模拟
frameworks/base/core/java/com/android/internal/space/api/GPSMock.java//柴祥-外部设置gps接口
frameworks/base/core/java/com/android/internal/space/api/IMockCallback.aidl//nop-Space
frameworks/base/core/java/com/android/internal/space/api/VpnMock.java//柴祥-Vpn模拟
frameworks/base/core/java/com/android/internal/space/api/WiFiMock.java//柴祥-WiFi模拟
frameworks/base/core/jni/com_android_internal_os_Zygote.cpp//nop-Space
frameworks/base/core/res/res/values-zh-rCN/strings.xml//岳彪-安装app校验-拒绝安装后弹窗
frameworks/base/core/res/res/values-zh-rHK/strings.xml//岳彪-安装app校验-拒绝安装后弹窗
frameworks/base/core/res/res/values-zh-rTW/strings.xml//岳彪-安装app校验-拒绝安装后弹窗
frameworks/base/core/res/res/values/config.xml//柴祥-运营商图标
frameworks/base/core/res/res/values/strings.xml//岳彪-安装app校验-拒绝安装后弹窗
frameworks/base/core/res/res/values/symbols.xml//岳彪-安装app校验-拒绝安装后弹窗
frameworks/base/core/res/res/xml/config_webview_packages.xml//陈敏-更新webview
frameworks/base/data/keyboards/Generic.kl//柴祥-键盘匹配-菜单换成任务切换
frameworks/base/packages/SettingsLiTile/src/com/android/settingslidrawer/TileUtils.java//nop-打印intent和对应组件
frameworks/base/packages/SettingsLisrc/com/android/settingslibluetooth/LocalBluetoothAdapter.java//柴祥-蓝牙模拟
frameworks/base/packages/SettingsProvider/res/values/defaults.xml//nop-系统默认设置-关闭超时熄屏、蓝牙默认关闭、安装校验关闭
frameworks/base/packages/SettingsProvider/src/com/android/providers/settings/DatabaseHelper.java//岳彪-时区
frameworks/base/packages/SettingsProvider/src/com/android/providers/settings/SettingsProvider.java//岳彪-共享AndroidID-|nop监控
frameworks/base/packages/SystemUI/legacy/recents/src/com/android/systemui/recents/LegacyRecentsImpl.java//柴祥-打印任务切换
frameworks/base/packages/SystemUI/res/layout/status_bar_mobile_signal_group.xml//柴祥-显示运营商
frameworks/base/packages/SystemUI/src/com/android/systemui/media/MediaProjectionPermissionActivity.java//nop-判断屏幕录制
frameworks/base/packages/SystemUI/src/com/android/systemui/qs/tiles/BluetoothTile.java//柴祥-蓝牙模拟
frameworks/base/packages/SystemUI/src/com/android/systemui/recents/OverviewProxyRecentsImpl.java//柴祥-监控任务切换
frameworks/base/packages/SystemUI/src/com/android/systemui/recents/Recents.java//柴祥-监控任务切换
frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/CommandQueue.java//柴祥-监控任务切换
frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/StatusBarMobileView.java//柴祥-显示运营商
frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/policy/BluetoothControllerImpl.java//柴祥-蓝牙模拟
frameworks/base/packages/VpnDialogs/src/com/android/vpndialogs/ConfirmDialog.java//nop-vpn模拟
frameworks/base/services/accessibility/java/com/android/server/accessibility/AccessibilityManagerService.java//nop-隐藏辅助功能服务列表
frameworks/base/services/core/java/com/android/server/BatteryService.java//nop-电池模拟
frameworks/base/services/core/java/com/android/server/ConnectivityService.java//nop-网络模拟
frameworks/base/services/core/java/com/android/server/PersistentDataBlockService.java//nop??????????????
frameworks/base/services/core/java/com/android/server/StorageManagerService.java// 柴祥-重置-文件不可访问
frameworks/base/services/core/java/com/android/server/am/ActivityManagerService.java//nop-监控-监控检测死掉
frameworks/base/services/core/java/com/android/server/am/AppErrors.java//nop-隐藏APP
frameworks/base/services/core/java/com/android/server/am/BatteryExternalStatsWorker.java//nop-判空空指针
frameworks/base/services/core/java/com/android/server/am/ProcessList.java//陈敏-应用保活
frameworks/base/services/core/java/com/android/server/connectivity/Vpn.java//柴祥-Vpn空指针
frameworks/base/services/core/java/com/android/server/display/DisplayPowerController.java//nop-监控-系统亮度
frameworks/base/services/core/java/com/android/server/inputmethod/InputMethodManagerService.java//nop-输入
frameworks/base/services/core/java/com/android/server/pm/PackageInstallerService.java//nop-自动授予权限运行时权限
frameworks/base/services/core/java/com/android/server/pm/PackageManagerService.java//搞鬼游戏 |绝安装后弹窗 |绝安装后弹窗 |ins更换头像打不开相册 |安装失败导致应用崩溃
frameworks/base/services/core/java/com/android/server/pm/permission/PermissionManagerService.java//nop-谷歌服务
frameworks/base/services/core/java/com/android/server/policy/PhoneWindowManager.java//柴祥-监控-任务切换
frameworks/base/services/core/java/com/android/server/space/AppFilter.java//岳彪-应用包名隐藏
frameworks/base/services/core/java/com/android/server/space/BatteryPolicy.java//nop-电池模拟
frameworks/base/services/core/java/com/android/server/space/SystemTracking.java//nop-Space服务-Space向Stream发送接口
frameworks/base/services/core/java/com/android/server/statusbar/StatusBarManagerInternal.java//柴祥-监控任务切换
frameworks/base/services/core/java/com/android/server/wm/ActivityRecord.java//nop-监控Activity
frameworks/base/services/core/java/com/android/server/wm/ActivityTaskManagerService.java//nop-判断是否允许启动应用
frameworks/base/services/core/java/com/android/server/wm/AppWarnings.java//nop-隐藏应用警告弹窗
frameworks/base/services/core/java/com/android/server/wm/DisplayContent.java//nop-指定键盘
frameworks/base/services/core/java/com/android/server/wm/InputManagerCallback.java//柴祥-监控-监控键盘事件
frameworks/base/services/core/java/com/android/server/wm/WindowManagerService.java//nop-禁止进入安全模式
frameworks/base/services/core/jni/com_android_server_PersistentDataBlockService.cpp//无效修改
frameworks/base/services/java/com/android/server/SystemServer.java//柴祥-拓展服务-提前自启
frameworks/native/libs/binder/BpBinder.cpp//nop-监控-监控部分Binder的名称
frameworks/native/libs/binder/ProcessState.cpp//陈敏-增加binder的虚拟机大小
frameworks/native/opengl/libs/GLES_CM/gl.cpp//柴祥-Gpu伪装
frameworks/native/services/inputflinger/EventHub.cpp//柴祥-监控-监控键盘事件
frameworks/native/services/inputflinger/InputDispatcher.cpp//柴祥-监控-监控键盘事件
frameworks/native/services/inputflinger/InputReader.cpp//柴祥-监控-监控键盘事件
frameworks/native/services/inputflinger/S9Logger.h//柴祥-监控-监控键盘事件
frameworks/opt/net/ethernet/java/com/android/server/ethernet/EthernetTracker.java//nop-网络模拟-！！！！
frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java//nop-wifi模拟
frameworks/opt/telephony/src/java/com/android/internal/telephony/RIL.java//nop-sim卡模拟
frameworks/opt/telephony/src/java/com/android/internal/telephony/SubscriptionController.java//nop-注释运行时错误
```

**01-陈敏--游戏--夜鸦进游戏黑屏？？？**

- 游戏播放资源有.apk的后缀，如果是谷歌的播放器则支持，rk的播放器不支持，修改后支持

**02-frameworks/base/services/core/java/com/android/server/PersistentDataBlockService.java//nop??????????????**

1. `PersistentDataBlockService` 类的作用：

该类继承自 `SystemService`，表示它是 Android 系统服务中的一部分，主要用于处理“持久数据块”相关的任务。通常，Android 中的持久数据块可能指的是一些设备或系统级别的存储区域，里面保存一些需要跨重启保存的重要数据。

- **`mContext`**：保存服务的上下文对象，通常是应用或系统的上下文，提供对系统资源的访问。
- **`mDataBlockFile`**：这是一个文件路径，由系统属性 `PERSISTENT_DATA_BLOCK_PROP` 提供，表示数据块存储的路径。
- **`mBlockDeviceSize`**：表示数据块的大小，初始化为 -1，可能是延迟加载的。

2. **`file.createNewFile()` 的作用：**

在构造函数中，我们看到了一段关于文件操作的代码：

```
java复制代码File file = new File(mDataBlockFile);
if (!file.exists()) {
    try {
        file.createNewFile();
    } catch (IOException e) {
    }
}
```

- **`mDataBlockFile`** 是一个从系统属性中获取的路径（通过 `SystemProperties.get(PERSISTENT_DATA_BLOCK_PROP)`），它指定了存储持久数据块的文件路径。

- **`new File(mDataBlockFile)`** 创建了一个 `File` 对象，表示该路径上的文件。

- `if (!file.exists())`

   检查该路径上的文件是否存在。如果文件不存在，则执行 

  ```
  createNewFile()
  ```

   创建新文件。

  - **`file.createNewFile()`**：如果文件在指定路径不存在，则会尝试创建一个新的文件。如果文件已经存在，则此方法不会执行任何操作。
  - **`IOException`**：如果在创建文件时发生任何 I/O 错误（如权限问题等），则捕获异常并不做处理（在这个代码中，异常被捕获但没有处理或记录）。

3. **为什么会加上这个文件检查和创建代码？**

这段代码主要是确保持久化数据块文件存在。如果该文件不存在，系统会创建一个新的空文件。它的作用可能是：

- 在系统启动时，确保持久化数据块文件已经准备好，避免后续访问时出现文件未找到的错误。
- 提供一个简单的文件持久化机制来存储系统的关键数据块（比如一些设备配置、系统状态、用户数据等）。