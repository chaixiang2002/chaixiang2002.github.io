### SIM卡是在Hal层实现的

s9修改sim信息

```java
//vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerShellCommand.java
private void runUpdateConfig(PrintWriter pw) throws RemoteException {
    mService.updateMock(addMap, delList);
}

//vendor/ntimespace/Space9dService/src/com/android/server/mock/MockManager.java
public String[] updateMock(Map<String, Object> addMap, List<String> removeKeys) {
    mMockMap.get(name).map.put(toMockKey(item), addMap.get(item));
    ...
    syncMockInfo(name, arrayMap);
    mockInfo.callback.onCallback(arrayMap);
}
```





# hardware/ntimespace/space-reference-ril



---

![image-20241223153832232](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202412231538759.png)

---

net.conn.checkInterval

```
jgrep SCAN_INTERVAL_MS |grep -v Test
```







WIFI模块

---

除了connect，其他是命令实时生效，设置里的开关也同步，

- 但是状态栏的没有实时同步
- connect
- WiFi关闭没有默认让其他WiFi参数清空



Network模块

---

```
net.wifi.enabled
net.wifi.connected
net.wifi.ssid
net.wifi.bssid
net.wifi.ipaddress
net.wifi.scanresults

net.cm.type
net.cm.subType
net.cm.typeName
net.cm.subtypeName
net.cm.extraInfo
net.bluetooth.address
net.bluetooth.name

sim.state
sim.imei
sim.imeisv
sim.meid
sim.operatorLongName
sim.operatorShortName
sim.numeric
sim.spn
sim.iccid
sim.imsi
sim.msisdn
sim.signalStrength
sim.esn
sim.lac
sim.cid

sim.sid
sim.arfcn
sim.pci
sim.netType
sim.radioType
sim.gid1
sim.alphaTag
sim.nai
sim.rilImplVersion
sim.baseband
sim.interface.mock



```



static void requestRadioPower(void *data, size_t datalen __unused, RIL_Token t)：把错误返回成功



疑点1：

```cpp
//hardware/ril/reference-ril/reference-ril.c
static bool hasWifiCapability()
{
#ifndef SIMULATION_MODE
    char propValue[PROP_VALUE_MAX];
    return property_get("ro.kernel.qemu.wifi", propValue, "") > 0 &&
           strcmp("1", propValue) == 0;
#else
    return true;
#endif
}
```

ro.kernel.qemu.wifi我们的值为0

bool hasWifi = hasWifiCapability();

想法：这里以后要改



static void requestRadioPower(void *data,直接返回成功NULL



static void requestQueryNetworkSelectionMode( ：直接返回成功



static void requestGetCurrentCalls(void *data __unused, ：直接返回成功

static void requestSignalStrength(void *data __unused, size_t datalen __unused,: 直接写强度

static void requestSetPreferredNetworkType( int request __unused, ：直接返回成功

static void requestCdmaBaseBandVersion(int request __unused,：直接返回成功 strdup("CBP8.2,21.258.08.00.030");

static void requestDeviceIdentity(int request __unused, ：直接返回成功 responseStr[0] = sim_conf.imei;sim_conf.imeisv;sim_conf.esn;sim_conf.meid;

static void requestCdmaGetSubscriptionSource(int request __unused,：直接返回成功 response = 1

static void requestCdmaSetSubscriptionSource(int request __unused,：直接返回成功和 RIL_onUnsolicitedResponse(RIL_UNSOL_CDMA_SUBSCRIPTION_SOURCE_CHANGED, ss, sizeof(ss[0]));

static void requestRegistrationState(int request, void *data __unused,：返回成功sim_conf.lac，sim_conf.cid

static void requestOperator(void *data __unused,：返回成功sim_conf.operatorLongName，sim_conf.operatorShortName，sim_conf.numeric

static void requestSimOpenChannel(void *data, size_t datalen, RIL_Token t)：返回成功 session_id = 1;

static void requestSimCloseChannel(void *data, size_t datalen, RIL_Token t)：返回成功

static void requestSetupDataCall(void *data,：返回成功 sim_conf.ifname 、sim_conf.ipaddresses、sim_conf.dnses、sim_conf.gateways、status、suggestedRetryTime、cid、active、type、pcscf、mtu

static void  requestSIM_IO(void *data,  :返回成功&sr  	sr.sw1 sr.sw2  sr.simResponse     sim_conf.iccid      msisdn

onRequest (int request, void *data, size_t datalen, RIL_Token t)  : 注释 RADIO_STATE_UNAVAILABLE

​				case RIL_REQUEST_GET_IMSI: 返回成功sim_conf.imsi

​				case RIL_REQUEST_GET_IMEI：返回成功sim_conf.imei

​				case RIL_REQUEST_PULL_LCEDATA: 返回RIL_E_RADIO_NOT_AVAILABLE

修改static RIL_RadioState

static RIL_RadioState

currentState()

{

  sState = getSIMState();

  return sState;

}

static const char * getVersion(void)           return "Space 3.140";

static void setRadioState(RIL_RadioState newState)  设置

​			  sState = RADIO_STATE_ON;

  			oldState = RADIO_STATE_UNAVAILABLE;

static SIM_Status getRUIMStatus(){ 直接返回return SIM_READY;

static SIM_Status getSIMStatus(){直接返回return currentState() == RADIO_STATE_ON ? SIM_READY : SIM_ABSENT;

static int getCardStatus(RIL_CardStatus_v6 **pp_card_status) {

​		  int sim_status = getSIMStatus();

​		 p_card_status->applications[0] = app_status_array[sim_status];

​    	 p_card_status->applications[1] = app_status_array[sim_status];

​    	 p_card_status->applications[2] = app_status_array[sim_status];



static int isRadioOn(){ 直接返回  return 1;

int query_supported_techs( ModemInfo *mdm __unused, int *supported ){直接  if (supported) *supported = ( 1 << 16 ); return 0;

int query_ctec(ModemInfo *mdm __unused, int *current, int32_t *preferred){直接 return 1;

static void setHardwareConfiguration(int num, RIL_HardwareConfig *cfg){直接return;

static void * mainLoop(void *param __unused) 主循环 if (fd < 0) { fd = 1;                 注释ret < 0的情况



![image-20250117162652857](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202501171626387.png)

[Android RIL - 李晓刚的博客 | LXG Blog](https://lixiaogang03.github.io/2019/09/12/Android-RIL/)

![image-20250121154115800](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202501211541532.png)

![image-20250121154404118](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202501211544032.png)

hardware/ril/rild/rild.c

hardware/gdpu/reference-ril/reference-ril.c

hardware/ril/reference-ril/atchannel.c

URC消息的处理流程基本上就是根据命令头的不同将其转化为不同的命令索引，然后调用RIL_onUnsolicitedResponse函数

这也符合整个RIL架构的设计理念：框架和处理方式由ril.c管理，差异化的AT命令由reference实现。

[解析Android RIL层初始化及事件机制-CSDN博客](https://blog.csdn.net/macdroid/article/details/43836255?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-5-43836255-blog-71911095.235^v43^pc_blog_bottom_relevance_base8&spm=1001.2101.3001.4242.4&utm_relevant_index=8)！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！非常详细

```
antdock:~# d-sh 3
b2467c2f1f30:/ # 
b2467c2f1f30:/ #  ps -ef |grep rild
radio          135     1 0 01:33:55 ?     00:00:00 rild
root          1201   367 0 01:34:10 pts/0 00:00:00 grep rild
b2467c2f1f30:/ # logcat |grep 135
01-22 01:34:00.316   135   135 D         : config.c getSIMState
01-22 01:34:00.652   135   135 D         : config.c getSIMState
01-22 01:34:00.736   135   135 I chatty  : uid=1001(radio) /vendor/bin/hw/rild expire 3 lines
01-22 01:34:01.135   730   730 W         : Connect socket err for path /data/system/root_sock: Connection refused
01-22 01:34:06.009   135  1002 D         : config.c getSIMState
01-22 01:34:06.009   135   142 D         : config.c getSIMState
01-22 01:34:06.009   135   142 D         : config.c getSIMState
01-22 01:34:06.010   135   135 D         : config.c getSIMState
01-22 01:34:06.011   135   135 D         : config.c getSIMState
01-22 01:34:15.282  1294  1351 D NetworkSecurityConfig: No Network Security Config specified, using platform default
01-22 01:34:15.358    78  1352 E ResolverController: No valid NAT64 prefix (100, <unspecified>/0)
01-22 01:34:17.009   135   142 D         : config.c getSIMState
01-22 01:34:17.009   135  1415 D         : config.c getSIMState
01-22 01:34:17.009   135   142 D         : config.c getSIMState
01-22 01:34:17.010   135   135 D         : config.c getSIMState
01-22 01:34:17.010   135   135 I chatty  : uid=1001(radio) /vendor/bin/hw/rild identical 1 line
01-22 01:34:17.011   135   135 D         : config.c getSIMState
01-22 01:34:28.010   135   142 D         : config.c getSIMState
01-22 01:34:28.010   135  1854 D         : config.c getSIMState
01-22 01:34:28.010   135   142 D         : config.c getSIMState
01-22 01:34:28.012   135   135 D         : config.c getSIMState
01-22 01:34:28.012   135   135 I chatty  : uid=1001(radio) /vendor/bin/hw/rild identical 1 line
01-22 01:34:28.013   135   135 D         : config.c getSIMState
01-22 01:34:35.669   992  2032 E JavaBinder: !!! FAILED BINDER TRANSACTION !!!  (parcel size = 2113536)
01-22 01:34:36.135   531   531 V KeyguardUpdateMonitor: onSubscriptionInfoChanged()
01-22 01:34:36.135   248   519 I CMK     : getNetworkCapabilities:raw=[ Transports: ETHERNET Capabilities: NOT_METERED&INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN&VALIDATED&NOT_ROAMING&FOREGROUND&NOT_CONGESTED&NOT_SUSPENDED LinkUpBandwidth>=100000Kbps LinkDnBandwidth>=100000Kbps]
01-22 01:34:36.135   248   519 I CMK     : getNetworkCapabilities:newNc=[ Transports: WIFI Capabilities: INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN&VALIDATED]
01-22 01:34:36.135   531   531 V KeyguardUpdateMonitor: SubInfo:{id=1, iccId=890124019[****] simSlotIndex=0 carrierId=1 displayName=T-Mobile carrierName=T-Mobile nameSource=0 iconTint=-16746133 mNumber=[****] dataRoaming=0 iconBitmap=android.graphics.Bitmap@9efca38 mcc 310 mnc 260mCountryIso=us isEmbedded false nativeAccessRules null cardString=890124019[****] cardId=-1 isOpportunistic false mGroupUUID=null mIsGroupDisabled=false profileClass=-1 ehplmns = null hplmns = null subscriptionType=0 mGroupOwner=null carrierConfigAccessRules=null}
01-22 01:34:37.430  2223  2223 D OpenRuntimeJNI: config:FFmpeg-arm64-v8a|2290712|245eef56f9c1186a8c0625fa0361f090|wcwss-arm64-v8a|3913544|4fcfbd76e52eef1b2793c5d28f563747|mmv8-arm64-v8a|16217760|33aeba5b752545fa9955243bf568d961|wxa-runtime-binding-arm64-v8a|583832|9a70ba73f4a702f89fbcd38b2fac4010|native-iv-arm64-v8a|84024|fdcdcf7b2afc456623e89f8c815ff4a1|andromeda-arm64-v8a|7883992|cffc9eaa8b572615925b328793e60f34|mp3lame-arm64-v8a|252056|01b87ad5990c3bdbdac9a0ad3d75d088|ilink_network-arm64-v8a|7996712|741fc050406fe204ede642da7ce59a08|mmimgcodec-arm64-v8a|104712|beabb2490cab86e1d18bc5bfa9860211|108168wxa-arm64-v8a|211040|a9d9d34a382599694b1776c1479867c2|canvas-arm64-v8a|420032|310c6eee4d5bbba39397040bef88964c|audio_common-arm64-v8a|99920|5c8443739cd1a2db1c1f8d3aaf3e2069|tencentlocsapp-arm64-v8a|24672|2a6e0c9447465dc06f3907ada01a14c5|wechataudiosilk-arm64-v8a|104048|b3b80a6fd70cac26d8630078f1b8aff9|wmpfcommonjni-arm64-v8a|1829776|fc3a0dd4d378591e326fd9c6cfc27701|mmmediasdk-arm64-v8a|2738216|899087cc24a630271acf8df8f6357996|mmskia-arm64-v8a|7116240|cec898c8e
01-22 01:34:37.430  2223  2223 D OpenRuntimeJNI: index:3 wcwss-arm64-v8a 3913544 4fcfbd76e52eef1b2793c5d28f563747
01-22 01:34:37.431  2223  2223 D OpenRuntimeJNI: index:135 QmNativeDataSource-arm64-v8a 63056 b5877428302d63f2be1b3a212ec3fe50
01-22 01:34:37.431  2223  2223 D OpenRuntimeJNI: index:309 mmavmedia-armeabi-v7a 10671400 31357d32d5f0930790c3a7830681ad95
01-22 01:34:39.011   135   142 D         : config.c getSIMState
01-22 01:34:39.011   135  2324 D         : config.c getSIMState
01-22 01:34:39.011   135   142 D         : config.c getSIMState
01-22 01:34:39.012   135   135 D         : config.c getSIMState
01-22 01:34:39.013   135   135 I chatty  : uid=1001(radio) /vendor/bin/hw/rild identical 1 line
01-22 01:34:39.014   135   135 D         : config.c getSIMState
01-22 01:34:45.674   992  1387 W PeoplePU:      at com.android.server.pm.PackageManagerService.onTransact(PackageManagerService.java:4135)
01-22 01:34:50.013   135   142 D         : config.c getSIMState
01-22 01:34:50.013   135  2499 D         : config.c getSIMState
01-22 01:34:50.013   135   142 D         : config.c getSIMState
01-22 01:34:50.015   135   135 D         : config.c getSIMState
01-22 01:34:50.016   135   135 I chatty  : uid=1001(radio) /vendor/bin/hw/rild identical 1 line
01-22 01:34:50.016   135   135 D         : config.c getSIMState
^C
130|b2467c2f1f30:/ # 
```



```markdown
上面提到的参数是和SIM卡在安卓系统中工作时相关的各种信息。每个参数代表了不同的SIM卡属性和配置，它们有助于网络连接、网络选择以及对不同网络环境的适配。以下是对这些参数的详细讲解：

### 1. `sim.sid`（CDMA网络类型下的SID）
https://blog.51cto.com/u_12553406/6078741
- **含义**：SID（System Identification Number）是CDMA网络中的一个系统标识符，通常用来标识一个特定的CDMA网络。它是一个10进制数字，代表了一个运营商的网络。
- **用途**：它通常用于定位服务和网络识别，尤其在CDMA网络中，SIM卡会通过SID来识别连接到哪个CDMA系统。

### 2. `sim.arfcn`（2/4/5G模式下的绝对无线频率信道编号）
https://blog.csdn.net/android_cai_niao/article/details/144551958
- **含义**：ARFCN（Absolute Radio Frequency Channel Number）是用于表示无线频率信道的编号。每个无线频率信道都有一个唯一的编号，表示该信道在无线网络中的位置。
- **用途**：在2G（GSM）、4G（LTE）和5G网络中，ARFCN用于标识不同的频率信道，有助于设备选择合适的频率来与基站通信。

### 3. `sim.pci`（4/5G模式下的物理小区ID）
https://blog.csdn.net/fafactx/article/details/21930015
- **含义**：PCI（Physical Cell Identity）是LTE和5G网络中用来标识物理小区的唯一标识符。它表示基站所在的物理位置或覆盖范围。
- **用途**：通过PCI，手机能够识别不同基站，选择合适的基站进行连接，以确保网络连接的稳定性和质量。

### 4. `sim.netType`（数据网络类型）
- **含义**：该字段表示设备当前所连接的网络类型。可以是：
  - `gsm`（2G网络）
  - `cdma`（3G网络）
  - `lte`（4G网络）
  - `nr`（5G网络）
- **用途**：该字段通常用于描述设备支持的数据网络类型，决定了设备能够使用哪种类型的网络服务。

### 5. `sim.radioType`（语音网络类型）
- **含义**：该字段描述设备用于语音服务的网络类型。与`sim.netType`类似，但它专门针对语音通信的网络类型，可能的值包括：
  - `gsm`（2G）
  - `cdma`（3G）
  - `lte`（4G）
  - `nr`（5G）
- **用途**：有些网络类型仅支持数据传输（如4G/5G），而一些旧的网络（如2G/3G）同时支持语音和数据。这些信息帮助手机区分使用何种网络进行语音通话。

### 6. `sim.gid1`（GroupLevel1）
- **含义**：GID1代表SIM卡中存储的“组标识符”信息，是用来区分不同的运营商、服务提供商或虚拟运营商。
- **用途**：这个字段在某些网络中用来决定SIM卡所属的服务组或者运营商网络，用于更细致的网络管理。

### 7. `sim.alphaTag`（Line1AlphaTag）
- **含义**：此字段代表SIM卡上的标识信息（如网络名称、运营商名称）。它会显示在设备的UI界面上，帮助用户辨识网络。
- **用途**：通常，`sim.alphaTag`显示为运营商名称或网络标识。如果是CDMA类型的SIM卡，不支持该字段。

### 8. `sim.nai`（CDMA网络类型下的NAI）
- **含义**：NAI（Network Access Identifier）是CDMA网络中用于网络接入的标识符，类似于GSM中的IMSI（国际移动用户识别码）。
- **用途**：它通常用于身份验证、网络授权等任务，帮助运营商确认设备的合法性。

### 9. `sim.rilImplVersion`（RIL实现版本名称）
static const char * getVersion(void)
- **含义**：RIL（Radio Interface Layer）是安卓系统和基带（移动网络硬件）之间的接口层。`rilImplVersion`表示当前设备所使用的RIL实现版本。
- **用途**：该信息用于诊断网络问题，并确认设备所用的无线协议栈版本。可以通过`getprop`命令查询对应的`gsm.version.ril-impl`属性。

### 10. `sim.baseband`（基带版本）
- **含义**：基带（Baseband）是指设备中负责无线通信的硬件和固件部分。`sim.baseband`显示当前设备所使用的基带版本号。
- **用途**：通过基带版本，可以检查设备是否使用了最新的无线通信协议或是否存在已知的网络连接问题。

### 11. `sim.interface.mock`（移动网卡仿真）
- **含义**：该字段表示设备是否支持移动网卡仿真，通常用于测试环境中。
- **用途**：如果开启该选项，设备可以模拟移动网络的接口，如`rmnet_data0`，通常用于开发和调试阶段的网络测试。

### 总结
这些SIM卡相关的参数涉及到设备如何识别和与不同类型的网络进行交互，包括CDMA、GSM、LTE、NR等多种网络标准。它们对设备的网络连接、语音通信、数据传输等方面至关重要。通过这些信息，安卓系统能够根据不同网络的特性调整相关的行为，例如选择合适的网络、显示正确的网络名称或执行特定的网络操作。
```





### 所有请求

```markdown
以下是AOSP 10中的 `hardware/ril/reference-ril/reference-ril.c` 文件中列出的 `RIL_REQUEST_*` 请求项及其含义：

### 1. **与呼叫相关的请求：**
- **RIL_REQUEST_HANGUP_WAITING_OR_BACKGROUND**：挂断等待或后台的通话。
- **RIL_REQUEST_HANGUP_FOREGROUND_RESUME_BACKGROUND**：挂断前台通话并恢复后台通话。
- **RIL_REQUEST_SWITCH_WAITING_OR_HOLDING_AND_ACTIVE**：切换等待或保持的通话与活动通话。
- **RIL_REQUEST_CONFERENCE**：发起电话会议。
- **RIL_REQUEST_UDUB**：挂断当前的电话并结束通话。

### 2. **基带和订阅相关的请求：**
- **RIL_REQUEST_BASEBAND_VERSION**：请求基带版本信息。                  sim.baseband
- **RIL_REQUEST_CDMA_GET_SUBSCRIPTION_SOURCE**：获取CDMA订阅来源。
- **RIL_REQUEST_CDMA_QUERY_PREFERRED_VOICE_PRIVACY_MODE**：查询CDMA的首选语音隐私模式。
- **RIL_REQUEST_CDMA_SET_PREFERRED_VOICE_PRIVACY_MODE**：设置CDMA的首选语音隐私模式。
- **RIL_REQUEST_CDMA_SET_ROAMING_PREFERENCE**：设置CDMA漫游偏好。
- **RIL_REQUEST_CDMA_SET_SUBSCRIPTION_SOURCE**：设置CDMA订阅来源。
- **RIL_REQUEST_CDMA_SUBSCRIPTION**：查询CDMA订阅信息。
- **RIL_REQUEST_DEVICE_IDENTITY**：获取设备的身份信息（IMEI等）。
- **RIL_REQUEST_EXIT_EMERGENCY_CALLBACK_MODE**：退出紧急回拨模式。

### 3. **SIM卡和网络相关的请求：**
- **RIL_REQUEST_GET_ACTIVITY_INFO**：获取当前活动的信息。
- **RIL_REQUEST_GET_CARRIER_RESTRICTIONS**：查询运营商的限制信息。
- **RIL_REQUEST_GET_CURRENT_CALLS**：获取当前的通话状态信息。
- **RIL_REQUEST_GET_IMEI**：获取设备的IMEI号。
- **RIL_REQUEST_GET_MUTE**：获取静音状态。
- **RIL_REQUEST_GET_NEIGHBORING_CELL_IDS**：查询邻近基站的ID。?????????????SID?
- **RIL_REQUEST_GET_PREFERRED_NETWORK_TYPE**：获取首选网络类型。????????
- **RIL_REQUEST_GET_RADIO_CAPABILITY**：获取设备的无线电能力信息。
- **RIL_REQUEST_GET_SIM_STATUS**：获取SIM卡状态。
- **RIL_REQUEST_NV_RESET_CONFIG**：重置基带配置。
- **RIL_REQUEST_QUERY_AVAILABLE_BAND_MODE**：查询支持的频段模式。
- **RIL_REQUEST_QUERY_NETWORK_SELECTION_MODE**：查询网络选择模式。
- **RIL_REQUEST_QUERY_TTY_MODE**：查询TTY（电传打字机）模式。
- **RIL_REQUEST_RADIO_POWER**：开关无线电电源。
- **RIL_REQUEST_SET_BAND_MODE**：设置设备支持的频段模式。
- **RIL_REQUEST_SET_CARRIER_RESTRICTIONS**：设置运营商限制。
- **RIL_REQUEST_SET_LOCATION_UPDATES**：设置位置更新。
- **RIL_REQUEST_SET_PREFERRED_NETWORK_TYPE**：设置首选网络类型。
- **RIL_REQUEST_SET_TTY_MODE**：设置TTY模式。
- **RIL_REQUEST_SET_UNSOL_CELL_INFO_LIST_RATE**：设置未经请求的蜂窝信息列表更新频率。
- **RIL_REQUEST_STOP_LCE**：停止LCE（连接探测）功能。
- **RIL_REQUEST_VOICE_RADIO_TECH**：获取语音网络的无线电技术类型（例如：GSM、CDMA、LTE等）。

### 4. **与通话管理相关的请求：**
- **RIL_REQUEST_GET_SIM_STATUS**：获取SIM卡状态。
- **RIL_REQUEST_GET_CURRENT_CALLS**：获取当前的通话列表。
- **RIL_REQUEST_DIAL**：拨打电话。
- **RIL_REQUEST_HANGUP**：挂断电话。
- **RIL_REQUEST_HANGUP_WAITING_OR_BACKGROUND**：挂断等待或后台的电话。
- **RIL_REQUEST_HANGUP_FOREGROUND_RESUME_BACKGROUND**：挂断前台电话，恢复后台电话。
- **RIL_REQUEST_SWITCH_WAITING_OR_HOLDING_AND_ACTIVE**：切换正在等待或保持的电话与当前活动的电话。
- **RIL_REQUEST_CONFERENCE**：发起电话会议。
- **RIL_REQUEST_UDUB**：拒绝当前通话并结束。

### 5. **短信和USSD相关的请求：**
- **RIL_REQUEST_SEND_SMS**：发送SMS短信。
- **RIL_REQUEST_SEND_SMS_EXPECT_MORE**：发送SMS短信，期望更多响应。
- **RIL_REQUEST_CDMA_SEND_SMS**：发送CDMA SMS。
- **RIL_REQUEST_IMS_SEND_SMS**：通过IMS发送短信。
- **RIL_REQUEST_SIM_OPEN_CHANNEL**：打开SIM卡通道。
- **RIL_REQUEST_SIM_CLOSE_CHANNEL**：关闭SIM卡通道。
- **RIL_REQUEST_SIM_TRANSMIT_APDU_CHANNEL**：通过SIM卡通道传输APDU命令。
- **RIL_REQUEST_SETUP_DATA_CALL**：建立数据连接。
- **RIL_REQUEST_DEACTIVATE_DATA_CALL**：断开数据连接。
- **RIL_REQUEST_SMS_ACKNOWLEDGE**：确认接收到的短信。
- **RIL_REQUEST_GET_IMSI**：获取IMSI（国际移动用户识别码）。
- **RIL_REQUEST_GET_IMEI**：获取IMEI（国际移动设备身份码）。
- **RIL_REQUEST_SIM_IO**：进行SIM卡I/O操作。
- **RIL_REQUEST_SEND_USSD**：发送USSD（未结构化补充服务数据）请求。
- **RIL_REQUEST_CANCEL_USSD**：取消USSD请求。

### 6. **网络选择和自动连接相关的请求：**
- **RIL_REQUEST_SET_NETWORK_SELECTION_AUTOMATIC**：设置网络选择为自动模式。
- **RIL_REQUEST_DATA_CALL_LIST**：查询数据呼叫列表。
- **RIL_REQUEST_QUERY_NETWORK_SELECTION_MODE**：查询当前网络选择模式。?????????NETWORK
- **RIL_REQUEST_OEM_HOOK_RAW**：OEM钩子（原始数据）请求。
- **RIL_REQUEST_OEM_HOOK_STRINGS**：OEM钩子（字符串数据）请求。

### 7. **SIM卡PIN管理请求：**
- **RIL_REQUEST_WRITE_SMS_TO_SIM**：写短信到SIM卡。
- **RIL_REQUEST_DELETE_SMS_ON_SIM**：删除SIM卡上的短信。
- **RIL_REQUEST_ENTER_SIM_PIN**：输入SIM卡PIN码。
- **RIL_REQUEST_ENTER_SIM_PUK**：输入SIM卡PUK码（PIN解锁码）。
- **RIL_REQUEST_ENTER_SIM_PIN2**：输入SIM卡第二个PIN码。
- **RIL_REQUEST_ENTER_SIM_PUK2**：输入SIM卡第二个PUK码。
- **RIL_REQUEST_CHANGE_SIM_PIN**：更改SIM卡PIN码。
- **RIL_REQUEST_CHANGE_SIM_PIN2**：更改SIM卡第二个PIN码。

### 8. **IMS和网络设置相关请求：**
- **RIL_REQUEST_IMS_REGISTRATION_STATE**：查询IMS（IP多媒体子系统）注册状态。
- **RIL_REQUEST_VOICE_RADIO_TECH**：获取语音无线电技术类型（例如，GSM、CDMA、LTE等）。
- **RIL_REQUEST_SET_PREFERRED_NETWORK_TYPE**：设置首选网络类型。
- **RIL_REQUEST_GET_PREFERRED_NETWORK_TYPE**：获取首选网络类型。
- **RIL_REQUEST_GET_CELL_INFO_LIST**：获取当前蜂窝信息列表。
- **RIL_REQUEST_SET_UNSOL_CELL_INFO_LIST_RATE**：设置蜂窝信息列表更新频率。
- **RIL_REQUEST_GET_HARDWARE_CONFIG**：获取硬件配置信息。
- **RIL_REQUEST_SHUTDOWN**：关闭设备。
- **RIL_REQUEST_QUERY_TTY_MODE**：查询TTY模式。
- **RIL_REQUEST_GET_RADIO_CAPABILITY**：获取无线电能力。
- **RIL_REQUEST_GET_MUTE**：查询静音状态。
- **RIL_REQUEST_SET_INITIAL_ATTACH_APN**：设置初始附加的APN。
- **RIL_REQUEST_ALLOW_DATA**：允许数据连接。
- **RIL_REQUEST_ENTER_NETWORK_DEPERSONALIZATION**：输入网络解锁码（如SIM卡锁定解除）。

### 9. **CDMA网络请求：**
- **RIL_REQUEST_CDMA_SET_PREFERRED_VOICE_PRIVACY_MODE**：设置CDMA的首选语音隐私模式。
- **RIL_REQUEST_BASEBAND_VERSION**：查询基带版本。
- **RIL_REQUEST_DEVICE_IDENTITY**：获取设备的身份信息（如IMEI）。
- **RIL_REQUEST_CDMA_SUBSCRIPTION**：查询CDMA订阅信息。
- **RIL_REQUEST_CDMA_GET_SUBSCRIPTION_SOURCE**：查询CDMA订阅来源。
- **RIL_REQUEST_CDMA_SET_ROAMING_PREFERENCE**：设置CDMA漫游偏好。
- **RIL_REQUEST_CDMA_SET_SUBSCRIPTION_SOURCE**：设置CDMA订阅来源。
- **RIL_REQUEST_START_LCE**：启动LCE（连接探测）。
- **RIL_REQUEST_STOP_LCE**：停止LCE。
- **RIL_REQUEST_PULL_LCEDATA**：拉取LCE数据。

这些

请求对应着Android硬件抽象层（HAL）中与无线电接口层（RIL）交互的各种操作，涵盖了从通话管理、数据连接到SIM卡管理等各类功能。
```





### 未验证

在 AOSP 中的 RIL（Radio Interface Layer）中，涉及到 SIM 卡信息、网络信息和设备标识符的多个请求与这些值相关。以下是每个字段可能涉及的 RIL 请求：

### 1. **`sim.sid`（CDMA网络类型下的SID）**

- 相关请求

  ：

  - `RIL_REQUEST_CDMA_SUBSCRIPTION`：该请求用于获取 CDMA 网络的订阅信息，可能包括 SID。static void requestCdmaSubscription( **VVVV**
  - `RIL_REQUEST_CDMA_GET_SUBSCRIPTION_SOURCE`：获取 CDMA 网络订阅源，可能涉及 SID。static void requestCdmaGetSubscriptionSource(

### 2. **`sim.arfcn`（2/4/5G模式下的绝对无线频率信道编号）**

- 相关请求

  ：

  - `RIL_REQUEST_GET_CELL_INFO_LIST`：获取当前小区信息（包括 ARFCN 等频率信息）。static void requestGetCellInfoList(**VVVVVVVVVVV**
  - `RIL_REQUEST_OPERATOR`：返回运营商相关信息，可能包括 ARFCN 在 LTE/NR 网络模式下的相关数据。static void requestOperator(

### 3. **`sim.pci`（4/5G模式下的物理小区ID）**

- 相关请求./libril/ril_service.cpp

  ：

  - `RIL_REQUEST_GET_CELL_INFO_LIST`：此请求获取包括 PCI 在内的小区信息。static void requestGetCellInfoList(
  - `RIL_REQUEST_VOICE_REGISTRATION_STATE` 或 `RIL_REQUEST_DATA_REGISTRATION_STATE`：这两个请求返回的注册状态信息中，可能会包括 PCI（物理小区标识符）。static void requestRegistrationState(       

### 4. **`sim.netType`（数据网络类型）**

- 相关请求

  ：

  - `RIL_REQUEST_OPERATOR`：返回当前操作的网络类型（GSM、CDMA、LTE、NR）。static void requestOperator(
  - `RIL_REQUEST_VOICE_REGISTRATION_STATE`：此请求返回的注册状态中包含网络类型信息。static void requestRegistrationState(
  - `RIL_REQUEST_DATA_REGISTRATION_STATE`：此请求也会返回网络类型信息，描述数据网络类型。

### 5. **`sim.radioType`（语音网络类型）**

- 相关请求

  ：

  - `RIL_REQUEST_VOICE_REGISTRATION_STATE`：返回语音网络类型。static void requestRegistrationState(
  - `RIL_REQUEST_VOICE_RADIO_TECH`：获取设备当前用于语音的无线电技术类型。case RIL_REQUEST_VOICE_RADIO_TECH: static int techFromModemType(int mdmtype) **VVVVVVVVVVV**

### 6. **`sim.gid1`（GroupLevel1）**

- 相关请求

  ：

  - `RIL_REQUEST_GET_SIM_STATUS`：该请求用于获取 SIM 卡的状态，可能包括 `gid1` 信息。
  - `RIL_REQUEST_CDMA_SUBSCRIPTION`：针对 CDMA 网络的订阅信息，可能包括 `gid1`。static void requestCdmaSubscription(？？？

### 7. **`sim.alphaTag`（Line1AlphaTag）**

- 相关请求

  ：

  - `RIL_REQUEST_OPERATOR`：该请求可以返回运营商名称或标识，这与 `alphaTag` 信息相关。static void requestOperator(
  - `RIL_REQUEST_GET_SIM_STATUS`：在返回的 SIM 卡状态中，可能会包括 `alphaTag`。

### 8. **`sim.nai`（CDMA网络类型下的NAI）**

- 相关请求

  ：

  - `RIL_REQUEST_CDMA_SUBSCRIPTION`：该请求可能返回 CDMA 网络的 NAI（网络接入标识符）。static void requestCdmaSubscription(
  - `RIL_REQUEST_CDMA_GET_SUBSCRIPTION_SOURCE`：获取 CDMA 网络订阅源，可能包括 NAI。static void requestCdmaGetSubscriptionSource(

### 9. **`sim.rilImplVersion`（RIL实现版本名称）**

- 相关请求

  ：

  - `RIL_REQUEST_BASEBAND_VERSION`：此请求会返回基带版本信息，通常与 `rilImplVersion` 一同获取。static const char * getVersion(void)**VVVVVV**
  - `RIL_REQUEST_GET_RADIO_CAPABILITY`：获取当前设备的无线电能力，可能包括 `rilImplVersion` 的信息。

### 10. **`sim.baseband`（基带版本）**

- 相关请求

  ：

  - `RIL_REQUEST_BASEBAND_VERSION`：此请求直接返回设备的基带版本信息。static void requestCdmaBaseBandVersion(**VVVVVVVVVVVVVV**
  - `RIL_REQUEST_GET_RADIO_CAPABILITY`：有时也包含基带相关的细节。

### 11. **`sim.interface.mock`（移动网卡仿真）**

- 相关请求

  ：

  - 该字段通常与开发、测试或调试阶段的仿真功能相关。与之直接相关的 RIL 请求并不多，但可以用于开发过程中对网络接口的模拟。
  - 如果启用了网络仿真功能，可以在 `RIL_REQUEST_*` 请求中进行模拟或检查网络接口的状态。

### 总结：

大部分与 SIM 卡、网络信息、和设备标识符相关的字段，都是通过以下几个 RIL 请求来获取的：

- `RIL_REQUEST_OPERATOR`
- `RIL_REQUEST_VOICE_REGISTRATION_STATE`
- `RIL_REQUEST_DATA_REGISTRATION_STATE`
- `RIL_REQUEST_GET_SIM_STATUS`
- `RIL_REQUEST_CDMA_SUBSCRIPTION`
- `RIL_REQUEST_BASEBAND_VERSION`
- `RIL_REQUEST_GET_CELL_INFO_LIST`

这些请求能够提供关于设备连接状态、网络类型、SIM 卡状态、基带版本、物理小区信息等详细信息。

```yml
sim.sid = 46000          # 中国移动的SID，通常CDMA网络下使用此SID来标识其系统（对于CDMA用户），对于2G/4G/5G网络则该值不适用
sim.arfcn = 6400          # 在中国移动的2G、4G或者5G网络中，可能的ARFCN编号（在不同网络制式下会有所不同）
sim.pci = 1               # 假设当前连接到的物理小区ID（PCI）。值从0到503，基站分配物理小区ID
sim.netType = lte         # 当前数据网络类型为LTE（4G网络）
sim.radioType = lte       # 语音网络类型，假设当前为4G语音网络（VoLTE）
sim.gid1 = 1              # 假设中国移动的运营商ID（Group Identifier 1）
sim.alphaTag = 中国移动   # SIM卡的标识信息（显示在手机屏幕上的运营商名称）
sim.nai = 46000           # NAI是网络接入标识符，用于身份验证。在CDMA网络中，NAI通常与IMSI相似，标识用户
sim.rilImplVersion = RIL_v1.0.0  # 当前RIL实现版本，假设为版本1.0.0
sim.baseband = MDM_5.1    # 基带版本号，表示设备支持的通信协议版本，假设是MDM系列5.1版本
sim.interface.mock = false  # 不支持移动网卡仿真

```

