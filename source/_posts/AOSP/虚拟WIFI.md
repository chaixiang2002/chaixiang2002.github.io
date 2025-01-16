[Redroid 11 启用虚拟wifi - Dev-Tan](https://www.202016.xyz/2023/08/17/redroid-11-enable-virtwifi.html)

[vendor_redroid_ext/wifi at master · redroid-rockchip/vendor_redroid_ext](https://github.com/redroid-rockchip/vendor_redroid_ext/tree/master/wifi)







----

packages/apps/Settings/res/values/strings.xml

  <!-- Wi-Fi state - Disconnected [CHAR LIMIT=NONE] -->

  <string name="disconnected">Not connected</string>

packages/apps/Settings/src/com/android/settings/wifi/WifiSummaryUpdater.java

```java
if (!mWifiTracker.enabled) {
    return mContext.getString(R.string.switch_off_text);
}
if (!mWifiTracker.connected) {
    return mContext.getString(R.string.disconnected);
}
```

packages/apps/Settings/res/values-zh-rCN/arrays.xml

```xml
  <string-array name="wifi_status">
    <item msgid="1201478116293383426"></item>
    <item msgid="7388036070768806193">"正在扫描..."</item>
    <item msgid="1656176059757237036">"正在连接..."</item>
    <item msgid="3249903732481917388">"正在验证身份…"</item>
    <item msgid="7789156794775399931">"正在获取IP地址..."</item>
    <item msgid="492518447401534767">"已连接"</item>
    <item msgid="4322989558568666518">"已暂停"</item>
    <item msgid="286164147080824297">"正在断开连接..."</item>
    <item msgid="1628460745311787730">"已断开连接"</item>
    <item msgid="4013828218541488949">"失败"</item>
    <item msgid="5473541238056528086">"已停用"</item>
    <item msgid="1114588261171522603">"暂时关闭（网络状况不佳）"</item>
  </string-array>
  <string-array name="wifi_status_with_ssid">
    <item msgid="1528087426723432177"></item>
    <item msgid="155483314608049961">"正在扫描..."</item>
    <item msgid="3409219643606946053">"正在连接到 <xliff:g id="NETWORK_NAME">%1$s</xliff:g>..."</item>
    <item msgid="7891463004457278422">"正在通过 <xliff:g id="NETWORK_NAME">%1$s</xliff:g> 进行身份验证..."</item>
    <item msgid="3193388999810487137">"正在从<xliff:g id="NETWORK_NAME">%1$s</xliff:g>获取IP地址..."</item>
    <item msgid="2227930004124157952">"已连接到 <xliff:g id="NETWORK_NAME">%1$s</xliff:g>"</item>
    <item msgid="7104168043537022445">"已暂停"</item>
    <item msgid="2595938203187002544">"正在断开与 <xliff:g id="NETWORK_NAME">%1$s</xliff:g> 的连接..."</item>
    <item msgid="2435175968703898648">"已断开连接"</item>
    <item msgid="4804573668906374228">"失败"</item>
    <item msgid="4036325515437530221">"已停用"</item>
    <item msgid="8883455894013518008">"暂时关闭（网络状况不佳）"</item>
  </string-array>
    <!-- no translation found for wifi_tether_security:0 (6312112980634811065) -->
    <!-- no translation found for wifi_tether_security:1 (1428294025896439258) -->
  <string-array name="wifi_p2p_wps_setup">
    <item msgid="1446717102923442720">"按钮"</item>
    <item msgid="2630618799033509548">"从对等设备获取的 PIN 码"</item>
    <item msgid="6088264311596031080">"此设备生成的 PIN 码"</item>
  </string-array>
  <string-array name="wifi_p2p_status">
    <item msgid="8357401480964012245">"已连接"</item>
    <item msgid="66312817817365647">"已邀请"</item>
    <item msgid="4463567967438038210">"失败"</item>
    <item msgid="6556827947082659801">"可用"</item>
    <item msgid="6096962300722555553">"超出范围"</item>
  </string-array>
```

packages/apps/Settings/src/com/android/settings/wifi/WifiInfoPreferenceController.java

```java
if (macRandomizationSupported && WifiInfo.DEFAULT_MAC_ADDRESS.equals(macAddress)) {
    mWifiMacAddressPref.setSummary(R.string.wifi_status_mac_randomized);
} else if (TextUtils.isEmpty(macAddress)
           || WifiInfo.DEFAULT_MAC_ADDRESS.equals(macAddress)) {
    mWifiMacAddressPref.setSummary(R.string.status_unavailable);
} else {
    mWifiMacAddressPref.setSummary(macAddress);
}
```

mWifiTracker.isConnected()

(info.isConnected()     NetworkInfo info = connectivity.getNetworkInfo(ConnectivityManager.TYPE_WIFI);

mSelectedAccessPoint.isConnectable()

mConnectListener = new WifiConnectListener(getActivity());

mEnableNextOnConnection = intent.getBooleanExtra(EXTRA_ENABLE_NEXT_ON_CONNECT, false);

​      switch (WifiUtils.getConnectingType(mSelectedAccessPoint)) {

​        case WifiUtils.CONNECT_TYPE_OSU_PROVISION:

​          mSelectedAccessPoint.startOsuProvisioning(mConnectListener);

​          mClickedConnect = true;

​          break;



​        case WifiUtils.CONNECT_TYPE_OPEN_NETWORK:

​          mSelectedAccessPoint.generateOpenNetworkConfig();

​          connect(mSelectedAccessPoint.getConfig(), mSelectedAccessPoint.isSaved());

​          break;





​    // Is the previous currently connected SSID different from the new one?

​    ConnectedAccessPointPreference preference =

​        (ConnectedAccessPointPreference)

​            (mConnectedAccessPointPreferenceCategory.getPreference(0));

​    // The AccessPoints need to be the same reference to ensure that updates are reflected

​    // in the UI.

​    if (preference.getAccessPoint() != connectedAp) {

​      removeConnectedAccessPointPreference();

​      addConnectedAccessPointPreference(connectedAp);

​      return true;

​    }



  protected void connect(final WifiConfiguration config, boolean isSavedNetwork) {

​    // Log subtype if configuration is a saved network.

​    mMetricsFeatureProvider.action(getContext(), SettingsEnums.ACTION_WIFI_CONNECT,

​        isSavedNetwork);

​    mWifiManager.connect(config, mConnectListener);

​    mClickedConnect = true;

  }



  protected void connect(final int networkId, boolean isSavedNetwork) {

​    // Log subtype if configuration is a saved network.

​    mMetricsFeatureProvider.action(getActivity(), SettingsEnums.ACTION_WIFI_CONNECT,

​        isSavedNetwork);

​    mWifiManager.connect(networkId, mConnectListener);

  }







------

frameworks/opt/net/wifi/service/java/com/android/server/wifi/ClientModeImpl.java



---

packages/apps/Settings/res/values-zh-rCN/arrays.xml

---

[Wi-Fi HAL  | Android Open Source Project](https://source.android.com/docs/core/connect/wifi-hal?hl=zh-cn)

- 供应商 HAL：Android 专用命令的 HAL surface。AIDL 文件位于 `hardware/interfaces/aidl` 中，HIDL 文件位于 `hardware/interfaces/wifi/1.x` 中。
- 客户端 HAL：wpa_supplicant 的 HAL Surface。AIDL 文件位于 `hardware/interfaces/supplicant/aidl` 中，HIDL 文件位于 `hardware/interfaces/supplicant/1.x` 中。
- Hostapd HAL：**hostapd** 的 HAL surface。AIDL 文件位于 `hardware/interfaces/hostapd/aidl` 中，HIDL 文件位于 `hardware/interfaces/hostapd/1.x` 中。