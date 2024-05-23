## 泰国项目这边我的尝试

2个页面（144和268）

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

144：个人认为是没有连接到app的服务器，证据如下

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

当我们有泰国ip后，就变成另一个页面

268：因为是第一次启动该软件，风控要求我们关闭wifi，用移动网络访问

### SIM相关信息的模拟

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image007.png)

主要代码在frameworks/base/telephony/java/android/telephony/TelephonyManager.java

state=0

imei=862266030218816                        getDeviceId（）

imeisv=99

esn=370483496

meid=A1000002B0BEB2

lac=2847

cid=37847

operatorLongName=CHINA MOBILE      getNetworkOperatorName(int subId)

operatorShortName=CMCC

numeric=46007                                      getNetworkOperatorForPhone(int
phoneId)

spn=China Mobile                                getSimOperatorNameForPhone(int
phoneId)

iccid=89860002191807255576               getSimSerialNumber(int subId)

msisdn=18861229088                            getLine1Number

imsi=460074008004488                          getSubscriberId(int subId)

-signalStrength=300

SIM_OPERATORh或者PLMN
=46003   getSimOperatorNameForPhone(int phoneId)

 *//* *获取**sim**卡**iccid*telephonyManager.getSimSerialNumber();

 *//* *获取电话号码*     telephonyManager.getLine1Number();

 *//* *获取手机服务商信息*telephonyManager.getNetworkOperator();

 (TelephonyManager) context.getSystemService(Context.TELEPHONY_SERVICE);

    sb.append("\nLine1Number = "

+ tm.getLine1Number());

  sb.append("\nNetworkOperator =
  " + tm.getNetworkOperator());//网络运营商编号

  sb.append("\nNetworkOperatorName =
  " + tm.getNetworkOperatorName());//网络运营商名称

  sb.append("\nSimCountryIso =
  " + tm.getSimCountryIso());

  sb.append("\nSimOperator = "
+ tm.getSimOperator());SIM运营商

  sb.append("\nSimOperatorName =
  " + tm.getSimOperatorName());

  sb.append("\nSimSerialNumber =
  " + tm.getSimSerialNumber());SIM 卡的序列号

  sb.append("\nSubscriberId(IMSI) =
  " + tm.getSubscriberId());

SIM 卡关联的国际移动用户识别码（IMSI）

经常错误

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image009.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image011.jpg)

网络类型模拟

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image012.png)

主要代码在

frameworks/base/core/java/android/net/ConnectivityManager.java

frameworks/base/core/java/android/net/NetworkInfo.java

关于

class NetworkInfo implements Parcelable {

private int mNetworkType;  TYPE_MOBILE    = 0;TYPE_WIFI        = 1;

private int mSubtype;

private String mTypeName;

private String mSubtypeName;

@NonNull

private State mState;

@NonNull

private DetailedState mDetailedState;

private String mReason;

private String mExtraInfo;

private boolean mIsFailover;

private boolean mIsAvailable;

private boolean mIsRoaming;

}

mSubtype=>

1、NETWORK_TYPE_1xRTT： 常量值：7 网络类型：1xRTT

2、NETWORK_TYPE_CDMA ： 常量值：4 网络类型： CDMA （电信2g）

3、NETWORK_TYPE_EDGE： 常量值：2 网络类型：EDGE（移动2g）

4、NETWORK_TYPE_EHRPD： 常量值：14 网络类型：eHRPD

5、NETWORK_TYPE_EVDO_0： 常量值：5 网络类型：EVDO 版本0.（电信3g）

6、NETWORK_TYPE_EVDO_A： 常量值：6 网络类型：EVDO 版本A （电信3g）

7、NETWORK_TYPE_EVDO_B： 常量值：12 网络类型：EVDO 版本B（电信3g）

8、NETWORK_TYPE_GPRS： 常量值：1 网络类型：GPRS （联通2g）

9、NETWORK_TYPE_HSDPA： 常量值：8 网络类型：HSDPA（联通3g）

10、NETWORK_TYPE_HSPA： 常量值：10 网络类型：HSPA

11、NETWORK_TYPE_HSPAP： 常量值：15 网络类型：HSPA+

12、NETWORK_TYPE_HSUPA： 常量值：9 网络类型：HSUPA

13、NETWORK_TYPE_IDEN： 常量值：11 网络类型：iDen

14、NETWORK_TYPE_LTE： 常量值：13 网络类型：LTE(3g到4g的一个过渡，称为准4g)

15、NETWORK_TYPE_UMTS： 常量值：3 网络类型：UMTS（联通3g）

16、NETWORK_TYPE_UNKNOWN：常量值：0 网络类型：未知

[NetworkInfo已过时_networkinfo过时-CSDN博客](https://blog.csdn.net/yuemitengfeng/article/details/105538802)

貌似现在改用NetworkCapabilities，呜呜呜

### Apk反编译分析

<pre><b><span lang="EN-US">package</span></b><span lang="EN-US"> com.huawei.hms.framework.network.grs.local.model;</span><span lang="EN-US"></span><b><span lang="EN-US">public</span></b><span lang="EN-US"></span><b><span lang="EN-US">class</span></b><span lang="EN-US"> CountryCodeBean</span><span lang="EN-US"><o:p></o:p></span></pre>

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image014.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image016.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image018.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image020.jpg)

<pre><b><span lang="EN-US">package</span></b><span lang="EN-US"> com.huawei.hms.framework.common;<o:p></o:p></span></pre>

<pre><b><span lang="EN-US">public</span></b><span lang="EN-US"></span><b><span lang="EN-US">class</span></b><span lang="EN-US"> NetworkUtil </span><span lang="EN-US"><o:p></o:p></span></pre>

```

```

```

```

frameworks/base/core/java/android/net/NetworkCapabilities.java

### **NetworkCapabilities**

1. **mNetworkCapabilities** ：

* 这是一个位掩码，表示网络的各种能力。例如，是否支持互联网、是否支持漫游、是否支持多播等。
* 通过设置不同的位来表示不同的网络能力。

1. **mTransportTypes** ：

* 表示网络的传输类型，例如 Wi-Fi、蜂窝数据、以太网等。
* 也是一个位掩码，可以同时表示多种传输类型。

1. **mLinkUpBandwidthKbps** 和 **mLinkDownBandwidthKbps**：
   * 分别表示网络的上行和下行带宽，以千比特每秒（kbps）为单位。
   * 这些值用于评估网络连接的速度。
2. **mNetworkSpecifier** ：

* 用于指定特定网络的标识符，例如网络的 SSID（Wi-Fi 名称）或其他自定义标识。
* 可以为空，表示没有特定的网络标识。

1. **mTransportInfo** ：

* 用于存储与网络传输相关的其他信息，例如蜂窝网络的运营商信息。
* 可以为空。

1. **mSignalStrength** ：

* 表示网络信号强度，通常用于移动网络（如蜂窝数据）。
* 未指定时，值为 **SIGNAL_STRENGTH_UNSPECIFIED**。

1. **mUids** ：

* 存储与网络相关的应用程序 UID（用户标识）。
* 可以为空。
* 

1. **mEstablishingVpnAppUid** ：

* 表示正在建立 VPN 连接的应用程序的 UID。
* 如果没有建立 VPN 连接，值为 **INVALID_UID**。

1. **mUnwantedNetworkCapabilities** ：

* 表示不希望的网络能力，例如不希望连接到漫游网络。
* 也是一个位掩码。

1. **mSSID** ：

* 表示 Wi-Fi 网络的 SSID（服务集标识符）。
* 可以为空。

[解决Android NetworkCapabilities判断当前网络类型的具体操作步骤_mob649e816138f5的技术博客_51CTO博客](https://blog.51cto.com/u_16175487/6660071)

frameworks/base/core/java/android/widget/TextView.java

frameworks/base/core/java/android/app/ContextImpl.java

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image024.jpg)

frameworks/base/services/core/java/com/android/server/connectivity/Vpn.java

frameworks/base/telephony/java/android/telephony/SignalStrength.java

getSubId()

getTelephonyProperty(int phoneId, String
property, String defaultVal)

funName: getNetworkOperatorName(int subId)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image026.jpg)

frameworks/opt/net/ethernet/java/com/android/server/ethernet/EthernetTracker.java

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image028.jpg)

privateintgetSubId()

订阅ID（Subscription
ID）是在移动通信网络中用于标识用户订阅服务的唯一标识符。在多SIM卡设备或支持多个运营商的设备上，每个SIM卡或运营商都有一个对应的订阅ID。订阅ID的作用是区分不同的用户订阅和管理与每个订阅相关的信息。

在Android系统中，订阅ID主要用于以下方面：

1. 多SIM卡管理：订阅ID用于标识不同SIM卡的订阅，使得应用程序可以根据不同的SIM卡执行相应的操作，例如拨打电话、发送短信等。通过订阅ID，应用程序可以确定使用哪个SIM卡进行通信。
2. 数据连接管理：订阅ID用于管理不同订阅的数据连接。在多SIM卡设备上，每个SIM卡都可以有自己的数据连接，订阅ID可以帮助应用程序确定使用哪个SIM卡的数据连接。
3. 电话功能管理：订阅ID用于处理电话功能，例如获取活动电话的状态、监听来电、获取当前订阅的网络信息等。通过订阅ID，应用程序可以针对不同的订阅执行电话相关的操作。
4. 短信功能管理：订阅ID用于处理短信功能，例如发送和接收短信。通过订阅ID，应用程序可以确定使用哪个SIM卡的短信功能。

总之，订阅ID在Android系统中用于标识和管理不同的用户订阅。它允许应用程序根据特定的订阅执行相关操作，例如通信、数据连接、电话功能和短信功能等。这对于多SIM卡设备或支持多个运营商的设备来说尤为重要，因为它们需要区分不同的订阅并提供相应的服务。

[识别运营商  |  Android 开源项目  |  Android Open Source Project
(google.cn)](https://source.android.google.cn/docs/core/connect/carrierid?hl=zh-cn)

方法签名为 public static String
getTelephonyProperty(int phoneId, String property, String defaultVal)，它接受三个参数：

* phoneId：表示手机的ID，用于指定要获取属性的手机。这里的手机ID是指在多SIM卡设备上标识不同手机的索引值。
* property：表示要获取的属性的名称。
* defaultVal：表示如果找不到指定属性的默认值。

org.webrtc.NetworkChangeDetector

com.vkey.android.internal.vguard.util.Utility

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image030.jpg)

### TelephonyManager

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image032.jpg)

### ConnectivityManager

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image034.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image036.jpg)

### NetworkInfo

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image038.jpg)

### NetworkCapabilities

[android设备获取wifi和蓝牙状态并进行打开或关闭操作_android系统打开蓝牙后wifi关闭-CSDN博客](https://blog.csdn.net/weixin_45265547/article/details/121772032)

frameworks/base/core/java/android/os/SystemProperties.java

### KMA

getSubId()

getTelephonyProperty(int phoneId, String property, String defaultVal)

getNetworkOperatorName(int subId)

getTypeName() :MOBILE

getActiveNetworkInfo()

getSubtype()

getNetworkOperatorForPhone(int phoneId)

getSimStateIncludingLoaded()

hasTransport(@Transport int transportType):4

10. getNetworkCountryIsoForPhone(int phoneId)

frameworks/base/telephony/java/android/telephony/SubscriptionManager.java

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image040.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image042.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image044.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image046.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image048.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image050.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image052.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image054.jpg)

private int getSimStateIncludingLoaded() {

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image056.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image058.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image060.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image061.png)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image063.jpg)

frameworks/base/services/core/java/com/android/server/connectivity/Vpn.java

### KPLUS

getDefaultSubscriptionId()

getSubId()

getTelephonyProperty(int
phoneId, String property, String defaultVal)

    gsm.operator.alpha

getNetworkOperatorName

getActiveNetworkInfo

getTypeName()

getSimOperatorNumeric()

getDefaultSubscriptionId()

getTelephonyProperty(int
phoneId, String property, String defaultVal)

10. getNetworkInfo(int networkType)222--------1

gsm.sim.operator.numeric

11. getSimOperatorNumericForPhone(int phoneId)
12. **NetworkCapabilities** ()
13. NetworkCapabilities(NetworkCapabilities nc)
14. getTelephonyProperty(int phoneId, String property, String
    defaultVal)

    gsm.sim.operator.numeric

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image065.jpg)

## 其他APP

### TMB

没有vpn闪退，有vpn要求4G网络

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image067.jpg)

getActiveNetworkInfo()

getDefaultSubscriptionId()

getNetworkOperatorName(int subId)

getNetworkCountryIsoForPhone(int phoneId)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image069.jpg)

### Scb

无论vpn与否，要求更新app

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image071.jpg) ![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image073.jpg)

### BBL

要谷歌商城，有谷歌play进入登陆页面，没有就报错

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image075.jpg)

但是装了谷歌play，很多app就闪退

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image076.png)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image078.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image080.jpg)

乱改网络的下场

漫游不能乱改

mIsRoaming = false;

会导致networkManageService

### 安卓id的获取

1|OP4EB7:/ $ settings get secure android_id

1054bffc0a1d1e99

## 当前进度

### 综合问题

找不到部分软件

Kplus（它安装）

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image082.jpg)

### Scb

目前卡在这

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image084.jpg)

过程分析

NetworkCapabilities.
hasTransport(@Transport int transportType):

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image085.png)

检测vpn，检测移动网络

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image087.jpg)

获取了网络信息

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image089.jpg)

？？

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image091.jpg)

？？？

点击不设置屏保后

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image093.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image094.png)

点击同意电话

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image096.jpg)

整体代码如下

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image098.png)

结束

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image100.jpg)

感觉还是原因还是这里

结果

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image101.png)

### Next（它安装）

目前结果

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image103.jpg)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image105.jpg)

android.security.keystore.IkeystoreKeyCharacteristicsCallback调用

1. **com.facebook.UserSettingsManager** 警告：
   * 提示用户设置 **AutoLogAppEventsEnabled** 和 **AdvertiserIDCollectionEnabled**。
   * 如果你想自动收集应用安装、启动和应用内购买事件，请将 **AutoLogAppEventsEnabled** 设置为 **TRUE**。
   * 如果你想在收集数据之前请求用户同意，请将 **AutoLogAppEventsEnabled** 设置为 **FALSE**，然后在获得用户同意后更改为 **TRUE**。
   * 相关文档：了解更多
2. **ktbcs.netbank** 错误：
   * 这个 dex 文件无效，将来会被拒绝。
   * 错误信息：接口字段不是公共的 final static，Lpc;.pc$ar$NoOp:
     1009(public static)
3. **NetworkSecurityConfig** 信息：
   * 使用了来自资源 network_security_config 的网络安全配置。
   * debugBuild 为 false。

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image107.jpg)

1. **DynamiteModule** 警告：
   * **IDynamite loader version** ：指示使用的 **Dynamite** 加载器版本为 2，但没有高精度的延迟测量。
   * **Considering local module** ：正在考虑本地模块 com.google.android.gms.measurement.dynamite:55 和远程模块 com.google.android.gms.measurement.dynamite:11。
   * **Selected local version** ：选择了本地版本的 com.google.android.gms.measurement.dynamite。

感觉无关

获取网络信息

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image109.jpg)

 **errorMessage** :
不支持的 GET 请求。ID 为 ‘2318048171545458’ 的对象不存在，无法加载，或不支持此操作。

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image111.jpg)

获取网络运营商名称，获取了几次

判断是否vpn

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image113.jpg)

警告表示某个事件缺少名为 “event_action” 的参数

Obtained fresh AdvertisingId info from
GmsCore.

这是一条信息，表示从 GmsCore 获取了最新的广告标识（Advertising ID）信息。

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image115.jpg)

还是com.google.android.gms.common.internal.IGmsCallbacks,这个包，个人感觉是这里的原因

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image117.jpg)

和K-plus一样，V-OS 在本地 iOS 或 Android 移动应用程序中嵌入了一个安全的沙盒环境，

 **java.lang.ClassNotFoundException:
android.support.v4.content.ContextCompat** ：这是一个类未找到的错误

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image119.jpg)

警告提醒开发者在使用 BottomSheetBehavior 时，应该使用 addBottomSheetCallback() 和
removeBottomSheetCallback() 来设置自定义的回调，而不是使用
setBottomSheetCallback()。这样可以避免不必要的问题和行为。与问题无关

按下确定，弹出要关闭页面

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image120.png)

![](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image122.jpg)

判断是否wifi

又是这个google的包

·
 **JavaBinder: onTransact: code=2,
descriptor=com.google.android.play.core.integrity.protocol.IExpressIntegrityServiceCallback,
caller PID=0, UID=10094** ：这是一个 Binder 事务的记录，涉及到 **Integrity** 服务的回调。

·
 **PlayCore: UID: [10099] PID: [7684]
OnWarmUpIntegrityTokenCallback : onWarmUpExpressIntegrityToken** ：这是一个 **Integrity** 回调的信息。

·
 **PlayCore: UID: [10099] PID: [7684]
StandardIntegrity : Unbind from service.** ：这是一个 **Integrity** 服务解绑的信息。

### Ttb

BBL（它安装）
