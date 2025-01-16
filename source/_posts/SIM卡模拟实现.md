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

static void  requestSIM_IO(void *data,