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

二、其他的模拟

| 电池battery          | mode           | String            | ac                                                                   | 充电模式``ac、usb、其他(wireless) |
| -------------------- | -------------- | ----------------- | -------------------------------------------------------------------- | ---------------------------------------- |
| max_charging_current | Int            | 500000            | 最大充电电流                                                         |                                          |
| max_charging_voltage | Int            | 5000000           | 最大充电电压                                                         |                                          |
| voltage              | Int            | 4121              | 当前电池的电压（单位通常是毫伏）                                     |                                          |
| temperature          | Int            | 250               | 电池温度                                                             |                                          |
| current              | Int            | 1000              | 电池的瞬时电流（单位通常是微安）。正值表示正在充电，负值表示正在放电 |                                          |
| cycle_count          | Int            | 1000              | 电池的充电循环次数                                                   |                                          |
| full_charge          | Int            | 1000              | 电池充满电时的电量（单位通常是微安时                                 |                                          |
| charge_counter       | Int            | 5235              | 电池累计充电的电量（单位通常是微安时）                               |                                          |
| technology           | String         | Li-poly           | 电池技术                                                             |                                          |
| 蓝牙bluetooth        | enable         | Boolean           | true                                                                 | 是否启用蓝牙                             |
| address              | String         | 02:00:00:00:00:00 | 蓝牙地址                                                             |                                          |
| name                 | String         | 当前机型          | 蓝牙名称                                                             |                                          |
| 网络连接connectivity | active_network | Int               | 0                                                                    | 当前网络ConnnectivityManager.TYPE_*      |
| 虚拟私有网络vpn      | bypass.pkgs    | String            | “”                                                                 | Vpn不加速包名，多个以,号隔开             |
| bypass.uids          | String         | “”              | Vpn不加速UID，多个以,号隔开                                          |                                          |
| 无线网络wifi         | ipaddr         | String            | 192.168.2.8                                                          | Wi-Fi当前IP地址                          |
| name                 | String         | TENDA_762A        | Wi-Fi名称                                                            |                                          |
| bssid                | String         | 02:00:00:00:00:00 | 热点地址                                                             |                                          |
| mac                  | String         | 02:00:00:00:00:00 | Wi-Fimac                                                             |                                          |
| support.5g           | Boolean        | true              | 是否支持5G                                                           |                                          |
| enable               | Boolean        | true              | 是否Wi-Fi启用                                                        |                                          |

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
