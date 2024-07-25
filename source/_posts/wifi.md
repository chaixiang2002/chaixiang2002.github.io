要在AOSP 10中定制Network & Internet设置中的WiFi页面，并实现一个虚拟的WiFi连接，需要修改相关的系统服务和UI代码。以下是找到相关代码文件和实现方法的步骤：

### 1. 找到WiFi设置页面的代码

WiFi设置页面属于系统设置的一部分，主要位于 `Settings`应用中。`Settings`应用的源码在以下路径：

```
packages/apps/Settings/
```

具体的WiFi设置页面位于 `wifi`子目录下：

```
packages/apps/Settings/src/com/android/settings/wifi/
```

### 2. 主要的文件和类

1. **WiFi设置的入口类**：

   - 文件：`WifiSettings.java`
   - 路径：`packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java`
   - 作用：负责显示WiFi设置页面和处理用户的交互。
2. **WiFi设置的详细页面**：

   - 文件：`WifiDetailPreferenceController.java`
   - 路径：`packages/apps/Settings/src/com/android/settings/wifi/details/WifiDetailPreferenceController.java`
   - 作用：显示具体的WiFi网络详情。

### 3. 修改WiFi设置页面

要mock一个虚拟的WiFi连接，可以从以下几个方面入手：

#### 3.1 修改WiFi扫描结果

为了显示虚拟的WiFi网络，需要修改WiFi扫描结果。在系统服务层，可以拦截或修改扫描结果。WiFi扫描结果主要通过 `WifiService`来管理：

- 文件：`WifiServiceImpl.java`
- 路径：`frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java`

在 `WifiServiceImpl`中，可以找到 `getScanResults()`方法，修改其返回值以添加虚拟的WiFi网络。

#### 3.2 修改连接逻辑

修改WiFi连接逻辑以处理虚拟WiFi连接。在 `WifiServiceImpl`中，可以找到 `connect()`方法，添加对虚拟WiFi网络的处理逻辑。

### 4. 具体实现步骤

#### 4.1 修改 `WifiServiceImpl.java`中的扫描结果

```java
@Override
public List<ScanResult> getScanResults(String callingPackage, String callingFeatureId) {
    List<ScanResult> results = super.getScanResults(callingPackage, callingFeatureId);

    // 添加虚拟的WiFi网络
    ScanResult virtualWifi = new ScanResult();
    virtualWifi.SSID = "Virtual_WiFi";
    virtualWifi.BSSID = "00:11:22:33:44:55";
    virtualWifi.capabilities = "[WPA2-PSK-CCMP][ESS]";
    virtualWifi.level = -50; // 信号强度
    results.add(virtualWifi);

    return results;
}
```

#### 4.2 修改 `WifiServiceImpl.java`中的连接逻辑

```java
@Override
public void connect(int networkId, ActionListener listener, int uid, String packageName) {
    if (isVirtualWifiNetwork(networkId)) {
        // 处理虚拟WiFi连接
        listener.onSuccess();
        return;
    }

    super.connect(networkId, listener, uid, packageName);
}

private boolean isVirtualWifiNetwork(int networkId) {
    // 判断是否是虚拟WiFi网络
    return networkId == VIRTUAL_WIFI_NETWORK_ID;
}
```

#### 4.3 修改UI层

在 `WifiSettings.java`中，可以添加对虚拟WiFi网络的处理逻辑。

```java
// 在初始化WiFi设置时，添加对虚拟WiFi网络的处理
private void initWifiSettings() {
    // 其他初始化代码

    // 添加虚拟WiFi网络
    AccessPoint virtualAp = new AccessPoint(getContext());
    virtualAp.setSsid("Virtual_WiFi");
    virtualAp.setBssid("00:11:22:33:44:55");
    virtualAp.setSecurity(AccessPoint.SECURITY_PSK);
    virtualAp.setLevel(-50);
    mWifiManager.addNetwork(virtualAp.getConfig());
}
```

### 总结

以上步骤展示了如何在AOSP 10中修改WiFi设置页面，并mock一个虚拟的WiFi连接。主要涉及到修改WiFi扫描结果和连接逻辑，同时在UI层添加对虚拟WiFi网络的处理。通过这些修改，可以在定制的操作系统中显示并处理虚拟的WiFi连接。

    [在AOSP 10中，处理WiFi扫描结果的代码主要位于 `WifiConfigController.java`和 `WifiSettings.java`这两个文件中](https://blog.csdn.net/frank_eos/article/details/111409440)[^1^](https://blog.csdn.net/frank_eos/article/details/111409440)[^2^](https://blog.csdn.net/zx54633089/article/details/110943136)。

* [`WifiConfigController.java`：这个文件主要负责处理WiFi配置，包括扫描结果的处理。你可能需要在这个文件中找到处理扫描结果的函数，并进行修改](https://blog.csdn.net/frank_eos/article/details/111409440)[^1^](https://blog.csdn.net/frank_eos/article/details/111409440)[^2^](https://blog.csdn.net/zx54633089/article/details/110943136)。
* [`WifiSettings.java`：这个文件是WiFi设置的主界面，它会显示扫描到的WiFi网络列表。如果你想要修改显示的扫描结果，你可能需要在这个文件中进行修改](https://blog.csdn.net/frank_eos/article/details/111409440)[^1^](https://blog.csdn.net/frank_eos/article/details/111409440)[^2^](https://blog.csdn.net/zx54633089/article/details/110943136)。

请注意，这只是一个大致的指导，具体的实现可能会根据你的具体需求和AOSP版本的不同而有所不同。你可能需要阅读和理解更多的源码，以找到最适合你需求的解决方案。

[希望这些信息对你有所帮助！如果你有其他问题，欢迎随时向我提问。](https://blog.csdn.net/frank_eos/article/details/111409440)[^1^](https://blog.csdn.net/frank_eos/article/details/111409440)[^2^](https://blog.csdn.net/zx54633089/article/details/110943136)

---

[android 10 模仿Settings写WiFi控制 安卓模拟wifi软件_mob64ca14106f2f的技术博客_51CTO博客](https://blog.51cto.com/u_16213684/11060345)

getBSSID（）获取BSSID属性

getDetailedStateOf（）获取客户端的连接性

getHiddenSSID（）获取SSID是否隐藏

getIpAddress（）获取IP地址

getLinkSpeed（）获取连接的速度

getMacAddress（）获取Mac地址

getRssi（）获取802.11n网络的信号

getSSID（）获取SSID

getSupicanState（）获取有关特定客户端端状态的信息

[Fake Wifi Connection (伪装WIFI连接) v1.3 安卓版 下载-脚本之家 (jb51.net)](https://www.jb51.net/softs/188369.html)

---

`XposedMain.java` 在 `FakeWifi` 项目中主要通过以下步骤实现了模拟 WiFi 连接：

1. **初始化 Xposed 模块**：在 `initZygote` 方法中注册 Xposed 模块，使其在 Zygote 进程中初始化。
2. **处理应用加载**：在 `handleLoadPackage` 方法中，检测目标包的加载，并调用 `fakeWifiState` 方法。
3. **模拟 WiFi 状态**：在 `fakeWifiState` 方法中，通过 Xposed Hook 拦截和修改系统 API（如 `isWifiEnabled`、`getConnectionInfo` 等），返回虚假的 WiFi 连接信息，欺骗应用认为设备已连接到 WiFi。

通过这些步骤，`FakeWifi` 项目实现了 WiFi 连接状态的模拟。具体代码可以在 [这里](https://github.com/chylek/FakeWifi/blob/master/app/src/main/java/eu/chylek/adam/fakewifi/XposedMain.java) 查看。

### 详细步骤

1. **`initZygote`**

   - 注册 Xposed 模块，确保模块在 Zygote 进程中初始化。
2. **`handleLoadPackage`**

   - 当加载特定应用包时调用，通常用于修改特定应用的行为。
   - 在该方法中调用 `fakeWifiState` 以修改 WiFi 相关的方法。
3. **`fakeWifiState`**

   - 使用 Xposed API（如 `XposedHelpers.findAndHookMethod`）来拦截和修改与 WiFi 状态相关的方法。
   - 修改方法包括 `isWifiEnabled`、`getConnectionInfo` 等，返回预设的虚假数据。
   - 例如，`isWifiEnabled` 总是返回 `true`，`getConnectionInfo` 返回一个模拟的 `WifiInfo` 对象。

### 参考实现

您可以将类似的逻辑集成到 AOSP 10 源码中，通过修改 WiFi 管理相关的 Java 文件来实现模拟 WiFi 连接。以下是可能需要修改的文件：

- `frameworks/base/services/core/java/com/android/server/wifi/WifiServiceImpl.java`
- `frameworks/base/services/core/java/com/android/server/wifi/WifiStateMachine.java`

通过在这些文件中插入模拟逻辑，可以实现 WiFi 连接状态的虚假返回。

### 总结

通过分析 `FakeWifi` 项目，您可以学习到如何利用 Xposed Hook 修改系统方法以实现模拟 WiFi 连接，并将其应用到 AOSP 10 源码的修改中。需要注意的是，修改 AOSP 源码需要编译整个系统并部署到设备上进行测试。

# WIFI架构

![1719316364855](image/wifi/1719316364855.png)

[Android WiFi 架构总览（模块及接口）_示了android系统wifi模块的架构(当然,这只是软件的控制命令部分,数据部分直接通过-CSDN博客](https://blog.csdn.net/xusiwei1236/article/details/48495485)

![1719316831141](image/wifi/1719316831141.png)

[Android的Wifi系统框架分析第一篇_wifi在代码的组成结构中-CSDN博客](https://blog.csdn.net/qq_30624591/article/details/95937502?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7Ebaidujs_baidulandingword%7ECtr-1-95937502-blog-48495485.235%5Ev43%5Epc_blog_bottom_relevance_base7&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7Ebaidujs_baidulandingword%7ECtr-1-95937502-blog-48495485.235%5Ev43%5Epc_blog_bottom_relevance_base7&utm_relevant_index=1)

- WifiManager: 它是Wifi模块向外部应用透漏出来的接口，其它所有应用都可以通过WifiManager来操作Wifi的各项功能，但是WifiManager本身不具备处理请求的能力，而是把所有的请求转发给WifServiceImpl来处理。
- WifiService: Java Framework中Wifi功能的总入口，负责Wifi功能的核心业务。它是服务器端的实现，作为Wifi部分的核心，处理实际的驱动加载、扫描、链接、断开等命令，以及底层上报的事件。对于主动的命令控制，WiFi是一个简单的封装，针对来自客户端的控制命令，调用相应的WifiNative底层实现。
- WifiServiceImpl: 本身也不具备处理请求的能力，而是将请求分类后交给不同的处理者处理，比如WifiStateMachine。
- WifiStateMachine: 它是一个复杂的状态机，维护了Wifi的启动、扫描、连接、断开等多个状态。它运行自己独有的线程中，拥有自己的消息队列。
- WifiStateTracker: 除了负责WiFi的电源管理模式等功能外，其核心是WifiMonitor所实现的事件轮询机制，以及消息处理函数handleMessage()。
- WifiMonitor: 专门负责接收来自Wpa_supplicant的事件，并将这些信息进行分类再交予StateMachine处理。
- WifiNative: 一个接口类，主要是提供一些native方法用于wifi framework层和WPAS通信。WifiNative的主要实现都在wifi.c函数里,WifiNative不过是将其封装,供framework层调用。

特别注意：WifiService 和 WifiMonitor 是整个模块的核心。WifiService 负责启动关闭 wpa_supplicant、启动关闭 WifiMonitor 监视线程和把命令下发给 wpa_supplicant,而 WifiMonitor 则负责从 wpa_supplicant 接收事件通知。也就是说WifiService负责wifi整个流程的控制，而WifiMonitor负责监视底层的事件。

### frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java

```
public boolean startScan(String packageName)
```

这个代码片段是Android系统中 `WifiServiceImpl`类中的一个方法，用于启动Wi-Fi扫描。下面是详细的解释：

### 函数签名

```java
@Override
public boolean startScan(String packageName) {
```

- `@Override`：表示这是重写父类或接口中的方法。
- `public boolean startScan(String packageName)`：这是一个公开的、返回布尔值的方法，参数是调用该方法的应用程序的包名。

### 权限检查

```java
if (enforceChangePermission(packageName) != MODE_ALLOWED) {
    return false;
}
```

- `enforceChangePermission(packageName)`：检查调用者是否有权限进行操作。如果没有权限，返回 `false`。

### 获取调用者信息

```java
int callingUid = Binder.getCallingUid();
long ident = Binder.clearCallingIdentity();
mLog.info("startScan uid=%").c(callingUid).flush();
```

- `Binder.getCallingUid()`：获取调用该方法的应用程序的UID。
- `Binder.clearCallingIdentity()`：清除调用者的身份信息，记录原来的身份信息以便稍后恢复。
- `mLog.info`：记录日志信息，记录调用者的UID。

### 检查设备是否处于空闲模式

```java
synchronized (this) {
    if (mInIdleMode) {
        sendFailedScanBroadcast();
        mScanPending = true;
        return false;
    }
}
```

- `synchronized (this)`：确保以下代码块是线程安全的。
- `if (mInIdleMode)`：检查设备是否处于空闲模式。如果是，则发送失败的扫描广播，并将扫描挂起标记为 `true`，返回 `false`。

### 权限和扫描操作

```java
try {
    mWifiPermissionsUtil.enforceCanAccessScanResults(packageName, callingUid);
    Mutable<Boolean> scanSuccess = new Mutable<>();
    boolean runWithScissorsSuccess = mWifiInjector.getClientModeImplHandler()
            .runWithScissors(() -> {
                scanSuccess.value = mScanRequestProxy.startScan(callingUid, packageName);
            }, RUN_WITH_SCISSORS_TIMEOUT_MILLIS);
    if (!runWithScissorsSuccess) {
        Log.e(TAG, "Failed to post runnable to start scan");
        sendFailedScanBroadcast();
        return false;
    }
    if (!scanSuccess.value) {
        Log.e(TAG, "Failed to start scan");
        return false;
    }
} catch (SecurityException e) {
    Slog.e(TAG, "Permission violation - startScan not allowed for"
            + " uid=" + callingUid + ", packageName=" + packageName + ", reason=" + e);
    return false;
} finally {
    Binder.restoreCallingIdentity(ident);
}
```

- `try`：尝试执行以下代码，如果发生 `SecurityException`则捕获。
- `mWifiPermissionsUtil.enforceCanAccessScanResults(packageName, callingUid)`：检查调用者是否有权限访问扫描结果。
- `Mutable<Boolean> scanSuccess = new Mutable<>()`：创建一个可变的布尔值对象，存储扫描是否成功。
- `boolean runWithScissorsSuccess = mWifiInjector.getClientModeImplHandler().runWithScissors(...)`：通过 `Handler`在规定时间内执行扫描任务，并将结果存储在 `scanSuccess.value`中。
  - `runWithScissors`：确保在特定的时间内运行任务。
  - `scanSuccess.value = mScanRequestProxy.startScan(callingUid, packageName)`：实际启动扫描操作。
- `if (!runWithScissorsSuccess)`：检查任务是否成功运行。如果不成功，记录错误日志并发送失败的扫描广播，返回 `false`。
- `if (!scanSuccess.value)`：检查扫描是否成功。如果不成功，记录错误日志，返回 `false`。
- `catch (SecurityException e)`：捕获权限异常，记录错误日志，返回 `false`。
- `finally`：无论是否发生异常，都恢复调用者的身份信息。

### 返回成功

```java
return true;
```

- 如果上述所有操作都成功，则返回 `true`。

### 总结

这个方法通过一系列的权限检查和状态检查来确保Wi-Fi扫描操作的安全性和成功执行。如果任何一步失败（如权限不足、设备处于空闲模式、扫描操作失败等），都会适时地记录日志、发送广播并返回 `false`。

---

---

[Android中的Wifi框架知识点_android wifi-CSDN博客](https://blog.csdn.net/chenmi123321/article/details/119248132)

\- wiki 可空、取值范围







grep -n 'public\|private\|protected' packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java



./frameworks/base/wifi/java/android/net/wifi/WifiManager.java

```java
public WifiInfo getConnectionInfo() ->mService.getConnectionInfo(mContext.getOpPackageName());

public List<ScanResult> getScanResults() ->
mService.getScanResults(mContext.getOpPackageName());

public boolean isScanAlwaysAvailable() -> mService.isScanAlwaysAvailable()

    public boolean isWifiEnabled() {
        return getWifiState() == WIFI_STATE_ENABLED;
    }

```



[redroid-rockchip (github.com)](https://github.com/redroid-rockchip)

![image-20240711144644571](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240711144644571.png)

# 准备工作



宿主机需要开启mac80211_hwsim内核模块

```
CONFIG_MAC80211_HWSIM=y
```



宿主机需切换到iptables-legacy，然后重启

```bash
update-alternatives --set iptables /usr/sbin/iptables-legacy
update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
```























---

./frameworks/base/services/core/java/com/android/server/ConnectivityService.java

./frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java

![image-20240716163455762](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407161634984.png)



packages/apps/Settings/src/com/android/settings/wifi/WifiMasterSwitchPreferenceController.java                     private WifiEnabler mWifiEnabler

[packages](http://aospxref.com/android-10.0.0_r47/xref/packages/)/[apps](http://aospxref.com/android-10.0.0_r47/xref/packages/apps/)/[Settings](http://aospxref.com/android-10.0.0_r47/xref/packages/apps/Settings/)/[src](http://aospxref.com/android-10.0.0_r47/xref/packages/apps/Settings/src/)/[com](http://aospxref.com/android-10.0.0_r47/xref/packages/apps/Settings/src/com/)/[android](http://aospxref.com/android-10.0.0_r47/xref/packages/apps/Settings/src/com/android/)/[settings](http://aospxref.com/android-10.0.0_r47/xref/packages/apps/Settings/src/com/android/settings/)/[wifi](http://aospxref.com/android-10.0.0_r47/xref/packages/apps/Settings/src/com/android/settings/wifi/)/[WifiEnabler.java](http://aospxref.com/android-10.0.0_r47/xref/packages/apps/Settings/src/com/android/settings/wifi/WifiEnabler.java)

onSwitchToggled(boolean isChecked)

mWifiManager.setWifiEnabled(isChecked)



`WifiEnabler` 类中的 `onSwitchToggled` 函数是用于处理用户在设置页面中切换 WiFi 开关时的操作。这个函数具体做了以下几件事：

1. **检查是否由于状态机事件而触发**：
   ```java
   if (mStateMachineEvent) {
       return true;
   }
   ```
   如果是由于状态机事件（例如，系统状态改变）触发的开关操作，直接返回 `true`，不做进一步处理。

2. **检查飞行模式下是否允许开启 WiFi**：
   ```java
   if (isChecked && !WirelessUtils.isRadioAllowed(mContext, Settings.Global.RADIO_WIFI)) {
       Toast.makeText(mContext, R.string.wifi_in_airplane_mode, Toast.LENGTH_SHORT).show();
       // Reset switch to off. No infinite check/listener loop.
       mSwitchWidget.setChecked(false);
       return false;
   }
   ```
   如果用户试图在飞行模式下开启 WiFi，而系统设置不允许此操作，会显示一个提示信息，并将 WiFi 开关重置为关闭状态，避免无限的开关监听循环。

3. **记录用户操作**：
   ```java
   if (isChecked) {
       mMetricsFeatureProvider.action(mContext, SettingsEnums.ACTION_WIFI_ON);
   } else {
       // Log if user was connected at the time of switching off.
       mMetricsFeatureProvider.action(mContext, SettingsEnums.ACTION_WIFI_OFF, mConnected.get());
   }
   ```
   如果用户开启了 WiFi，会记录一次 `ACTION_WIFI_ON` 操作。如果用户关闭了 WiFi，并且在关闭时用户是连接状态，会记录一次 `ACTION_WIFI_OFF` 操作，附带当前连接状态。

4. **设置 WiFi 开关状态**：
   ```java
   if (!mWifiManager.setWifiEnabled(isChecked)) {
       // Error
       mSwitchWidget.setEnabled(true);
       Toast.makeText(mContext, R.string.wifi_error, Toast.LENGTH_SHORT).show();
   }
   ```
   尝试通过 `WifiManager` 设置 WiFi 的开启状态。如果设置失败，会重新启用 WiFi 开关并显示一个错误提示信息。

总的来说，这个函数处理了用户对 WiFi 开关的交互操作，确保在不同状态下正确地处理 WiFi 开关的开启和关闭操作，并提供用户反馈。

private void handleWifiStateChanged(int state) {
    mStateMachineEvent = true;
    switch (state) {
        case WifiManager.WIFI_STATE_ENABLING:
            // 更新 UI 以显示 WiFi 正在启用
            break;
        case WifiManager.WIFI_STATE_ENABLED:
            // 更新 UI 以显示 WiFi 已启用
            break;
        case WifiManager.WIFI_STATE_DISABLING:
            // 更新 UI 以显示 WiFi 正在禁用
            break;
        case WifiManager.WIFI_STATE_DISABLED:
            // 更新 UI 以显示 WiFi 已禁用
            break;
        default:
            // 处理其他状态
            break;
    }
    mStateMachineEvent = false;
}



mWifiManager.setWifiEnabled(isChecked)

./frameworks/base/wifi/java/android/net/wifi/WifiManager.java

mService.setWifiEnabled(mContext.getOpPackageName(), enabled)

IWifiManager service
interface IWifiManager;

`IWifiManager` 是一个 AIDL 接口，定义了 WiFi 服务的各种操作。`IWifiManager` 的具体实现是在 `WifiServiceImpl` 类中，这个类是 `IWifiManager` 接口的实际服务实现。在 AOSP 10 中，`WifiServiceImpl` 的代码通常位于以下目录：

```
frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java
```

### 相关源码结构

1. **AIDL 文件**：
   - `IWifiManager.aidl` 文件通常位于：
     ```
     frameworks/base/wifi/java/android/net/wifi/IWifiManager.aidl
     ```
   - 这个文件定义了 `IWifiManager` 接口的各种方法。

2. **实现类**：
   - `WifiServiceImpl` 类是 `IWifiManager` 接口的实现类，位于：
     ```
     frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java
     ```
   - 这个类实现了所有 `IWifiManager` 接口定义的方法，并提供了具体的业务逻辑。

### 具体实现

在 `WifiServiceImpl` 中，会实现 `IWifiManager` 接口的方法，并提供具体的操作。例如：

```java
public class WifiServiceImpl extends IWifiManager.Stub {
    // 构造函数和成员变量
    public WifiServiceImpl(Context context) {
        // 初始化操作
    }

    @Override
    public boolean setWifiEnabled(boolean enable) {
        // 具体实现WiFi开启/关闭的逻辑
    }

    // 其他IWifiManager接口方法的实现
}
```

### `WifiManager` 初始化

在 `WifiManager` 类的构造函数中，通过 `Context.getSystemService(Context.WIFI_SERVICE)` 获取到 `WifiServiceImpl` 的实例：

```java
public class WifiManager {
    private final Context mContext;
    private final IWifiManager mService;

    public WifiManager(Context context, IWifiManager service) {
        mContext = context;
        mService = service;
    }

    // 其他方法
}
```

在 `ContextImpl` 类中，当调用 `Context.getSystemService(Context.WIFI_SERVICE)` 时，会返回 `WifiServiceImpl` 的实例：

```java
@Override
public Object getSystemService(String name) {
    if (WIFI_SERVICE.equals(name)) {
        return WifiManager.getInstance();
    }
    // 其他服务的获取
}
```

`WifiManager.getInstance()` 会返回 `WifiManager` 的实例，而 `WifiManager` 的实例则持有 `WifiServiceImpl` 的引用。

### 总结

要找到 `WifiManager` 中 `IWifiManager` 的实现，可以查看以下文件和目录：

- `IWifiManager.aidl` 文件位于：
  ```
  frameworks/base/wifi/java/android/net/wifi/IWifiManager.aidl
  ```
- `WifiServiceImpl` 类的实现位于：
  ```
  frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java
  ```

希望这些信息对你有所帮助！如果你还有其他问题，欢迎继续提问。

frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java

public synchronized boolean setWifiEnabled(String packageName, boolean enable) 



frameworks/base/wifi/java/android/net/wifi/WifiManager.java

mService.getWifiEnabledState()

frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java

public int getWifiEnabledState() ->mClientModeImpl.syncGetWifiState()

mClientModeImpl = mWifiInjector.getClientModeImpl();

/[frameworks](http://aospxref.com/android-10.0.0_r47/xref/frameworks/)/[opt](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/)/[net](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/)/[wifi](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/)/[service](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/)/[java](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/)/[com](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/)/[android](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/android/)/[server](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/android/server/)/[wifi](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/android/server/wifi/)/[ClientModeManager.java](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/android/server/wifi/ClientModeManager.java)

[frameworks](http://aospxref.com/android-10.0.0_r47/xref/frameworks/)/[opt](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/)/[net](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/)/[wifi](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/)/[service](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/)/[java](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/)/[com](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/)/[android](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/android/)/[server](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/android/server/)/[wifi](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/android/server/wifi/)/[ClientModeImpl.java](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/net/wifi/service/java/com/android/server/wifi/ClientModeImpl.java)

```
    public int syncGetWifiState() {
        return mWifiState.get();
    }
```

private final AtomicInteger mWifiState = new AtomicInteger(WIFI_STATE_DISABLED);







---

packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java

onStart()->mWifiManager.getWifiState()->mService.getWifiEnabledState()

mMock.getWifiEnabledState(mClientModeImpl.syncGetWifiState());

frameworks/base/core/java/com/android/internal/space/api/WiFiMock.java

 mMap = mSpaceService.addMockCallback(NAME, this);

vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerService.java

mMockManager.addMockCallback(name, callback)

vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java

mockInfo = mMockMap.get(name);

private void loadMockInfo()
mockInfo.map.putAll(CommonHelper.readMapFile("/data/misc/mock/" + name + ".prop"));

mMockMap.put(name, mockInfo);

busybox vi /data/misc/mock/wifi.prop     重启生效

packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java

updateAccessPointPreferences()

packages/apps/Settings/src/com/android/settings/wifi/dpp/WifiNetworkListFragment.java

这两个文件都涉及到安卓系统中的Wi-Fi设置功能，特别是更新Wi-Fi网络列表的显示。它们的作用和主要区别如下：

### packages/apps/Settings/src/com/android/settings/wifi/dpp/WifiNetworkListFragment.java

**主要作用：**
`WifiNetworkListFragment`类主要用于显示Wi-Fi DPP（Device Provisioning Protocol）相关的Wi-Fi网络列表。`updateAccessPointPreferences`方法的作用是更新Wi-Fi网络的显示列表，特别是与Wi-Fi DPP配置相关的网络。

**方法详解：**
1. **检查Wi-Fi是否启用：** 如果Wi-Fi没有启用，则直接返回。
2. **获取已保存的Wi-Fi接入点：** 调用`WifiSavedConfigUtils.getAllConfigs`方法获取所有已保存的Wi-Fi接入点。
3. **过滤和排序：** 
   - 过滤出有效的DPP配置Wi-Fi网络。
   - 将可用的（reachable）Wi-Fi网络排在前面，并按名称排序。
4. **更新显示：**
   - 清空现有的Wi-Fi接入点显示。
   - 创建并添加新的Wi-Fi接入点显示，设置其可用性和顺序。
   - 如果`mIsTest`标志为真，添加一个假网络偏好项用于测试。

### packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java

**主要作用：**
`WifiSettings`类用于显示和管理所有的Wi-Fi网络，包括已连接和可用的网络。`updateAccessPointPreferences`方法的作用是更新Wi-Fi网络的显示列表，重点是用户当前可用的Wi-Fi网络。

**方法详解：**
1. **检查Wi-Fi是否启用：** 如果Wi-Fi没有启用，则直接返回。
2. **获取Wi-Fi接入点列表：** 从`mWifiTracker`中获取所有Wi-Fi接入点，并按其信号强度和状态排序。
3. **更新显示：**
   - 清除现有的Wi-Fi接入点显示。
   - 如果有已连接的Wi-Fi接入点，先配置并显示已连接的Wi-Fi接入点。
   - 遍历其他Wi-Fi接入点，过滤掉不可用的（out of range）接入点，并创建新的偏好项用于显示。
   - 如果`mOpenSsid`不为空且与当前接入点的SSID匹配，则进行特殊处理（如处理错误密码情况）。
   - 添加新的Wi-Fi接入点显示，并设置监听器和刷新。
   - 更新额外的设置摘要。
4. **处理空列表情况：** 
   - 如果没有可用的Wi-Fi接入点，显示一个提示信息。
   - 否则，延迟隐藏进度条以与动画同步。

### 方法作用的区别：

1. **应用场景不同：**
   - `WifiNetworkListFragment`中的`updateAccessPointPreferences`主要用于DPP相关的Wi-Fi网络列表更新。
   - `WifiSettings`中的`updateAccessPointPreferences`用于一般的Wi-Fi设置页面，处理所有Wi-Fi网络的显示和管理。

2. **处理的Wi-Fi接入点不同：**
   - `WifiNetworkListFragment`专注于已保存的Wi-Fi接入点，并进行DPP相关的过滤和排序。
   - `WifiSettings`处理所有可用的Wi-Fi接入点，包括已连接和未连接的网络。

3. **显示逻辑不同：**
   - `WifiNetworkListFragment`按可用性和名称排序Wi-Fi接入点。
   - `WifiSettings`按信号强度和状态排序，并额外处理空列表的情况。

这两个方法都涉及更新Wi-Fi网络列表，但在应用场景、处理的Wi-Fi接入点类型和显示逻辑上有所不同。



packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java

updateAccessPointPreferences()

List<AccessPoint> accessPoints = mWifiTracker.getAccessPoints();

**frameworks/base/packages/SettingsLib/src/com/android/settingslib/wifi/WifiTracker.java**   

List<AccessPoint> accessPoints = new ArrayList<>(mInternalAccessPoints);

packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java的mWifiTracker.getAccessPoints()里

updateAccessPoints(final List<ScanResult> newScanResults,List<WifiConfiguration> configs)

frameworks/base/wifi/java/android/net/wifi/ScanResult.java





---

### s9写入config状态
vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerShellCommand.java

runUpdateConfig(PrintWriter pw)

mService.updateMock(addMap, delList); mService -》Space9dManagerService

vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerService.java

mMockManager.updateMock((Map<String, Object>)addMap, (List<String>)removeKeys)

mMockMap.get(name).map.put(toMockKey(item), addMap.get(item));

mMockMap =》 loadMockInfo()



所以整个过程只有一个Map，是MockManager的mMockMap的某个map

---

### wifiSetting读取wifi状态

packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java

wifiState = mWifiManager.getWifiState()

frameworks/base/wifi/java/android/net/wifi/WifiManager.java

mService.getWifiEnabledState()      mService=》WifiServiceImpl

frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java

mMock.getWifiEnabledState(mClientModeImpl.syncGetWifiState())

frameworks/base/core/java/com/android/internal/space/api/WiFiMock.java

enable = (boolean) (mMap.getOrDefault("enable", true))出现Map

mMap = mSpaceService.addMockCallback(NAME, this);

vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerService.java

mMockManager.addMockCallback(name, callback)

vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java

```java
	Map<String, Object> result = new ArrayMap();

	result.putAll(mockInfo.map);

return result;
```

---

### s9写入属性时持久化操作

vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java

```java
updateMock(Map<String, Object> addMap, List<String> removeKeys){
	//1. 添加mMockMap.get(name).map.put(toMockKey(item), addMap.get(item));
	//2. 删除mMockMap.get(name).map.remove(toMockKey(item));
    
	//3. 同步写入syncMockInfo(name, arrayMap);
    //4. 让wifimock的map等于新mockInfo.callback.onCallback(arrayMap);
}

frameworks/base/core/java/com/android/internal/space/api/WiFiMock.java

  @Override

  public void onCallback(Map map) {

    this.mMap = map;

  }
```



## wifi设置开关按钮

这个方法是AOSP 10中用于设置WiFi开关状态的主要方法之一。它的作用是根据传入的参数启用或禁用WiFi。在这个方法中，有几个关键步骤和检查来确保操作的安全性和合法性。

### 代码分析

1. **权限检查**
   ```java
   if (enforceChangePermission(packageName) != MODE_ALLOWED) {
       return false;
   }
   ```
   检查调用者是否具有更改WiFi状态的权限。

2. **特权检查**
   ```java
   boolean isPrivileged = isPrivileged(Binder.getCallingPid(), Binder.getCallingUid());
   if (!isPrivileged && !isDeviceOrProfileOwner(Binder.getCallingUid())
           && !mWifiPermissionsUtil.isTargetSdkLessThan(packageName, Build.VERSION_CODES.Q,
             Binder.getCallingUid())
           && !isSystem(packageName, Binder.getCallingUid())) {
       mLog.info("setWifiEnabled not allowed for uid=%")
               .c(Binder.getCallingUid()).flush();
       return false;
   }
   ```
   确认调用者是否为特权用户（如系统应用或设备所有者等）。

3. **飞行模式检查**
   ```java
   if (mSettingsStore.isAirplaneModeOn() && !isPrivileged) {
       mLog.err("setWifiEnabled in Airplane mode: only Settings can toggle wifi").flush();
       return false;
   }
   ```
   如果启用了飞行模式，只有特权应用才能更改WiFi状态。

4. **热点状态检查**
   ```java
   boolean apEnabled = mWifiApState == WifiManager.WIFI_AP_STATE_ENABLED;
   if (apEnabled && !isPrivileged) {
       mLog.err("setWifiEnabled SoftAp enabled: only Settings can toggle wifi").flush();
       return false;
   }
   ```
   如果启用了热点，只有特权应用才能更改WiFi状态。

5. **加密守护进程检查**
   ```java
   if (mFrameworkFacade.inStorageManagerCryptKeeperBounce()) {
       return false;
   }
   ```
   如果系统处于加密守护进程的跳跃状态，则忽略任何WiFi状态更改请求。

6. **记录日志和清除调用者身份**
   ```java
   mLog.info("setWifiEnabled package=% uid=% enable=%").c(packageName)
           .c(Binder.getCallingUid()).c(enable).flush();
   long ident = Binder.clearCallingIdentity();
   ```

7. **处理WiFi切换**
   
   ```java
   try {
       if (!mSettingsStore.handleWifiToggled(enable)) {
           return true;
       }
   } finally {
       Binder.restoreCallingIdentity(ident);
   }
   ```

### 关键方法解释

1. **mSettingsStore.handleWifiToggled(enable)**
   这个方法的主要作用是更新WiFi状态并进行相关设置存储。

   ```java
   public synchronized boolean handleWifiToggled(boolean wifiEnabled) {
       if (wifiEnabled) {
           if (isAirplaneModeOn() && !isAirplaneToggleable()) {
               // Airplane mode is on and wifi is not allowed to be toggled in airplane mode
               return false;
           }
           persistWifiState(true);
       } else {
           persistWifiState(false);
       }
       return true;
   }
   ```
   `handleWifiToggled`方法会根据传入的参数（true或false）来设置WiFi的启用或禁用状态。该方法会检查飞行模式以及是否允许在飞行模式下切换WiFi，并将WiFi状态持久化存储。

2. **mWifiMetrics.incrementNumWifiToggles(isPrivileged, enable)**
   这个方法主要用于记录WiFi开关切换的次数，用于统计和分析。

   ```java
   public void incrementNumWifiToggles(boolean isPrivileged, boolean enable) {
       if (enable) {
           mWifiOnMetrics.increment(isPrivileged);
       } else {
           mWifiOffMetrics.increment(isPrivileged);
       }
   }
   ```
   该方法会根据WiFi是启用还是禁用，以及调用者是否为特权用户来增加相应的计数器。

### 总结

`setWifiEnabled`方法通过一系列权限检查和状态检查，确保调用者有权更改WiFi状态，并在合适的条件下调用`mSettingsStore.handleWifiToggled(enable)`来实际执行WiFi开关操作。`mWifiMetrics.incrementNumWifiToggles(isPrivileged, enable)`用于记录WiFi开关操作的统计数据。这些机制共同保证了WiFi状态更改的安全性和可靠性。



在AOSP 10中，`Settings.Global.putInt(cr, Settings.Global.WIFI_ON, state)` 这个方法实际上是将WiFi的状态存储在全局设置中。这个方法将WiFi的状态（启用或禁用）写入系统的设置数据库，从而更新WiFi开关的状态。

### `persistWifiState(int state)` 方法分析

```java
private void persistWifiState(int state) {
    Log.d("wifi-","---WifiSettingsStore.persistWifiState(int state) ----");

    final ContentResolver cr = mContext.getContentResolver();
    mPersistWifiState = state;
    Settings.Global.putInt(cr, Settings.Global.WIFI_ON, state);
}
```

这个方法的核心部分是调用 `Settings.Global.putInt(cr, Settings.Global.WIFI_ON, state)`，它将WiFi的状态存储在 `Settings.Global.WIFI_ON` 这个全局设置项中。

### `Settings.Global.putInt(ContentResolver cr, String name, int value)` 方法

`Settings.Global.putInt` 是一个静态方法，用于将指定的整数值写入到全局设置数据库中。它的实现位于 `frameworks/base/core/java/android/provider/Settings.java` 文件中：

```java
public static boolean putInt(ContentResolver cr, String name, int value) {
    return putLongForUser(cr, name, value, cr.getUserId());
}

public static boolean putLongForUser(ContentResolver cr, String name, long value, int userHandle) {
    return putForUser(cr, name, Long.toString(value), userHandle);
}

public static boolean putForUser(ContentResolver cr, String name, String value, int userHandle) {
    return sNameValueCache.putStringForUser(cr, name, value, userHandle);
}
```

`putInt` 方法最终调用了 `sNameValueCache.putStringForUser` 方法，它将数据写入到数据库中。

### `NameValueCache.putStringForUser` 方法

`NameValueCache` 是一个内部类，负责缓存设置项并将它们写入到实际的数据库中：

```java
private static final class NameValueCache {
    private final String mVersionSystemProperty;
    private final Uri mUri;
    private final String mCallGetCommand;
    private final String mCallSetCommand;
    private final ArrayMap<String, String> mValues = new ArrayMap<>();

    public boolean putStringForUser(ContentResolver cr, String name, String value, int userHandle) {
        try {
            Bundle arg = new Bundle();
            arg.putString(SETTINGS_CALL_METHOD_USER_KEY, Integer.toString(userHandle));
            arg.putString("value", value);
            cr.call(mUri, mCallSetCommand, name, arg);
            return true;
        } catch (RemoteException e) {
            return false;
        }
    }
}
```

在这个方法中，调用了 `ContentResolver.call` 方法将设置项的值写入数据库。

### `ContentResolver.call` 方法

`ContentResolver.call` 方法通过 ContentProvider 机制将数据写入到数据库中：

```java
public final @Nullable Bundle call(@NonNull Uri uri, @NonNull String method,
        @Nullable String arg, @Nullable Bundle extras) {
    IContentProvider provider = acquireProvider(uri);
    if (provider == null) {
        throw new IllegalArgumentException("Unknown URI " + uri);
    }
    try {
        return provider.call(mPackageName, mAttributionTag, uri.getAuthority(), method, arg, extras);
    } catch (RemoteException e) {
        return null;
    } finally {
        releaseProvider(provider);
    }
}
```

这个方法通过调用 `IContentProvider.call` 将设置项写入数据库。对于 `Settings.Global.WIFI_ON`，会使用 `SettingsProvider` 来处理。

### `SettingsProvider`

`SettingsProvider` 位于 `frameworks/base/packages/SettingsProvider/src/com/android/providers/settings/SettingsProvider.java` 文件中。它是系统设置的实际存储位置，处理对 `Settings.Global` 的读写请求。

### 具体处理流程

当 `Settings.Global.putInt` 被调用时，`SettingsProvider` 中的 `call` 方法会被触发，它处理 `Settings.Global.WIFI_ON` 的设置请求：

```java
@Override
public Bundle call(String callingPkg, String method, String arg, Bundle extras) {
    if (METHOD_SET_GLOBAL.equals(method)) {
        putGlobalString(arg, extras.getString("value"));
    }
    // 其他方法处理...
}
```

在这个方法中，会调用 `putGlobalString` 方法将值写入到数据库中。

### `putGlobalString` 方法

```java
private boolean putGlobalString(String name, String value) {
    return putString(Settings.Global.CONTENT_URI, name, value, UserHandle.USER_CURRENT);
}
```

### `putString` 方法

```java
private boolean putString(Uri uri, String name, String value, int userHandle) {
    ContentValues values = new ContentValues();
    values.put(Settings.NameValueTable.NAME, name);
    values.put(Settings.NameValueTable.VALUE, value);
    return mOpenHelper.getWritableDatabase().insert(TABLE_GLOBAL, null, values) != -1;
}
```

### 总结

通过 `Settings.Global.putInt(cr, Settings.Global.WIFI_ON, state)` 方法，WiFi 状态被写入到全局设置数据库中，对应的设置项是 `Settings.Global.WIFI_ON`。当这个值被更新时，系统会根据新的设置值（0 表示关闭，1 表示打开）来切换 WiFi 的开关状态。这个机制确保了 WiFi 状态的持久化存储和系统设置的一致性。

### 开关全流程梳理

> - packages/apps/Settings/src/com/android/settings/wifi/WifiEnabler.java
>
>   onSwitchToggled(boolean isChecked)
>
> - frameworks/base/wifi/java/android/net/wifi/WifiManager.java
>
>   setWifiEnabled(boolean enabled)
>
> - frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java
>
>   setWifiEnabled(String packageName, boolean enable)
>
> - frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiSettingsStore.java
>
>   handleWifiToggled(boolean wifiEnabled)
>
>   persistWifiState(int state)
>
>   Settings.Global.putInt(cr, Settings.Global.WIFI_ON, state);
>
> - frameworks/base/core/java/android/provider/Settings.java
>
>   Global::putInt(ContentResolver cr, String name, int value)
>
>   putStringForUser(resolver, name, value, null, false, resolver.getUserId())
>
>   putStringForUser(@NonNull ContentResolver resolver,
>
>   ​        @NonNull String name, @Nullable String value, @Nullable String tag,
>
>   ​        boolean makeDefault, @UserIdInt int userHandle)



### 原AOSP获取wifi状态全流程

> - frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java
>
>   getWifiEnabledState() ->mClientModeImpl.syncGetWifiState()
>
> - frameworks/opt/net/wifi/service/java/com/android/server/wifi/ClientModeImpl.java
>
>   syncGetWifiState() ->mWifiState.get()
>
>   setWifiStateForApiCalls(int newState) mWifiState.set(newState)
>
>   反推-----
>
> - frameworks/opt/net/wifi/service/java/com/android/server/wifi/ClientModeManager.java
>
>   updateWifiState(int newState, int currentState)  ->mClientModeImpl.setWifiStateForApiCalls(newState);

#### wifi的updateWifiState

![image-20240718154815971](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407181548081.png)

根据 `jgrep` 命令输出的结果，列出了涉及 `updateWifiState` 方法的文件和代码行。以下是对这些文件和方法功能的解释：

### 1. `BatteryStatsImpl.java`
路径: `./base/core/java/com/android/internal/os/BatteryStatsImpl.java:10710`

```java
public void updateWifiState(@Nullable final WifiActivityEnergyInfo info) {
```

**功能**: 
- 用于更新电池统计信息中的 WiFi 状态。这与设备的电池使用情况和 WiFi 活动相关。

### 2. `WifiStatusTracker.java`
路径: `./base/packages/SettingsLib/src/com/android/settingslib/wifi/WifiStatusTracker.java:110`, `112`, `138`

```java
private void updateWifiState() {
```

**功能**: 
- 跟踪 WiFi 状态变化，并更新相应的状态信息。这通常用于 UI 层，显示 WiFi 状态给用户。

### 3. `WifiTracker.java`
路径: `./base/packages/SettingsLib/src/com/android/settingslib/wifi/WifiTracker.java:925`, `957`

```java
private void updateWifiState(int state) {
```

**功能**: 
- 主要用于跟踪 WiFi 状态，并在状态发生变化时进行相应的处理。这也涉及到 WiFi 状态的显示和管理。

### 4. `DemoStatusIcons.java`
路径: `./base/packages/SystemUI/src/com/android/systemui/statusbar/phone/DemoStatusIcons.java:226`

```java
public void updateWifiState(WifiIconState state) {
```

**功能**: 
- 用于在系统状态栏的演示模式中更新 WiFi 图标的状态。

### 5. `StatusBarIconController.java`
路径: `./base/packages/SystemUI/src/com/android/systemui/statusbar/phone/StatusBarIconController.java:373`

```java
mDemoStatusIcons.updateWifiState(state);
```

**功能**: 
- 调用 `DemoStatusIcons` 类的方法来更新状态栏中的 WiFi 图标状态。

### 6. `BatteryStatsService.java`
路径: `./base/services/core/java/com/android/server/am/BatteryStatsService.java:1101`

```java
mStats.updateWifiState(info);
```

**功能**: 
- 服务层方法，用于更新电池统计信息中的 WiFi 状态。这与 `BatteryStatsImpl` 类似，提供服务端的统计更新。

### 7. `BatteryExternalStatsWorker.java`
路径: `./base/services/core/java/com/android/server/am/BatteryExternalStatsWorker.java:506`

```java
mStats.updateWifiState(extractDeltaLocked(wifiInfo));
```

**功能**: 
- 同样用于电池统计信息的更新，这里处理外部的统计数据。

### 8. `ClientModeManager.java`
路径: `./opt/net/wifi/service/java/com/android/server/wifi/ClientModeManager.java:82`, `85`, `133`, `224`, `232`, `234`, `259`, `269`, `292`, `303`, `327`

```java
private void updateWifiState(int newState, int currentState) {
```

**功能**: 
- 主要用于管理客户端模式下的 WiFi 状态变化，处理从启用到禁用的各种状态过渡。

### 9. `ScanOnlyModeManager.java`
路径: `./opt/net/wifi/service/java/com/android/server/wifi/ScanOnlyModeManager.java:127`, `202`, `225`, `259`, `278`

```java
private void updateWifiState(int state) {
```

**功能**: 
- 用于管理仅扫描模式下的 WiFi 状态。这与 `ClientModeManager` 类似，但只涉及扫描功能，不包括连接功能。

### 总结

这些文件和方法共同作用于不同层级和模块的 WiFi 状态管理：

- **电池统计相关** (`BatteryStatsImpl.java`, `BatteryStatsService.java`, `BatteryExternalStatsWorker.java`)：用于跟踪和更新 WiFi 状态对电池的影响。
- **UI 相关** (`WifiStatusTracker.java`, `WifiTracker.java`, `DemoStatusIcons.java`, `StatusBarIconController.java`)：用于跟踪和更新 WiFi 状态，并在 UI 中显示。
- **系统服务和管理相关** (`ClientModeManager.java`, `ScanOnlyModeManager.java`)：用于管理 WiFi 的不同模式和状态转换。

这些方法共同确保 WiFi 状态的准确跟踪、管理和显示，从底层统计到用户界面的各个方面。





根据 `jgrep` 的输出结果，以下是涉及 `ClientModeManager` 的文件及其主要功能的解释：

### 1. `ActiveModeWarden.java`
路径: `./opt/net/wifi/service/java/com/android/server/wifi/ActiveModeWarden.java`

```java
private ClientModeManager.Listener mClientModeCallback;
```

**功能**:
- `ActiveModeWarden` 负责管理 WiFi 模式的激活和状态，包括客户端模式、扫描模式等。它通过监听 `ClientModeManager` 的状态变化来管理不同模式的切换。

### 2. `ClientModeImpl.java`
路径: `./opt/net/wifi/service/java/com/android/server/wifi/ClientModeImpl.java`

```java
private ClientModeManager.Listener mClientModeCallback = null;
```

**功能**:
- `ClientModeImpl` 是具体实现客户端模式的类，它实现了 WiFi 连接的管理，包括连接、断开连接、配置等。它通过 `ClientModeManager.Listener` 监听状态变化。

### 3. `ClientModeManager.java`
路径: `./opt/net/wifi/service/java/com/android/server/wifi/ClientModeManager.java`

```java
public class ClientModeManager implements ActiveModeManager {
```

**功能**:
- `ClientModeManager` 是核心类，负责管理客户端模式下的 WiFi 连接和状态。它实现了 `ActiveModeManager` 接口，提供管理 WiFi 状态的方法。

### 4. `SarManager.java`
路径: `./opt/net/wifi/service/java/com/android/server/wifi/SarManager.java`

```java
// Tracking the STA state through calls from the ClientModeManager.
```

**功能**:
- `SarManager` 负责管理 WiFi 发射功率调整，以符合特定的 SAR（Specific Absorption Rate）法规。它通过 `ClientModeManager` 跟踪 STA（Station）状态。

### 5. `WifiController.java`
路径: `./opt/net/wifi/service/java/com/android/server/wifi/WifiController.java`

```java
private ClientModeManager.Listener mClientModeCallback = new ClientModeCallback();
```

**功能**:
- `WifiController` 是 WiFi 管理的主要控制器，负责处理 WiFi 的各种状态和事件。它通过 `ClientModeManager.Listener` 监听客户端模式的状态变化，并作出相应的控制。

### 6. `WifiInjector.java`
路径: `./opt/net/wifi/service/java/com/android/server/wifi/WifiInjector.java`

```java
public ClientModeManager makeClientModeManager(ClientModeManager.Listener listener) {
```

**功能**:
- `WifiInjector` 是一个依赖注入类，负责创建 `ClientModeManager` 实例并注入所需的依赖。它通过 `makeClientModeManager` 方法创建 `ClientModeManager` 实例，并注册状态变化监听器。

### 功能总结

这些文件和类共同作用于 Android WiFi 子系统的管理和控制：

1. **`ActiveModeWarden`**：管理和切换不同的 WiFi 模式（如客户端模式和扫描模式）。
2. **`ClientModeImpl`**：具体实现客户端模式的功能，包括 WiFi 连接管理。
3. **`ClientModeManager`**：核心管理类，负责整体客户端模式下的 WiFi 状态和连接。
4. **`SarManager`**：管理 WiFi 发射功率，以符合 SAR 法规。
5. **`WifiController`**：处理 WiFi 状态和事件的主要控制器。
6. **`WifiInjector`**：负责创建和注入 WiFi 管理类的依赖。

通过这些类和文件的协同工作，Android 系统能够高效地管理和控制 WiFi 的各种状态和模式。







### 下拉框关闭WiFi

```
WifiManager.setWifiEnabled(boolean enabled)
WifiServiceImpl.setWifiEnabled(String packageName, boolean enable)
WifiSettingsStore.handleWifiToggled(boolean wifiEnabled)
WifiSettingsStore.persistWifiState(int state)
state:0
```

### 下拉框打开wifi

```
WifiManager.setWifiEnabled(boolean enabled)
WifiServiceImpl.setWifiEnabled(String packageName, boolean enable)
WifiSettingsStore.handleWifiToggled(boolean wifiEnabled)
WifiSettingsStore.persistWifiState(int state)
state:1
    ClientModeManager.updateWifiState(int newState, int currentState)
    ClientModeImpl.setWifiStateForApiCalls(int newState) 
    mWifiState:2
    WifiStatusTracker.handleBroadcast(Intent intent)
    WifiStatusTracker.updateWifiState()
    wifimanager.getWifiState()
    wifiserviceImpl.getWifiEnabledState()
    -ClientModeImpl.syncGetWifiState() 
    mWifiState:2
```



### wifi设置获取状态

````
wifimanager.getWifiState()
wifiserviceImpl.getWifiEnabledState()
ClientModeImpl.syncGetWifiState()
WiFiMock.getWifiEnabledState()
enable:true
````



### wifi设置获取状态

```
wifimanager.getWifiState()
wifiserviceImpl.getWifiEnabledState()
ClientModeImpl.syncGetWifiState()
mWifiState:1
WiFiMock.getScanResults() 
    wifimanager.getWifiState（）
    wifiserviceImpl.getWifiEnabledState()
    ClientModeImpl.syncGetWifiState()
    mWifiState:1
WifiTracker.onReceive(Context context, Intent intent)
WifiTracker.updateWifiState(int state)
WifiStatusTracker.handleBroadcast(Intent intent)
WifiStatusTracker.updateWifiState()
    wifimanager.getWifiState()
    wifiserviceImpl.getWifiEnabledState()
    ClientModeImpl.syncGetWifiState()
    mWifiState:1
```



### wifi设置关闭wifi

```
WifiEnabler.onSwitchToggled(boolean isChecked)
WifiManager.setWifiEnabled(boolean enabled)
WifiServiceImpl.setWifiEnabled(String packageName, boolean enable)
WifiSettingsStore.handleWifiToggled(boolean wifiEnabled)
WifiSettingsStore.persistWifiState(int state)
```

### wifi设置打开wifi

```
// 打开按钮
WifiEnabler.onSwitchToggled(boolean isChecked)
WifiManager.setWifiEnabled(boolean enabled)
WifiServiceImpl.setWifiEnabled(String packageName, boolean enable)
WifiSettingsStore.handleWifiToggled(boolean wifiEnabled)
WifiSettingsStore.persistWifiState(int state)
	Settings.Global.putInt(cr, Settings.Global.WIFI_ON, state);

//开启中
ClientModeManager.ClientModeStateMachine.processMessage(Message message)
ClientModeManager.updateWifiState(int newState, int currentState)
	newState:2 currentState:1
ClientModeImpl.setWifiStateForApiCalls(int newState)
	mWifiState.set(newState);

// 干什么？
WifiStatusTracker.handleBroadcast(Intent intent)
WifiStatusTracker.updateWifiState()
        state = mWifiManager.getWifiState();
            wifiserviceImpl.getWifiEnabledState()
            ClientModeImpl.syncGetWifiState()
                mWifiState.get();
        enabled = state == WifiManager.WIFI_STATE_ENABLED;

//????	
WifiTracker.onReceive(Context context, Intent intent)
WifiTracker.updateWifiState(int state)
		state = mWifiManager.getWifiState();
            wifiserviceImpl.getWifiEnabledState()
            ClientModeImpl.syncGetWifiState()
                mWifiState.get();
//k              
WifiEnabler.onSwitchToggled(boolean isChecked)
wifimanager.getWifiState()
wifiserviceImpl.getWifiEnabledState()
ClientModeImpl.syncGetWifiState()
wifiSettings.onWifiStateChanged(int state)

```





```
    public static final int WIFI_STATE_DISABLING = 0;

    public static final int WIFI_STATE_DISABLED = 1;

    public static final int WIFI_STATE_ENABLING = 2;

    public static final int WIFI_STATE_ENABLED = 3;

    public static final int WIFI_STATE_UNKNOWN = 4;
```

---

### 下拉框

frameworks/base/packages/SystemUI/src/com/android/systemui/qs/tiles/WifiTile.java

final CallbackInfo cb = mSignalCallback.mInfo;

在 `WifiTile` 类中获取 WiFi 状态的关键方法是 `handleUpdateState(SignalState state, Object arg)`。通过分析该方法可以看到，它使用了 `mSignalCallback.mInfo` 来获取当前 WiFi 的状态信息。

下面是该方法中的关键部分：

```java
@Override
protected void handleUpdateState(SignalState state, Object arg) {
    if (DEBUG) Log.d(TAG, "handleUpdateState arg=" + arg);
    final CallbackInfo cb = mSignalCallback.mInfo;
    //...（省略部分代码）
    boolean wifiConnected = cb.enabled && (cb.wifiSignalIconId > 0) && (cb.ssid != null);
    boolean wifiNotConnected = (cb.wifiSignalIconId > 0) && (cb.ssid == null);
    boolean enabledChanging = state.value != cb.enabled;
    //...（省略部分代码）
    state.value = transientEnabling || cb.enabled;
    state.activityIn = cb.enabled && cb.activityIn;
    state.activityOut = cb.enabled && cb.activityOut;
    //...（省略部分代码）
}
```

从上述代码可以看出，`mSignalCallback.mInfo` 是 WiFi 状态的主要数据来源。具体而言，`cb.enabled` 表示 WiFi 是否已启用，`cb.wifiSignalIconId` 表示 WiFi 信号图标的 ID，`cb.ssid` 表示连接的 WiFi 网络的 SSID。

为了深入了解 `mSignalCallback.mInfo` 是如何获取到 WiFi 状态信息的，我们需要查看 `mSignalCallback` 的定义和初始化。

### `mSignalCallback` 的定义和初始化

通常情况下，`mSignalCallback` 可能是通过监听 WiFi 状态变化的回调接口实现的。我们需要查找 `WifiTile` 类中的 `mSignalCallback` 的定义和赋值。

在 `WifiTile` 类中，`mSignalCallback` 的定义如下：

```java
private final SignalCallback mSignalCallback = new SignalCallback();
```

`SignalCallback` 是一个内部类，它实现了 `CallbackInfo` 接口，负责处理 WiFi 状态变化。

### `SignalCallback` 内部类

以下是 `SignalCallback` 类的部分实现：

```java
private final class SignalCallback implements NetworkController.SignalCallback {
    final CallbackInfo mInfo = new CallbackInfo();

    @Override
    public void setWifiIndicators(WifiIndicators indicators) {
        if (indicators.qsIcon != null) {
            mInfo.enabled = indicators.enabled;
            mInfo.wifiSignalIconId = indicators.qsIcon.icon;
            mInfo.ssid = indicators.ssid;
            mInfo.activityIn = indicators.activityIn;
            mInfo.activityOut = indicators.activityOut;
            mInfo.isTransient = indicators.transient;
            mInfo.statusLabel = indicators.statusLabel;
            refreshState();
        }
    }
}
```

从上述代码可以看到，`SignalCallback` 内部类通过实现 `NetworkController.SignalCallback` 接口，并在 `setWifiIndicators` 方法中更新 WiFi 状态信息。`indicators` 参数包含了 WiFi 的状态信息，如是否启用 (`enabled`)、信号图标 (`qsIcon.icon`)、SSID (`ssid`) 等。

### 总结

在 `WifiTile` 类中，WiFi 开关状态通过 `SignalCallback` 内部类的 `setWifiIndicators` 方法获取，并存储在 `CallbackInfo` 对象中。`handleUpdateState` 方法使用 `mSignalCallback.mInfo` 获取当前 WiFi 的状态，并根据这些状态更新 WiFi Tile 的显示。

具体来说，WiFi 开关状态主要由 `CallbackInfo` 中的 `enabled` 字段表示，它在 `setWifiIndicators` 方法中根据 `WifiIndicators` 参数进行更新。

### 下拉框状态栏获取WiFi状态

```
WifiSignalController.notifyListeners(SignalCallback callback)
	callback.setWifiIndicators(mCurrentState.enabled, ...
WifiTile WifiSignalCallback setWifiIndicators
	mInfo.enabled = enabled;
    mInfo.connected = qsIcon.visible;
WifiSignalController.notifyListeners(SignalCallback callback)

WifiTile.handleUpdateState(SignalState state, Object arg)
	wifiConnected = cb.enabled 
WifiTile.handleUpdateState(SignalState state, Object arg)
WifiTile.handleUpdateState(SignalState state, Object arg)
```

这些文件涉及到多个层次的WiFi管理和显示，从底层服务到系统界面及用户设置。以下是对每个文件及其作用的详细解释：

### 1. `base/core/java/com/android/internal/space/api/WiFiMock.java`
#### 主要作用：
这个文件可能用于模拟WiFi连接和状态。通常用于测试或开发环境下，模拟真实的WiFi行为而无需实际的硬件支持。

### 2. `base/packages/SettingsLib/src/com/android/settingslib/wifi/WifiStatusTracker.java`
#### 主要作用：
这个文件用于跟踪和更新WiFi的状态信息。它负责从系统中获取当前的WiFi状态，并将这些信息传递给相关组件，以便在界面上显示。

### 3. `base/packages/SettingsLib/src/com/android/settingslib/wifi/WifiTracker.java`
#### 主要作用：
用于跟踪WiFi网络的变化情况，如扫描结果、连接状态变化等。它提供了回调机制，可以让其他组件监听WiFi状态的变化。

### 4. `base/packages/SystemUI/src/com/android/systemui/qs/tiles/WifiTile.java`
#### 主要作用：
实现快速设置面板中的WiFi开关Tile。负责处理用户交互（如点击、长按），并根据WiFi状态更新Tile的显示。

### 5. `base/packages/SystemUI/src/com/android/systemui/statusbar/phone/DemoStatusIcons.java`
#### 主要作用：
用于在系统状态栏中显示WiFi等状态图标。这个文件可能涉及到状态栏图标的演示模式，用于测试或演示状态栏图标的变化。

### 6. `base/packages/SystemUI/src/com/android/systemui/statusbar/phone/StatusBarIconController.java`
#### 主要作用：
管理状态栏中图标的显示和更新，包括WiFi图标。根据系统状态和事件，更新图标的显示状态。

### 7. `base/packages/SystemUI/src/com/android/systemui/statusbar/policy/WifiSignalController.java`
#### 主要作用：
用于控制和更新WiFi信号图标。它监控WiFi信号强度和连接状态的变化，并将这些变化反映到状态栏的WiFi图标上。

### 8. `base/wifi/java/android/net/wifi/WifiManager.java`
#### 主要作用：
提供了应用程序接口(API)来管理WiFi连接和配置。开发者可以使用这个类来开启/关闭WiFi，扫描可用网络，连接到指定网络等。

### 9. `opt/net/wifi/service/java/com/android/server/wifi/ClientModeImpl.java`
#### 主要作用：
WiFi客户端模式的具体实现。处理WiFi连接的建立、维持和断开。这个文件是WiFi连接管理的核心部分。

### 10. `opt/net/wifi/service/java/com/android/server/wifi/ClientModeManager.java`
#### 主要作用：
管理WiFi客户端模式的生命周期和状态。负责在不同模式之间进行切换，并处理模式变化的逻辑。

### 11. `opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java`
#### 主要作用：
WiFi服务的实现类，提供系统级的WiFi管理功能。处理来自应用层的WiFi管理请求，并与底层WiFi硬件和驱动交互。

### 12. `opt/net/wifi/service/java/com/android/server/wifi/WifiSettingsStore.java`
#### 主要作用：
存储和管理WiFi相关的设置和配置。负责读取和保存用户的WiFi设置（如WiFi开关状态、已连接的网络等）。

### 13. `../packages/apps/Settings/src/com/android/settings/wifi/WifiEnabler.java`
#### 主要作用：
用于在设置界面中启用或禁用WiFi。监听WiFi开关的状态变化，并更新UI。

### 14. `../packages/apps/Settings/src/com/android/settings/wifi/WifiMasterSwitchPreferenceController.java`
#### 主要作用：
WiFi主开关的控制器。管理设置界面中的WiFi开关选项，处理用户的开关操作并更新UI。

### 15. `../packages/apps/Settings/src/com/android/settings/wifi/WifiSettings.java`
#### 主要作用：
WiFi设置界面的主类。提供WiFi设置界面的功能，包括显示可用网络、连接到网络、管理已保存的网络等。

### 16. `../vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerShellCommand.java`
#### 主要作用：
处理Space9d服务的Shell命令。用于调试和管理Space9d服务，提供命令行接口来执行特定的管理任务。

### 17. `../vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java`
#### 主要作用：
管理模拟服务。这个类可能用于在开发或测试环境下模拟各种服务行为，以便进行测试而不需要真实的硬件或服务。

这些文件共同组成了从底层WiFi管理到用户界面显示的完整WiFi功能链条，涵盖了状态跟踪、连接管理、UI更新和模拟测试等多个方面。























### WifiTracker

- WifiManager wifiManager
- ConnectivityManager
- WifiListener
- NetworkInfo mLastNetworkInfo;

---

下拉栏获取状态

- frameworks/base/packages/SystemUI/src/com/android/systemui/qs/tiles/WifiTile.java
- frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/policy/WifiSignalController.java

下拉栏设置状态

/linux_data/rockchip_android_src/android_10$ md5sum vendor/rockchip/common/vpu/lib/librockit/librockit.so
828a23b272c82242d23c19f7e8651e23  vendor/rockchip/common/vpu/lib/librockit/librockit.so