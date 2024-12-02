**frameworks/base/core/java/android/net/VpnService.java**

public ParcelFileDescriptor establish()

- return getService().establishVpn(mConfig);

**frameworks/base/core/java/android/net/IConnectivityManager.aidl**

`IConnectivityManager` 是一个 AIDL 接口生成的类

**frameworks/base/services/core/java/com/android/server/ConnectivityService.java**

public ParcelFileDescriptor establishVpn(VpnConfig config)

- return mVpns.get(user).establish(config);

**frameworks/base/services/core/java/com/android/server/connectivity/Vpn.java**

public synchronized ParcelFileDescriptor establish(VpnConfig config

- config.dnsServers = mMock.regroupDnsServer(config.dnsServers);

**frameworks/base/core/java/com/android/internal/space/api/VpnMock.java**

public List<String> regroupDnsServer(List<String> legacyDns) {

- for (String dns : legacyDns) { ：报错空指针

