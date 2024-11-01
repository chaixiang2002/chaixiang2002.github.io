vendor/opengapps/build/modules/GoogleServicesFramework/Android.mk

[Android AOSP内置GMS服务 - asjhan - 博客园](https://www.cnblogs.com/jhanzhou/p/17337871.html)

[opengapps/aosp_build: AOSP Build system compatible version of Open GApps](https://github.com/opengapps/aosp_build)

```
vendor/opengapps/build
vendor/opengapps/sources/all
vendor/opengapps/sources/arm64
```

device/manufacturer/product/device.mk

```makefile
# add google apps
GAPPS_VARIANT := pico
```

device/manufacturer/product/device.mk

```makefile
$(call inherit-product, vendor/opengapps/build/opengapps-packages.mk)
```

vendor/opengapps/build/opengapps-packages.mk

```makefile
GAPPS_PRODUCT_PACKAGES += \
    GoogleServicesFramework \             # gsf
    Phonesky                              # 这是谷歌商店com.android.vending



# GAPPS_PRODUCT_PACKAGES += \
    GoogleServicesFramework \
    GooglePlayServices \
    Phonesky
```

---

```
root@snowrepo:/snow/android10-rk3588/vendor/opengapps# find -name '*.apk' |grep gsf
./sources/all/app/com.google.android.gsf.notouch/14/nodpi/1.apk
./sources/all/priv-app/com.google.android.gsf.login/21/nodpi/22.apk
./sources/all/priv-app/com.google.android.gsf.login/23/nodpi/23.apk
./sources/all/priv-app/com.google.android.gsf.login/24/nodpi/24.apk
./sources/all/priv-app/com.google.android.gsf.login/25/nodpi/25.apk
./sources/all/priv-app/com.google.android.gsf.login/8/nodpi/19.apk
./sources/all/priv-app/com.google.android.gsf/19/nodpi/19.apk
./sources/all/priv-app/com.google.android.gsf/21/nodpi/21.apk
./sources/all/priv-app/com.google.android.gsf/22/nodpi/22.apk
./sources/all/priv-app/com.google.android.gsf/23/nodpi/23.apk
./sources/all/priv-app/com.google.android.gsf/24/nodpi/24.apk
./sources/all/priv-app/com.google.android.gsf/25/nodpi/25.apk
./sources/all/priv-app/com.google.android.gsf/26/nodpi/26.apk
./sources/all/priv-app/com.google.android.gsf/27/nodpi/27.apk
./sources/all/priv-app/com.google.android.gsf/28/nodpi/28.apk
./sources/all/priv-app/com.google.android.gsf/29/nodpi/29.apk
./sources/all/priv-app/com.google.android.gsf/30/nodpi/30.apk
./sources/all/priv-app/com.google.android.gsf/31/nodpi/31.apk
root@snowrepo:/snow/android10-rk3588/vendor/opengapps# find -name '*.apk' |grep gms
./sources/all/app/com.google.android.gms.policy_sidecar_aps/28/nodpi/2052073.apk
./sources/all/priv-app/com.google.android.gms.policy_sidecar_aps/28/nodpi/24900.apk
./sources/all/priv-app/com.google.android.gms.setup/21/nodpi/128400.apk
./sources/all/priv-app/com.google.android.gms.setup/24/nodpi/342400.apk
./sources/all/priv-app/com.google.android.gms.setup/26/nodpi/650400.apk
./sources/arm/priv-app/com.google.android.gms.leanback/19/213-320/14799069.apk
./sources/arm/priv-app/com.google.android.gms.leanback/21/213-320/220920091.apk
./sources/arm/priv-app/com.google.android.gms.leanback/30/213-320/220221090.apk
./sources/arm/priv-app/com.google.android.gms/16/160/212620001.apk
./sources/arm/priv-app/com.google.android.gms/16/240/212620002.apk
./sources/arm/priv-app/com.google.android.gms/16/320/212620003.apk
./sources/arm/priv-app/com.google.android.gms/16/480/212620004.apk
./sources/arm/priv-app/com.google.android.gms/19/nodpi/220221000.apk
./sources/arm/priv-app/com.google.android.gms/21/240/220920007.apk
./sources/arm/priv-app/com.google.android.gms/21/320/214857008.apk
./sources/arm/priv-app/com.google.android.gms/21/480/214857009.apk
./sources/arm/priv-app/com.google.android.gms/21/nodpi/214857006.apk
./sources/arm/priv-app/com.google.android.gms/23/240/220920016.apk
./sources/arm/priv-app/com.google.android.gms/23/320/220920017.apk
./sources/arm/priv-app/com.google.android.gms/23/480/220920018.apk
./sources/arm/priv-app/com.google.android.gms/23/nodpi/220920015.apk
./sources/arm/priv-app/com.google.android.gms/27/160/220920058.apk
./sources/arm/priv-app/com.google.android.gms/27/320/220920060.apk
./sources/arm/priv-app/com.google.android.gms/28/240/220221025.apk
./sources/arm/priv-app/com.google.android.gms/28/320/220920026.apk
./sources/arm/priv-app/com.google.android.gms/28/480/220920027.apk
./sources/arm/priv-app/com.google.android.gms/28/nodpi/220920024.apk
./sources/arm/priv-app/com.google.android.gms/29/240/214218034.apk
./sources/arm/priv-app/com.google.android.gms/29/320/214218035.apk
./sources/arm/priv-app/com.google.android.gms/29/480/214218036.apk
./sources/arm/priv-app/com.google.android.gms/29/nodpi/214218033.apk
./sources/arm/priv-app/com.google.android.gms/30/240/220221034.apk
./sources/arm/priv-app/com.google.android.gms/30/320/220221035.apk
./sources/arm/priv-app/com.google.android.gms/30/480/220221036.apk
./sources/arm/priv-app/com.google.android.gms/30/nodpi/220920033.apk
./sources/arm/priv-app/com.google.android.gms/31/480/220221043.apk
./sources/arm/priv-app/com.google.android.gms/31/nodpi/220221042.apk
./sources/arm64/app/com.google.android.gms.policy_sidecar_o/23/nodpi/20440.apk
./sources/arm64/priv-app/com.google.android.gms.leanback/21/213-320/220920092.apk
./sources/arm64/priv-app/com.google.android.gms.leanback/30/213-320/220221091.apk
./sources/arm64/priv-app/com.google.android.gms/21/320/214857011.apk
./sources/arm64/priv-app/com.google.android.gms/21/480/214857012.apk
./sources/arm64/priv-app/com.google.android.gms/21/nodpi/214857010.apk
./sources/arm64/priv-app/com.google.android.gms/23/320/220920020.apk
./sources/arm64/priv-app/com.google.android.gms/23/480/220920021.apk
./sources/arm64/priv-app/com.google.android.gms/23/nodpi/220920019.apk
./sources/arm64/priv-app/com.google.android.gms/28/320/220221029.apk
./sources/arm64/priv-app/com.google.android.gms/28/480/220920030.apk
./sources/arm64/priv-app/com.google.android.gms/28/nodpi/220920028.apk
./sources/arm64/priv-app/com.google.android.gms/29/320/214218038.apk
./sources/arm64/priv-app/com.google.android.gms/29/480/214218039.apk
./sources/arm64/priv-app/com.google.android.gms/29/nodpi/214218037.apk
./sources/arm64/priv-app/com.google.android.gms/30/320/220920038.apk
./sources/arm64/priv-app/com.google.android.gms/30/480/220920039.apk
./sources/arm64/priv-app/com.google.android.gms/30/nodpi/220920037.apk
./sources/arm64/priv-app/com.google.android.gms/31/480/220920045.apk
./sources/arm64/priv-app/com.google.android.gms/31/nodpi/220920044.apk
root@snowrepo:/snow/android10-rk3588/vendor/opengapps# find -name '*.apk' |grep vending
./sources/arm/priv-app/com.android.vending.leanback/21/nodpi/83011408.apk
./sources/arm/priv-app/com.android.vending/19/nodpi/83032100.apk
./sources/arm/priv-app/com.android.vending/21/nodpi/83032110.apk
./sources/arm64/priv-app/com.android.vending/21/nodpi/83032110.apk
root@snowrepo:/snow/android10-rk3588/vendor/opengapps# 
```





```shell
pm list package |grep gms
pm list package |grep gsf
pm list package |grep com.android.vending

dumpsys package com.google.android.gsf |grep versionName
dumpsys package com.google.android.gms |grep versionName
dumpsys package com.android.vending |grep versionName
```



```
vendor/opengapps/sources/all/priv-app/com.google.android.gsf/29/nodpi/29.apk

vendor/opengapps/sources/arm64/priv-app/com.google.android.gms/29/480/214218039.apk
```

google server 24.37.34
google play 40.0.18-29[0][PR]