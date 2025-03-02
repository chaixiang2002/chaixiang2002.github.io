```verilog
01-18 06:32:13.501   403   441 W cam     : hasSystemFeature(String name, int version)---android.hardware.type.automotive
01-18 06:32:13.501   403   441 W cam     : hasSystemFeature(String name, int version)---android.software.leanback
01-18 06:32:13.502   403   420 D VpnJni  : Address added on tun0: 26.26.26.1/24
01-18 06:32:13.502   403   542 I EthernetTracker: maybeTrackInterface tun0
01-18 06:32:13.503   403   432 I EthernetTracker: interfaceLinkStateChanged, iface: tun0, up: false
01-18 06:32:13.503   403   432 I EthernetTracker: interfaceLinkStateChanged, iface: tun0, up: true
01-18 06:32:13.503   403   542 D EthernetNetworkFactory: updateCapabilityFilter: [ Transports: ETHERNET Capabilities: NOT_METERED&INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN&NOT_ROAMING&NOT_CONGESTED LinkUpBandwidth>=100000Kbps LinkDnBandwidth>=100000Kbps]
01-18 06:32:13.503   403   542 D EthernetNetworkFactory: acceptRequest, request: NetworkRequest [ REQUEST id=1, [ Capabilities: INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN] ], score: 70
01-18 06:32:13.504   403   542 I EthernetNetworkFactory: networkForRequest, request: NetworkRequest [ REQUEST id=1, [ Capabilities: INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN] ], network: NetworkInterfaceState{ iface: eth0, up: true, hwAddress: 50:ed:ab:3b:f6:ed, networkInfo: [type: Ethernet[], state: CONNECTED/CONNECTED, reason: (unspecified), extra: 50:ed:ab:3b:f6:ed, failover: false, available: true, roaming: false], networkCapabilities: [ Transports: ETHERNET Capabilities: NOT_METERED&INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN&NOT_ROAMING&NOT_CONGESTED LinkUpBandwidth>=100000Kbps LinkDnBandwidth>=100000Kbps], networkAgent: Handler (com.android.server.ethernet.EthernetNetworkFactory$NetworkInterfaceState$1) {3c2e3b1}, score: 70, ipClient: android.net.ip.IIpClient$Stub$Proxy@7b2a109,linkProperties: {InterfaceName: eth0 LinkAddresses: [ 192.168.168.53/24,fe80::6b8e:3ed3:d8bb:e333/64 ] DnsAddresses: [ /114.114.114.114,/4.2.2.1 ] Domains: null MTU: 0 TcpBufferSizes: 524288,1048576,3145728,524288,1048576,2097152 Routes: [ fe80::/64 -> :: eth0,::/0 -> fe80::b689:1ff:fe28:b834 eth0,240e:97c:0:305::c0a8:a800/120 -> :: eth0,192.168.168.0/24 -> 0.0.0.0 eth0,0.0.0.0/0 -> 192.168.168.1 eth0 ]}}
01-18 06:32:13.504   403   542 D EthernetNetworkFactory: acceptRequest, request: NetworkRequest [ REQUEST id=7, [ Capabilities: INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN] ], score: 70
01-18 06:32:13.504   403   542 I EthernetNetworkFactory: networkForRequest, request: NetworkRequest [ REQUEST id=7, [ Capabilities: INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN] ], network: NetworkInterfaceState{ iface: eth0, up: true, hwAddress: 50:ed:ab:3b:f6:ed, networkInfo: [type: Ethernet[], state: CONNECTED/CONNECTED, reason: (unspecified), extra: 50:ed:ab:3b:f6:ed, failover: false, available: true, roaming: false], networkCapabilities: [ Transports: ETHERNET Capabilities: NOT_METERED&INTERNET&NOT_RESTRICTED&TRUSTED&NOT_VPN&NOT_ROAMING&NOT_CONGESTED LinkUpBandwidth>=100000Kbps LinkDnBandwidth>=100000Kbps], networkAgent: Handler (com.android.server.ethernet.EthernetNetworkFactory$NetworkInterfaceState$1) {3c2e3b1}, score: 70, ipClient: android.net.ip.IIpClient$Stub$Proxy@7b2a109,linkProperties: {InterfaceName: eth0 LinkAddresses: [ 192.168.168.53/24,fe80::6b8e:3ed3:d8bb:e333/64 ] DnsAddresses: [ /114.114.114.114,/4.2.2.1 ] Domains: null MTU: 0 TcpBufferSizes: 524288,1048576,3145728,524288,1048576,2097152 Routes: [ fe80::/64 -> :: eth0,::/0 -> fe80::b689:1ff:fe28:b834 eth0,240e:97c:0:305::c0a8:a800/120 -> :: eth0,192.168.168.0/24 -> 0.0.0.0 eth0,0.0.0.0/0 -> 192.168.168.1 eth0 ]}}
01-18 06:32:13.528  2534  2534 D AndroidRuntime: Shutting down VM
01-18 06:32:13.528  2534  2534 E AndroidRuntime: FATAL EXCEPTION: main
01-18 06:32:13.528  2534  2534 E AndroidRuntime: Process: net.typeblog.socks:vpn, PID: 2534
01-18 06:32:13.528  2534  2534 E AndroidRuntime: java.lang.RuntimeException: Unable to start service net.typeblog.socks.SocksVpnService@899a142 with Intent { cmp=net.typeblog.socks/.SocksVpnService (has extras) }: java.lang.SecurityException: ConnectivityService: Neither user 10090 nor current process has android.permission.ACCESS_NETWORK_STATE.
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.app.ActivityThread.handleServiceArgs(ActivityThread.java:4115)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.app.ActivityThread.access$1800(ActivityThread.java:229)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1901)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.os.Handler.dispatchMessage(Handler.java:107)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.os.Looper.loop(Looper.java:214)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.app.ActivityThread.main(ActivityThread.java:7438)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at java.lang.reflect.Method.invoke(Native Method)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:930)
01-18 06:32:13.528  2534  2534 E AndroidRuntime: Caused by: java.lang.SecurityException: ConnectivityService: Neither user 10090 nor current process has android.permission.ACCESS_NETWORK_STATE.
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.os.Parcel.createException(Parcel.java:2071)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.os.Parcel.readException(Parcel.java:2039)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.os.Parcel.readException(Parcel.java:1987)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.net.IConnectivityManager$Stub$Proxy.establishVpn(IConnectivityManager.java:3028)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.net.VpnService$Builder.establish(VpnService.java:897)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at net.typeblog.socks.SocksVpnService.configure(SocksVpnService.java:210)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at net.typeblog.socks.SocksVpnService.onStartCommand(SocksVpnService.java:103)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.app.ActivityThread.handleServiceArgs(ActivityThread.java:4097)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        ... 8 more
01-18 06:32:13.528  2534  2534 E AndroidRuntime: Caused by: android.os.RemoteException: Remote stack trace:
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.app.ContextImpl.enforce(ContextImpl.java:1896)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.app.ContextImpl.enforceCallingOrSelfPermission(ContextImpl.java:1924)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at com.android.server.ConnectivityService.enforceAccessPermission(ConnectivityService.java:1955)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at com.android.server.ConnectivityService.getActiveNetwork(ConnectivityService.java:1342)
01-18 06:32:13.528  2534  2534 E AndroidRuntime:        at android.net.ConnectivityManager.getActiveNetwork(ConnectivityManager.java:978)
01-18 06:32:13.528  2534  2534 E AndroidRuntime: 
01-18 06:32:13.529  1087  1235 V Space   : s9_sock---sendTracking: app_crash ({"opType":"app_crash","resultCode":0,"package":"net.typeblog.socks","process":"net.typeblog.socks:vpn","crash_type":"crash"})
01-18 06:32:13.529  1087  1235 V Space   : s9_sock------send sock_num=0 message={"opType":"app_crash","resultCode":0,"package":"net.typeblog.socks","process":"net.typeblog.socks:vpn","crash_type":"crash"}
01-18 06:32:13.540   403  2555 I DropBoxManagerService: add tag=data_app_crash isTagEnabled=true flags=0x2
```

------

- frameworks/base/services/core/java/com/android/server/connectivity/Vpn.java    加上他的改动就有错

- frameworks/base/services/core/java/com/android/server/ConnectivityService.java

- frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiServiceImpl.java

-------

```
// frameworks/base/core/java/com/android/internal/space/api/VpnMock.java
public List<String> regroupDnsServer(List<String> legacyDns){
	...
	ConnectivityManager manager = (ConnectivityManager)
                mContext.getSystemService(Context.CONNECTIVITY_SERVICE);
	LinkProperties linkProperties = manager.getLinkProperties(manager.getActiveNetwork());
	...
}
```

问题点：ConnectivityService.getActiveNetwork();会验证android.Manifest.permission.ACCESS_NETWORK_STATE权限

有部分Vpn应用本意是不会访问这个权限的方法，但是由于我们修改了安卓10的Vpn.java，在修改的方法中，在原本不会调用ConnectivityService.getActiveNetwork()的方法调用了getActiveNetwork)，导致这部分应用运行时报权限错误，影响应用正常使用
如何既保证我功能的实现，又不影响这些应用的正常运行？