AOSP 10 中，Wi-Fi 相关的 Java 类位于 `frameworks/base/wifi/java/android/net/wifi` 目录下

AOSP 12 开始，Wi-Fi 模块被重构为独立的 APEX 模块，Wi-Fi 相关的 Java 类被移动到了 `packages/modules/Wifi/framework/java/android/net/wifi` 目录



frameworks/base/core/java/com/android/internal/space/api/WiFiMock.java的构建文件

```yml
frameworks/base/core/java/Android.bp

filegroup {
    name: "framework-core-sources",
    srcs: [
        "**/*.java",!!!!!!!!!!!!!!!!
        "**/*.aidl",
    ],
    visibility: ["//frameworks/base"],
}

frameworks/base/Android.bp
filegroup {
    name: "framework-non-updatable-sources",
    srcs: [
        // Java/AIDL sources under frameworks/base
        ":framework-annotations",
        ":framework-blobstore-sources",
        ":framework-core-sources",!!!!!!!!!!!!!!!!
        ":framework-drm-sources",
        ":framework-graphics-nonupdatable-sources",
        ":framework-jobscheduler-sources", // jobscheduler is not a module for R
        ":framework-keystore-sources",
        ":framework-identity-sources",
        ":framework-location-sources",
        ":framework-lowpan-sources",
        ":framework-mca-effect-sources",
        ":framework-mca-filterfw-sources",
        ":framework-mca-filterpacks-sources",
        ":framework-media-sources",
        ":framework-mms-sources",
        ":framework-opengl-sources",
        ":framework-rs-sources",
        ":framework-sax-sources",
        ":framework-telecomm-sources",
        ":framework-telephony-common-sources",
        ":framework-telephony-sources",
        ":framework-vcn-util-sources",
        ":framework-wifi-annotations",
        ":framework-wifi-non-updatable-sources",
        ":PacProcessor-aidl-sources",
        ":ProxyHandler-aidl-sources",
        ":net-utils-framework-common-srcs",

        // AIDL from frameworks/base/native/
        ":platform-compat-native-aidl",

        // AIDL sources from external directories
        ":android.hardware.security.keymint-V1-java-source",
        ":android.hardware.security.secureclock-V1-java-source",
        ":android.security.apc-java-source",
        ":android.security.authorization-java-source",
        ":android.security.legacykeystore-java-source",
        ":android.security.maintenance-java-source",
        ":android.security.metrics-java-source",
        ":android.system.keystore2-V1-java-source",
        ":credstore_aidl",
        ":dumpstate_aidl",
        ":framework_native_aidl",
        ":gatekeeper_aidl",
        ":gsiservice_aidl",
        ":guiconstants_aidl",
        ":idmap2_aidl",
        ":idmap2_core_aidl",
        ":incidentcompanion_aidl",
        ":inputconstants_aidl",
        ":installd_aidl",
        ":libaudioclient_aidl",
        ":libbinder_aidl",
        ":libbluetooth-binder-aidl",
        ":libcamera_client_aidl",
        ":libcamera_client_framework_aidl",
        ":packagemanager_aidl",
        ":libupdate_engine_aidl",
        ":resourcemanager_aidl",
        ":storaged_aidl",
        ":vold_aidl",
        ":deviceproductinfoconstants_aidl",

        // For the generated R.java and Manifest.java
        ":framework-res{.aapt.srcjar}",

        // etc.
        ":framework-javastream-protos",
        ":statslog-framework-java-gen", // FrameworkStatsLog.java
        ":audio_policy_configuration_V7_0",
    ],
}


filegroup {
    name: "android-non-updatable-stub-sources",
    srcs: [
        ":framework-mime-sources", // mimemap builds separately but has no separate droidstubs.
        ":framework-non-updatable-sources",!!!!!!!!!!!!!!!!========================
        ":opt-telephony-srcs",
        ":opt-net-voip-srcs",
        "core/java/**/*.logtags",
        "**/package.html",
    ],
    visibility: ["//visibility:private"],
}

java_defaults {
    name: "framework-minus-apex-defaults",
    defaults: ["framework-aidl-export-defaults"],
    srcs: [
        ":framework-non-updatable-sources",!!!!!!!!!!!!!!!!========================
        "core/java/**/*.logtags",
    ],
    aidl: {
        generate_get_transaction_name: true,
        local_include_dirs: [
            "media/aidl",
        ],
        include_dirs: [
            "frameworks/av/aidl",
            "frameworks/native/libs/permission/aidl",
            "packages/modules/Connectivity/framework/aidl-export",
        ],
    },
    dxflags: [
        "--core-library",
        "--multi-dex",
    ],
    jarjar_rules: ":framework-jarjar-rules",
    javac_shard_size: 150,
    plugins: [
        "view-inspector-annotation-processor",
        "staledataclass-annotation-processor",
        "error_prone_android_framework",
    ],
    required: [
        "framework-platform-compat-config",
        // TODO: remove gps_debug and protolog.conf.json when the build system propagates "required" properly.
        "gps_debug.conf",
        "icu4j-platform-compat-config",
        "protolog.conf.json.gz",
        "services-platform-compat-config",
        "documents-ui-compat-config",
        "calendar-provider-compat-config",
    ],
    libs: [
        "app-compat-annotations",
        "ext",
        "framework-updatable-stubs-module_libs_api",
        "unsupportedappusage",
    ],
    sdk_version: "core_platform",
    static_libs: [
        "bouncycastle-repackaged-unbundled",
        "framework-internal-utils",
        // If MimeMap ever becomes its own APEX, then this dependency would need to be removed
        // in favor of an API stubs dependency in java_library "framework" below.
        "mimemap",
        "av-types-aidl-java",
        "tv_tuner_resource_manager_aidl_interface-java",
        "soundtrigger_middleware-aidl-java",
        "modules-utils-preconditions",
        "modules-utils-os",
        "framework-permission-aidl-java",
        "spatializer-aidl-java",
        "audiopolicy-types-aidl-java",

	// add by ntimespace at 2024-11-28
	"android.hardware.health-V1.0-java",
    ],
}



stubs_defaults {
    name: "android-non-updatable-stubs-defaults",
    srcs: [":android-non-updatable-stub-sources"],
    sdk_version: "none",
    system_modules: "none",
    java_version: "1.8",
    arg_files: ["core/res/AndroidManifest.xml"],
    // TODO(b/147699819): remove below aidl includes.
    aidl: {
        local_include_dirs: [
            "apex/media/aidl/stable",
            "media/aidl",
            "telephony/java",
        ],
        include_dirs: [
            "frameworks/av/aidl",
            "frameworks/native/libs/permission/aidl",
            "packages/modules/Connectivity/framework/aidl-export",
        ],
    },
    // These are libs from framework-internal-utils that are required (i.e. being referenced)
    // from framework-non-updatable-sources. Add more here when there's a need.
    // DO NOT add the entire framework-internal-utils. It might cause unnecessary circular
    // dependencies gets bigger.
    libs: [
        "android.hardware.cas-V1.2-java",
        "android.hardware.health-V1.0-java-constants",
        "android.hardware.radio-V1.5-java",
        "android.hardware.radio-V1.6-java",
        "android.hardware.thermal-V1.0-java-constants",
        "android.hardware.thermal-V2.0-java",
        "android.hardware.tv.input-V1.0-java-constants",
        "android.hardware.tv.tuner-V1.0-java-constants",
        "android.hardware.tv.tuner-V1.1-java-constants",
        "android.hardware.usb-V1.0-java-constants",
        "android.hardware.usb-V1.1-java-constants",
        "android.hardware.usb.gadget-V1.0-java",
        "android.hardware.vibrator-V1.3-java",
        "framework-protos",
        "art.module.public.api",
        // There are a few classes from modules used by the core that
        // need to be resolved by metalava. We use a prebuilt stub of the
        // full sdk to ensure we can resolve them. If a new class gets added,
        // the prebuilts/sdk/current needs to be updated.
        "sdk_system_current_android",
        // NOTE: The below can be removed once the prebuilt stub contains IKE.
        "sdk_system_current_android.net.ipsec.ike",
    ],
    filter_packages: packages_to_document,
    high_mem: true, // Lots of sources => high memory use, see b/170701554
    installable: false,
    annotations_enabled: true,
    previous_api: ":android.api.public.latest",
    merge_annotations_dirs: ["metalava-manual"],
    defaults_visibility: ["//visibility:private"],
    visibility: ["//frameworks/base/api"],
}


java_library {
    name: "framework-minus-apex-intdefs",!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    defaults: ["framework-minus-apex-defaults"],!!!!!!!!!!!!!!!!!!!!!!
    plugins: ["intdef-annotation-processor"],
}

java_library {
    name: "framework-minus-apex",!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    defaults: ["framework-minus-apex-defaults"],!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    installable: true,
    // For backwards compatibility.
    stem: "framework",
    apex_available: ["//apex_available:platform"],
    visibility: [
        "//frameworks/base",
        // TODO(b/147128803) remove the below lines
        "//frameworks/base/apex/appsearch/framework",
        "//frameworks/base/apex/blobstore/framework",
        "//frameworks/base/apex/jobscheduler/framework",
        "//frameworks/base/packages/Tethering/tests/unit",
        "//packages/modules/Connectivity/Tethering/tests/unit",
    ],
    errorprone: {
        javacflags: [
            "-Xep:AndroidFrameworkBinderIdentity:ERROR",
            "-Xep:AndroidFrameworkCompatChange:ERROR",
            "-Xep:AndroidFrameworkUid:ERROR",
        ],
    },
}

```











---



packages/modules/Wifi/framework/java/android/net/wifi/WifiSsid.java的构建

```yml
packages/modules/Wifi/framework/Android.bp
filegroup {
    name: "framework-wifi-updatable-java-sources",
    srcs: [
        "java/**/*.java",!!!!!!!!!!!!!!
        "java/**/*.aidl",
    ],
    path: "java",
    visibility: ["//visibility:private"],
}

filegroup {
    name: "framework-wifi-updatable-sources",
    srcs: [
        ":framework-wifi-updatable-java-sources",!!!!!!!!!!!
        ":framework-wifi-updatable-exported-aidl-sources",
        ":module-utils-os-aidls",
    ],
}

java_defaults {
    name: "framework-wifi-defaults",
    defaults: ["wifi-module-sdk-version-defaults"],
    static_libs: [
        "framework-wifi-util-lib",
        "android.hardware.wifi-V1.0-java-constants",
        "modules-utils-build",
        "modules-utils-os",
        "androidx.annotation_annotation",
    ],
    libs: [
        "unsupportedappusage", // for android.compat.annotation.UnsupportedAppUsage
        "framework-connectivity.stubs.module_lib",
    ],
    aidl: {
        include_dirs: [
            "packages/modules/Connectivity/framework/aidl-export",
        ],
    },
    srcs: [
        ":framework-wifi-updatable-sources",!!!!!!!!!!!!!!
        ":module-utils-os-aidls",
    ],
}

java_library {
    name: "framework-wifi-pre-jarjar",
    defaults: ["framework-wifi-defaults"],
    sdk_version: "module_current",
    libs: ["framework-annotations-lib"],
    // java_api_finder must accompany `srcs` (`srcs` defined in `framework-wifi-defaults`)
    plugins: ["java_api_finder"],
    installable: false,
    visibility: [
        "//frameworks/opt/net/wifi/service",
        "//frameworks/opt/net/wifi/tests/wifitests",
        "//packages/modules/Wifi/service",
        "//packages/modules/Wifi/service/tests/wifitests",
    ],
}

// post-jarjar version of framework-wifi
java_sdk_library {
    name: "framework-wifi",
    defaults: [
        "framework-module-defaults",
        "framework-wifi-defaults",
    ],

    stub_only_libs: ["framework-connectivity.stubs.module_lib"],

    jarjar_rules: ":wifi-jarjar-rules",

    installable: true,
    optimize: {
        enabled: false
    },
    hostdex: true, // for hiddenapi check

    // Restrict access to implementation library.
    impl_library_visibility: [
        "//frameworks/opt/net/wifi/service:__subpackages__",
        "//packages/modules/Wifi/service:__subpackages__",
    ] + test_access_hidden_api_whitelist,

    apex_available: [
        "com.android.wifi",
        "test_com.android.wifi",
    ],
    permitted_packages: [
        "android.hardware.wifi",
        "android.net.wifi",
        // Created by jarjar rules.
        "com.android.wifi.x",
    ],
    lint: {
        strict_updatability_linting: true,
    },
}

```







---

packages/modules/Wifi/service/java/com/android/server/wifi/WifiServiceImpl.java

```yml
packages/modules/Wifi/service/Android.bp
filegroup {
    name: "wifi-service-srcs",
    srcs: [
        "java/**/*.java",!!!!!!!!!!!!!!!!!!!!!!!!!
        "java/**/*.logtags",
        ":framework-wifi-service-shared-srcs",
        ":net-utils-wifi-service-common-srcs",
        ":statslog-wifi-java-gen",
        ":coex-table-parser",
    ],
}

java_library {
    name: "wifi-service-pre-jarjar",
    installable: false,
    defaults: ["wifi-service-common"],
    srcs: [ ":wifi-service-srcs" ],!!!!!!!!!!!!!!!!!!!
    // java_api_finder must accompany `srcs`
    plugins: ["java_api_finder"],

    sdk_version: "system_server_current",
    lint: {
        baseline_filename: "lint-baseline-pre-jarjar.xml",
        strict_updatability_linting: true,
    },
    libs: [
        "error_prone_annotations",
        "jsr305",
        "framework-annotations-lib",
        // load the resources from the resources APK.
        "ServiceWifiResources",
        // need pre-jarjar symbols so that wifi-service can reference the original class names at
        // compile time
        "framework-wifi-pre-jarjar",
        "framework-connectivity.stubs.module_lib",
        "framework-statsd.stubs.module_lib",
        "framework-tethering.stubs.module_lib",
        "unsupportedappusage",
    ],

    static_libs: [
        "android.hardware.wifi-V1.0-java",
        "android.hardware.wifi-V1.1-java",
        "android.hardware.wifi-V1.2-java",
        "android.hardware.wifi-V1.3-java",
        "android.hardware.wifi-V1.4-java",
        "android.hardware.wifi-V1.5-java",
        "android.hardware.wifi.hostapd-V1.0-java",
        "android.hardware.wifi.hostapd-V1.1-java",
        "android.hardware.wifi.hostapd-V1.2-java",
        "android.hardware.wifi.hostapd-V1.3-java",
        "android.hardware.wifi.supplicant-V1.0-java",
        "android.hardware.wifi.supplicant-V1.1-java",
        "android.hardware.wifi.supplicant-V1.2-java",
        "android.hardware.wifi.supplicant-V1.3-java",
        "android.hardware.wifi.supplicant-V1.4-java",
        "android.hidl.manager-V1.2-java",
        "androidx.annotation_annotation",
        "bouncycastle-unbundled",
        "ksoap2",
        // Note: libprotobuf-java-lite uses a few core platform APIs which
        // does show up as @hide API usage. But, this can be safely ignored
        // since the library uses reflection to ensure that the OS does provide
        // the necessary core platform APIs.
        "libprotobuf-java-lite",
        "libnanohttpd",
        "services.net-module-wifi",
        "wifi-lite-protos",
        "wifi-nano-protos",
    ],
}


java_library {
    name: "service-wifi",！！！！！！！！！！！！！！！！！！！！！！！！！！！！！
    defaults: ["wifi-service-common"],
    installable: true,
    static_libs: ["wifi-service-pre-jarjar"],

    // need to include `libs` so that Soong doesn't complain about missing classes after jarjaring
    libs: [
        "framework-wifi.impl",
    ],

    sdk_version: "system_server_current",

    jarjar_rules: ":wifi-jarjar-rules",
    optimize: {
        enabled: true,
        shrink: true,
        proguard_flags_files: ["proguard.flags"],
    },
    dex_preopt: {
        enabled: false,
        app_image: false,
    },

    visibility: [
        "//frameworks/opt/net/wifi/service/apex",
        "//frameworks/opt/net/wifi/tests/wifitests/apex",
        "//packages/modules/Wifi/apex",
        "//packages/modules/Wifi/service/tests/wifitests/apex",
    ],
    apex_available: [
        "com.android.wifi",
        "test_com.android.wifi",
    ],
}


packages/modules/Wifi/apex/Android.bp
apex_defaults {
    name: "com.android.wifi-defaults",
    androidManifest: ":com.android.wifi-androidManifest",
    bootclasspath_fragments: ["com.android.wifi-bootclasspath-fragment"],
    java_libs: [
        "service-wifi",！！！！！！！！！！！！！！！！！！
    ],
    // from build rule `cacerts_wfa`
    prebuilts: [
        "target-cacert-wifi-674b5f5b.0",
        "target-cacert-wifi-21125ccd.0",
        "target-cacert-wifi-ea93cb5b.0",
    ],
    key: "com.android.wifi.key",
    certificate: ":com.android.wifi.certificate",
    apps: [
        "OsuLogin",
        "ServiceWifiResources",
    ],
    min_sdk_version: "30",
    updatable: true,
    // Indicates that pre-installed version of this apex can be compressed.
    // Whether it actually will be compressed is controlled on per-device basis.
    compressible: true,
}

// Mainline wifi apex module.
apex {
    name: "com.android.wifi",
    defaults: ["com.android.wifi-defaults"],
    manifest: "apex_manifest.json",
}

```





报错：

```

packages/modules/Wifi/service/java/com/android/server/wifi/WifiServiceImpl.java:128: error: package com.android.internal.space.api does not exist
import com.android.internal.space.api.WiFiMock;
                                     ^
packages/modules/Wifi/service/java/com/android/server/wifi/WifiServiceImpl.java:237: error: cannot find symbol
    WiFiMock mMock;
    ^
  symbol:   class WiFiMock
  location: class WifiServiceImpl
2 errors
[ 13% 143/1098] R8: out/target/common/obj/APPS/Camera2_intermediates/dex/classes.dex
Warning: Missing class com.google.errorprone.annotations.CanIgnoreReturnValue (referenced from: java.lang.Object com.google.common.base.AbstractIterator.endOfData() and 126 other contexts)
Missing class com.google.errorprone.annotations.CompatibleWith (referenced from: boolean com.google.common.collect.Multimap.containsEntry(java.lang.Object, java.lang.Object) and 1 other context)
Missing class com.google.errorprone.annotations.DoNotMock (referenced from: com.google.common.base.Optional and 8 other contexts)
Missing class com.google.errorprone.annotations.ForOverride (referenced from: boolean com.google.common.base.Equivalence.doEquivalent(java.lang.Object, java.lang.Object) and 4 other contexts)
Missing class com.google.errorprone.annotations.concurrent.GuardedBy (referenced from: void com.google.common.collect.MapMakerInternalMap$Segment.drainKeyReferenceQueue(java.lang.ref.ReferenceQueue) and 5 other contexts)
Missing class com.google.errorprone.annotations.concurrent.LazyInit (referenced from: com.google.common.collect.ImmutableSet com.google.common.collect.ImmutableMap.entrySet and 5 other contexts)
[ 13% 144/1098] //packages/apps/ManagedProvisioning:ManagedProvisioning r8 [common]
Warning: Library class com.android.internal.logging.nano.MetricsProto$MetricsEvent extends program class com.android.framework.protobuf.nano.MessageNano
Warning: Missing class org.jetbrains.annotations.NotNull (referenced from: kotlin.Unit kotlin.Unit.INSTANCE and 179 other contexts)
Missing class org.jetbrains.annotations.Nullable (referenced from: okio.Segment okio.Buffer.head and 18 other contexts)
03:43:34 ninja failed with: exit status 1

#### failed to build some targets (48 seconds) ####

root@snowrepo:/snow/android12-rk3588# 
```







分析：
WiFiMock.java属于com.android.internal.space.api，编译成framework-minus-apex的jar包。

依赖：

import android.net.wifi.ScanResult;

import android.net.wifi.SupplicantState;

import android.net.wifi.WifiInfo;

import android.net.wifi.WifiSsid;



WifiSsid.java现是android.net.wifi，编译成framework-wifi的java_sdk包



WifiServiceImpl.java是android.net.wifi，编译成com.android.wifi的apex包








目前不知道在android.net.wifi包里如何获取我们的自定义的服务或者其他系统服务（例如在WifiServiceImpl.java中获取我们frameworks/base/core/java/com/android/internal/space/NineDSpaceManager.java），
导致功能实现比较困难