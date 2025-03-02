[写给应用开发的 Android Framework 教程——HAL与硬件服务之 Hal 层添加访问 linux 驱动的接口 - 掘金](https://juejin.cn/post/7229202557049749564?searchId=202502201409074334DB40C20087A1F1EE)！！！！！！！！！！！！！！

[Android HIDL理解（基于Android O）_android13移植hidl-CSDN博客](https://blog.csdn.net/kuang_tian_you/article/details/86599869)



```
root@PC-20230101BFYW:/snow/android10-rk3588/vendor/jelly# tree
.
└── hardware
    └── interfaces
        ├── Android.bp
        ├── current.txt
        ├── hello_hidl
        │   └── 1.0
        │       ├── Android.bp
        │       ├── IHello.hal
        │       └── default
        │           ├── Android.bp
        │           ├── Hello.cpp
        │           ├── Hello.h
        │           ├── jelly.hardware.hello_hidl@1.0-service.rc
        │           ├── jelly.hardware.hello_hidl@1.0-service.xml
        │           ├── service.cpp
        │           └── test
        │               ├── Android.bp
        │               └── hello_hidl_test.cpp
        └── update-makefiles.sh

6 directories, 13 files
root@PC-20230101BFYW:/snow/android10-rk3588/vendor/jelly# 
```



```yml
//vendor/jelly/hardware/interfaces/Android.bp----------------------------
hidl_package_root {
    name: "jelly.hardware",
    path: "vendor/jelly/hardware/interfaces",
}

//vendor/jelly/hardware/interfaces/hello_hidl/1.0/Android.bp
hidl_interface {
    name: "jelly.hardware.hello_hidl@1.0",
    root: "jelly.hardware",
    srcs: [
        "IHello.hal",
    ],
    interfaces: [
        "android.hidl.base@1.0",
    ],
    gen_java: false,
}

//vendor/jelly/hardware/interfaces/hello_hidl/1.0/default/Android.bp----
// FIXME: your file license if you have one

cc_library_shared {
    name: "jelly.hardware.hello_hidl@1.0-impl",
    relative_install_path: "hw",
    proprietary: true,
    srcs: [
        "Hello.cpp",
    ],
    shared_libs: [
        "libhidlbase",
        "libhidltransport",
        "libutils",
        "jelly.hardware.hello_hidl@1.0",
        "liblog",
    ],
}

cc_binary {
    name: "jelly.hardware.hello_hidl@1.0-service",
    init_rc: ["jelly.hardware.hello_hidl@1.0-service.rc"],
    vintf_fragments: ["jelly.hardware.hello_hidl@1.0-service.xml"],
    defaults: ["hidl_defaults"],
    relative_install_path: "hw",
    vendor: true,
    srcs: ["service.cpp", "Hello.cpp"],
    shared_libs: [
        "jelly.hardware.hello_hidl@1.0",
        "libhardware",
        "libhidlbase",
        "libhidltransport",
        "libutils",
        "liblog",
    ],
}

//vendor/jelly/hardware/interfaces/hello_hidl/1.0/default/test/Android.bp---------
cc_binary {
    name: "hello_hidl_test",
    srcs: ["hello_hidl_test.cpp"],
    vendor: true,
    shared_libs: [
        "liblog",
        "jelly.hardware.hello_hidl@1.0",
        "libhidlbase",
        "libhidltransport",
        "libhwbinder",
        "libutils",
    ],
}

```

```xml
// vendor/jelly/hardware/interfaces/hello_hidl/1.0/default/jelly.hardware.hello_hidl@1.0-service.rc
service vendor_hello_hidl_service /vendor/bin/hw/jelly.hardware.hello_hidl@1.0-service
	class hal
	user system
	group system


// vendor/jelly/hardware/interfaces/hello_hidl/1.0/default/jelly.hardware.hello_hidl@1.0-service.xml
<manifest version="1.0" type="device">
  <hal format="hidl">
        <name>jelly.hardware.hello_hidl</name>
        <transport>hwbinder</transport>
        <version>1.0</version>
        <interface>
            <name>IHello</name>
            <instance>default</instance>
        </interface>
    </hal>
</manifest>

```



```makefile

BOARD_SEPOLICY_DIRS += \
    device/Jelly/Rice14/sepolicy

PRODUCT_PACKAGES += \
    jelly.hardware.hello_hidl@1.0-service \
    hello_hidl_test \
    jelly.hardware.hello_hidl@1.0-impl \

```



https://s.juzicloud.vip/link/1G8hIWKuLQsmUNkE?clash=1