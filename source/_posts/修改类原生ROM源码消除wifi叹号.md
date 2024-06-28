[【教程】修改类原生ROM源码消除wifi叹号(更新安卓10.0) | 九面相柳的博客 (jmxl.github.io)](https://jmxl.github.io/2019/10/19/%E3%80%90%E6%95%99%E7%A8%8B%E3%80%91%E4%BF%AE%E6%94%B9%E7%B1%BB%E5%8E%9F%E7%94%9FROM%E6%BA%90%E7%A0%81%E6%B6%88%E9%99%A4wifi%E5%8F%B9%E5%8F%B7-%E6%9B%B4%E6%96%B0%E5%AE%89%E5%8D%9310-0/)

```
packages/modules/NetworkStack/res/config.xml
```

```
<!-- HTTP URL for network validation, to use for detecting captive portals. -->
<string name="default_captive_portal_http_url" translatable="false">http://connect.rom.miui.com/generate_204</string>

<!-- HTTPS URL for network validation, to use for confirming internet connectivity. -->
<string name="default_captive_portal_https_url" translatable="false">https://connect.rom.miui.com/generate_204</string>

<!-- List of fallback URLs to use for detecting captive portals. -->
<string-array name="default_captive_portal_fallback_urls" translatable="false">
    <item>http://connect.rom.miui.com/generate_204</item>
    <item>http://connect.rom.miui.com/generate_204</item>
</string-array>
```
