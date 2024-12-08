一、使用方法

示例1：关闭SIM卡

 s9 config -a sim.state=0

示例2：修改电话号码

 s9 config -a sim.msisdn=18023893147

查看所有模拟信息

s9 dump mock
查看某个模块的信息
s9 dump mock sim

| SIM卡             | state  | Int                  | 1                               | SIM卡状态：0关闭、1开启 |
| ----------------- | ------ | -------------------- | ------------------------------- | ----------------------- |
| imei              | String | 8.63218E+14          | 国际移动设备识别码              |                         |
| imeisv            | String | 23                   | 国际移动设备识别码软件版本      |                         |
| esn               | String | 1234                 | 电子序列号                      |                         |
| meid              | String | A00CCBB39223B        | 移动设备识别码                  |                         |
| lac               | Int    | 2847                 | 十六进制                        |                         |
| cid               | Int    | 93F2                 | 十六进制                        |                         |
| operatorLongName  | String | CHINA MOBILE         | 运营商名称                      |                         |
| operatorShortName | String | CMCC                 | 运营商短名称                    |                         |
| numeric           | String | 46000                | MCC：移动国家码 MNC：移动网络码 |                         |
| spn               | String | China Mobile         | 服务提供商名称                  |                         |
| iccid             | String | 89860002191807255576 | 集成电路卡识别码                |                         |
| msisdn            | String | 18023893147          | 手机号                          |                         |
| imsi              | String | 4.60074E+14          | 国际移动用户识别码              |                         |
| signalStrength    | Int    | 290                  | 信号强度                        |                         |
| ifname            | String | radio0               | 网络名称                        |                         |
| ipaddresses       | String | 223.107.202.11       | IP地址                          |                         |
| dnses             | String | 114.114.114.114      | dns服务                         |                         |
| gateways          | String | 10.0.3.1             | ``                  |                         |

二、目前国外镜像SIM相关模拟

|

```
echo 'state=1
imei=863218052020280
imeisv=23
esn=1234
meid=A00CCBB39223B
lac=2847
cid=93F2
operatorLongName=T-Mobile USA
operatorShortName=T-Mobile
numeric=310260
spn=T-Mobile
iccid=8901240197145277856F
msisdn=13106958678
imsi=310260123456789
signalStrength=290

ifname=radio0
ipaddresses=223.107.202.11
dnses=114.114.114.114
gateways=10.0.3.1
' > /data/misc/radio/sim.prop
 settings put system time_12_24 24
setprop persist.sys.timezone America/New_York
```

|  |
| - |

三、基于CarrierResolver的SIM信息模拟方法（技术储备）

/[frameworks](http://aospxref.com/android-10.0.0_r47/xref/frameworks/)/[opt](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/)/[telephony](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/telephony/)/[src](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/telephony/src/)/[java](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/telephony/src/java/)/[com](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/telephony/src/java/com/)/[android](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/telephony/src/java/com/android/)/[internal](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/telephony/src/java/com/android/internal/)/[telephony](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/telephony/src/java/com/android/internal/telephony/)/[CarrierResolver.java](http://aospxref.com/android-10.0.0_r47/xref/frameworks/opt/telephony/src/java/com/android/internal/telephony/CarrierResolver.java)

在 安卓系统内添加 /data/user_de/0/com.android.phone/files/carrier_test_conf.xml

|

```
<carrierTestOverrides>
    <carrierTestOverride key="numeric" value="310260"/>
    <carrierTestOverride key="mccmnc" value="310260"/>
    <carrierTestOverride key="spn" value="T-Mobile"/>
    <carrierTestOverride key="operatorShortName" value="T-Mobile"/>
    <carrierTestOverride key="operatorLongName" value="T-Mobile USA"/>
    <carrierTestOverride key="pnn" value="T-Mobile"/>
    <carrierTestOverride key="msisdn" value="+15555551234"/>
    <carrierTestOverride key="imsi" value="310260123456789"/>
    <carrierTestOverride key="iccid" value="8901260123456789012"/>
    <carrierTestOverride key="cid" value="12345"/>
    <carrierTestOverride key="lac" value="67890"/>
    <carrierTestOverride key="ipaddresses" value="192.0.2.1"/>
    <carrierTestOverride key="gateways" value="192.0.2.254"/>
    <carrierTestOverride key="gid1" value="1"/>
    <carrierTestOverride key="gid2" value="1"/>
</carrierTestOverrides>

```

|  |
| - |

### 唯一值

**这些值通常是唯一的，直接从SIM卡或网络获取：**

* **numeric** : 通常指的是MCC和MNC的组合，用于标识运营商。例如，T-Mobile USA的numeric为 `310260`。
* **imeisv** : 设备的IMEI软件版本，是IMEI的扩展。
* **msisdn** : 移动用户的电话号码。
* **imei** : 国际移动设备识别码，用于唯一标识设备。
* **imsi** : 国际移动用户识别码，用于唯一标识用户。
* **meid** : 移动设备识别码，是CDMA设备的唯一标识。
* **iccid** : 集成电路卡识别码，用于唯一标识SIM卡。
* **esn** : 电子序列号，是CDMA设备的唯一标识（较旧，已被MEID替代）。

### 运营商相关值

**这些值与特定的移动运营商相关，可能会有多个值，但对于特定的运营商组合是唯一的：**

* **mccmnc** : 移动国家代码和移动网络代码的组合，用于唯一标识运营商。例如，T-Mobile USA的MCC/MNC为 `310260`。
* **spn** : 服务提供商名称。例如，T-Mobile。
* **operatorShortName** : 运营商的短名称。例如，T-Mobile。
* **operatorLongName** : 运营商的长名称。例如，T-Mobile USA。
* **pnn** : 公众陆地移动网络名称，用于显示网络名称。

### 网络和位置相关值

**这些值与设备的网络连接和位置有关：**

* **signalStrength** : 信号强度。
* **cid** : 小区ID，标识特定的基站。
* **lac** : 位置区域码，标识特定的区域。
* **ipaddresses** : IP地址，设备连接到网络时分配的地址。
* **gateways** : 网关地址，用于数据通信。

### 其他值

**这些值与SIM卡的组标识有关：**

* **gid1** : 组标识1，运营商自定义的标识符。
* **gid2** : 组标识2，运营商自定义的标识符。

### 关联和重复

**有些值可能会有重复或相关性：**

* **numeric** 和 **mccmnc** : 两者通常是相同的，都是MCC和MNC的组合。
* **operatorShortName** 和 **spn** : 可能会相同或相似，但也可能不同。例如，短名称和服务提供商名称都可能为 `T-Mobile`。
* **operatorLongName** 和 **pnn** : 可能会相同或相似，但也可能不同。例如，长名称和公众陆地移动网络名称都可能为 `T-Mobile USA`。

**总结：**

* **唯一值：numeric（mccmnc）、imeisv、msisdn、imei、imsi、meid、iccid、esn**
* **运营商相关值：mccmnc（numeric）、spn、operatorShortName、operatorLongName、pnn**
* **网络和位置相关值：signalStrength、cid、lac、ipaddresses、gateways**
* **其他值：gid1、gid2**

**要将所有这些值模拟成美国T-Mobile的值，需要根据T-Mobile在美国的具体信息来配置。下面是针对每个值的具体说明和示例配置：**

**TelephonyManager类提供的主要的方法：**

Public Methods

int

getCallState()

返回一个常数，表示设备上的呼叫状态

CellLocation

getCellLocation()

返回设备的当前位置。

int

getDataActivity()

返回一个常数，表示活动的数据连接的类型。

int

getDataState()

返回一个常数表示当前数据连接状态

String

getDeviceId()

返回唯一的设备ID,例如,IMEI GSM和MEID CDMA手机。

String

getDeviceSoftwareVersion()

返回设备的软件版本号,例如,的IMEI / SV GSM手机。

String

getLine1Number()

返回1号线的电话号码，例如，MSISDN用于GSM电话。

List`<NeighboringCellInfo>`

getNeighboringCellInfo()

返回设备的相邻小区信息。

String

getNetworkCountryIso()

返回注册的网络运营商的国家代码

String

getNetworkOperator()

返回的MCC +跨国公司的注册网络运营商

String

getNetworkOperatorName()

返回注册的网络运营商的名字

int

getNetworkType()

返回一个常数，表示目前在设备上使用的无线电技术（网络类型）。

int

getPhoneType()

返回设备的类型（手机制式）。

String

getSimCountryIso()

 返回SIM卡运营商的国家代码

String

getSimOperator()

返回MCC +跨国公司(移动国家代码+移动网络代码)的提供者的SIM卡。

String

getSimOperatorName()

返回服务提供者的名称(SPN)。

String

getSimSerialNumber()

返回SIM卡的序列号,如果适用的话。

int

getSimState()

返回一个常数表示SIM卡设备的状态。

String

getSubscriberId()

返回唯一的用户ID,例如,IMSI为GSM手机。

String

getVoiceMailAlphaTag()

检索与语音信箱号码相关的字母标识符。

String

getVoiceMailNumber()

返回语音信箱号码。

boolean

hasIccCard()

boolean

isNetworkRoaming()

返回true，如果该设备被认为是漫游当前网络上，支持GSM目的。

void

listen(PhoneStateListener listener, int events)

注册一个侦听器对象接收改变指定的电话状态的通知。

四、NetworkInfo类型

关于

![](http://wiki.ntimespace.com/download/attachments/19010625/image2024-5-27_17-16-31.png?version=1&modificationDate=1716801392627&api=v2 "云手机项目 &gt; SIM卡信息模拟与网络 &gt; image2024-5-27_17-16-31.png")

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

五、NetworkCapabilities

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
