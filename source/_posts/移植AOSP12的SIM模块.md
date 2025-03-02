![image-20250216223920048](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502162239841.png)





报错

```

root@snowrepo:/snow/android12-rk3588# ./build_docker_android.sh -A --version=0002
14:35:13 Build sandboxing disabled due to nsjail error.
14:35:14 Build sandboxing disabled due to nsjail error.
14:35:15 Build sandboxing disabled due to nsjail error.

============================================
PLATFORM_VERSION_CODENAME=REL
PLATFORM_VERSION=12
TARGET_PRODUCT=rk3588_docker
TARGET_BUILD_VARIANT=user
TARGET_BUILD_TYPE=release
TARGET_ARCH=arm64
TARGET_ARCH_VARIANT=armv8-a
TARGET_CPU_VARIANT=generic
TARGET_2ND_ARCH=arm
TARGET_2ND_ARCH_VARIANT=armv8-a
TARGET_2ND_CPU_VARIANT=generic
HOST_ARCH=x86_64
HOST_2ND_ARCH=x86
HOST_OS=linux
HOST_OS_EXTRA=Linux-5.4.0-192-generic-x86_64-Ubuntu-20.04.3-LTS
HOST_CROSS_OS=windows
HOST_CROSS_ARCH=x86
HOST_CROSS_2ND_ARCH=x86_64
HOST_BUILD_TYPE=release
BUILD_ID=SD2A.220601.003.B1
OUT_DIR=out
============================================
will build android
lpunpack is /snow/android12-rk3588/out/soong/host/linux-x86/bin/lpunpack
lpunpack is exit
start install clean



14:35:18 Build sandboxing disabled due to nsjail error.
build/make/core/soong_config.mk:195: warning: BOARD_PLAT_PUBLIC_SEPOLICY_DIR has been deprecated. Use SYSTEM_EXT_PUBLIC_SEPOLICY_DIRS instead.
build/make/core/soong_config.mk:196: warning: BOARD_PLAT_PRIVATE_SEPOLICY_DIR has been deprecated. Use SYSTEM_EXT_PRIVATE_SEPOLICY_DIRS instead.
============================================
PLATFORM_VERSION_CODENAME=REL
PLATFORM_VERSION=12
TARGET_PRODUCT=rk3588_docker
TARGET_BUILD_VARIANT=user
TARGET_BUILD_TYPE=release
TARGET_ARCH=arm64
TARGET_ARCH_VARIANT=armv8-a
TARGET_CPU_VARIANT=generic
TARGET_2ND_ARCH=arm
TARGET_2ND_ARCH_VARIANT=armv8-a
TARGET_2ND_CPU_VARIANT=generic
HOST_ARCH=x86_64
HOST_2ND_ARCH=x86
HOST_OS=linux
HOST_OS_EXTRA=Linux-5.4.0-192-generic-x86_64-Ubuntu-20.04.3-LTS
HOST_CROSS_OS=windows
HOST_CROSS_ARCH=x86
HOST_CROSS_2ND_ARCH=x86_64
HOST_BUILD_TYPE=release
BUILD_ID=SD2A.220601.003.B1
OUT_DIR=out
============================================
14:35:18 Entire data directory removed.
14:35:19 Deleted images and staging directories.

#### build completed successfully (2 seconds) ####

start build android
14:35:20 Build sandboxing disabled due to nsjail error.
build/make/core/soong_config.mk:195: warning: BOARD_PLAT_PUBLIC_SEPOLICY_DIR has been deprecated. Use SYSTEM_EXT_PUBLIC_SEPOLICY_DIRS instead.
build/make/core/soong_config.mk:196: warning: BOARD_PLAT_PRIVATE_SEPOLICY_DIR has been deprecated. Use SYSTEM_EXT_PRIVATE_SEPOLICY_DIRS instead.
============================================
PLATFORM_VERSION_CODENAME=REL
PLATFORM_VERSION=12
TARGET_PRODUCT=rk3588_docker
TARGET_BUILD_VARIANT=user
TARGET_BUILD_TYPE=release
TARGET_ARCH=arm64
TARGET_ARCH_VARIANT=armv8-a
TARGET_CPU_VARIANT=generic
TARGET_2ND_ARCH=arm
TARGET_2ND_ARCH_VARIANT=armv8-a
TARGET_2ND_CPU_VARIANT=generic
HOST_ARCH=x86_64
HOST_2ND_ARCH=x86
HOST_OS=linux
HOST_OS_EXTRA=Linux-5.4.0-192-generic-x86_64-Ubuntu-20.04.3-LTS
HOST_CROSS_OS=windows
HOST_CROSS_ARCH=x86
HOST_CROSS_2ND_ARCH=x86_64
HOST_BUILD_TYPE=release
BUILD_ID=SD2A.220601.003.B1
OUT_DIR=out
============================================
device/ntimespace/ntimespace_prod.mk was modified, regenerating...
device/ntimespace/ntimespace_prod.mk was modified, regenerating...
[  0% 1/224] including out/soong/Android-rk3588_docker.mk ...
    0:39 including out/soong/Android-rk3588_docker.mk ...



















[ 62% 140/224] including hardware/ntimespace/libhwjpeg/Android.mk ...
git-7ba9240ca6 author: chaixiang 2025-02-14 tmp
[ 91% 205/224] including system/sepolicy/Android.mk ...
system/sepolicy/Android.mk:57: warning: BOARD_PLAT_PUBLIC_SEPOLICY_DIR has been deprecated. Use SYSTEM_EXT_PUBLIC_SEPOLICY_DIRS instead.
system/sepolicy/Android.mk:62: warning: BOARD_PLAT_PRIVATE_SEPOLICY_DIR has been deprecated. Use SYSTEM_EXT_PRIVATE_SEPOLICY_DIRS instead.
[ 99% 222/224] finishing build rules ...


[ 16% 2458/14591] build out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log
FAILED: out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log
/bin/bash -c "(echo \"PRODUCT_OTA_ENFORCE_VINTF_KERNEL_REQUIREMENTS=false\" > out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log ) && (echo -n -e 'Deps: \\n  ' >> out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log ) && (sed 's/ /\\n  /g' <<< \"out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml out/target/product/rk3588_docker/system/etc/vintf/manifest.xml out/target/product/rk3588_docker/system/etc/vintf/manifest/android.frameworks.stats@1.0-service.xml out/target/product/rk3588_docker/system/etc/vintf/manifest/android.hidl.allocator@1.0-service.xml out/target/product/rk3588_docker/system/etc/vintf/manifest/android.system.keystore2-service.xml out/target/product/rk3588_docker/system/etc/vintf/manifest/android.system.suspend@1.0-service.xml out/target/product/rk3588_docker/system/etc/vintf/manifest/manifest_android.frameworks.cameraservice.service@2.2.xml out/target/product/rk3588_docker/system/etc/vintf/manifest/manifest_media_c2_software.xml out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml out/target/product/rk3588_docker/vendor/etc/vintf/compatibility_matrix.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.cas@1.2-service.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.drm@1.4-service.widevine.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.gatekeeper@1.0-service.software.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.health@2.1.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.wifi@1.0-service.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.drm@1.2-service.clearkey.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.drm@1.4-service.clearkey.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.gnss@1.0.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_media_c2_V1_1.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/power-default.xml out/target/product/rk3588_docker/vendor/etc/vintf/manifest/rockchip.hardware.rockit.hw@1.0-service.xml\" >> out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log ) && (echo -n -e 'Args: \\n  ' >> out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log ) && (cat <<< \" --dirmap /system:out/target/product/rk3588_docker/system --dirmap /vendor:out/target/product/rk3588_docker/vendor --dirmap /odm:out/target/product/rk3588_docker/vendor/odm --dirmap /product:out/target/product/rk3588_docker/system/product --dirmap /system_ext:out/target/product/rk3588_docker/system/system_ext  --property ro.product.first_api_level=31\" >> out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log ) && (echo \"For ODM SKU = EMPTY_ODM_SKU_PLACEHOLDER, vendor SKU = EMPTY_VENDOR_SKU_PLACEHOLDER\" >> out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log; ( out/host/linux-x86/bin/checkvintf --check-compat  --dirmap /system:out/target/product/rk3588_docker/system --dirmap /vendor:out/target/product/rk3588_docker/vendor --dirmap /odm:out/target/product/rk3588_docker/vendor/odm --dirmap /product:out/target/product/rk3588_docker/system/product --dirmap /system_ext:out/target/product/rk3588_docker/system/system_ext  --property ro.product.first_api_level=31 --property ro.boot.product.hardware.sku= --property ro.boot.product.vendor.sku= >> out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log 2>&1 ) || (cat out/target/product/rk3588_docker/obj/PACKAGING/check_vintf_all_intermediates/check_vintf_compatible.log && exit 1) )"
PRODUCT_OTA_ENFORCE_VINTF_KERNEL_REQUIREMENTS=false
Deps: 
  out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml
  out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml
  out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml
  out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml
  out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml
  out/target/product/rk3588_docker/system/etc/vintf/manifest.xml
  out/target/product/rk3588_docker/system/etc/vintf/manifest/android.frameworks.stats@1.0-service.xml
  out/target/product/rk3588_docker/system/etc/vintf/manifest/android.hidl.allocator@1.0-service.xml
  out/target/product/rk3588_docker/system/etc/vintf/manifest/android.system.keystore2-service.xml
  out/target/product/rk3588_docker/system/etc/vintf/manifest/android.system.suspend@1.0-service.xml
  out/target/product/rk3588_docker/system/etc/vintf/manifest/manifest_android.frameworks.cameraservice.service@2.2.xml
  out/target/product/rk3588_docker/system/etc/vintf/manifest/manifest_media_c2_software.xml
  out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/compatibility_matrix.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.cas@1.2-service.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.drm@1.4-service.widevine.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.gatekeeper@1.0-service.software.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.health@2.1.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.wifi@1.0-service.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.drm@1.2-service.clearkey.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.drm@1.4-service.clearkey.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.gnss@1.0.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_media_c2_V1_1.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/power-default.xml
  out/target/product/rk3588_docker/vendor/etc/vintf/manifest/rockchip.hardware.rockit.hw@1.0-service.xml
Args: 
   --dirmap /system:out/target/product/rk3588_docker/system --dirmap /vendor:out/target/product/rk3588_docker/vendor --dirmap /odm:out/target/product/rk3588_docker/vendor/odm --dirmap /product:out/target/product/rk3588_docker/system/product --dirmap /system_ext:out/target/product/rk3588_docker/system/system_ext  --property ro.product.first_api_level=31
For ODM SKU = EMPTY_ODM_SKU_PLACEHOLDER, vendor SKU = EMPTY_VENDOR_SKU_PLACEHOLDER
checkvintf I 02-16 14:37:32 2189790 2189790 VintfObject.cpp:58] getFrameworkHalManifest: Reading VINTF information.
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/manifest/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/android.frameworks.stats@1.0-service.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/android.hidl.allocator@1.0-service.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/android.system.suspend@1.0-service.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/manifest_media_c2_software.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/manifest_android.frameworks.cameraservice.service@2.2.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/android.system.keystore2-service.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/product/etc/vintf/manifest.xml': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/manifest/': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest/': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 VintfObject.cpp:58] getDeviceHalManifest: Reading VINTF information.
checkvintf I 02-16 14:37:32 2189790 2189790 check_vintf.cpp:79] Sysprop ro.boot.product.vendor.sku=
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.cas@1.2-service.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.gatekeeper@1.0-service.software.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.drm@1.4-service.widevine.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.wifi@1.0-service.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.health@2.1.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.drm@1.2-service.clearkey.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.drm@1.4-service.clearkey.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.gnss@1.0.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/power-default.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_media_c2_V1_1.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/rockchip.hardware.rockit.hw@1.0-service.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 check_vintf.cpp:79] Sysprop ro.boot.product.hardware.sku=
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/odm/etc/vintf/manifest.xml': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/odm/etc/manifest.xml': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/vendor/odm/etc/vintf/manifest/': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 VintfObject.cpp:64] getDeviceHalManifest: Successfully processed VINTF information
checkvintf I 02-16 14:37:32 2189790 2189790 VintfObject.cpp:64] getFrameworkHalManifest: Successfully processed VINTF information
checkvintf I 02-16 14:37:32 2189790 2189790 VintfObject.cpp:58] getFrameworkCompatibilityMatrix: Reading VINTF information.
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 VintfObject.cpp:64] getFrameworkCompatibilityMatrix: Successfully processed VINTF information
checkvintf I 02-16 14:37:32 2189790 2189790 VintfObject.cpp:58] getDeviceCompatibilityMatrix: Reading VINTF information.
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/compatibility_matrix.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 VintfObject.cpp:64] getDeviceCompatibilityMatrix: Successfully processed VINTF information
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 14:37:32 2189790 2189790 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/': NAME_NOT_FOUND
checkvintf I 02-16 14:37:32 2189790 2189790 check_vintf.cpp:384] All HALs in device manifest are declared in FCM <= level 6
checkvintf E 02-16 14:37:32 2189790 2189790 check_vintf.cpp:620] files are incompatible: Cannot open out/target/product/rk3588_docker/system/product/etc/vintf/: No such file or directory
checkvintf E 02-16 14:37:32 2189790 2189790 check_vintf.cpp:620] android.hardware.radio@1.0::IRadio/slot1 is deprecated; requires at least 1.6
checkvintf E 02-16 14:37:32 2189790 2189790 check_vintf.cpp:620] android.hardware.radio@1.0::IRadio/slot1 is deprecated; requires at least 1.6
checkvintf E 02-16 14:37:32 2189790 2189790 check_vintf.cpp:620] android.hardware.radio@1.0::ISap/slot1 is deprecated; requires at least 1.2
checkvintf E 02-16 14:37:32 2189790 2189790 check_vintf.cpp:620] android.hardware.radio@1.0::ISap/slot1 is deprecated; requires at least 1.2: Success
INCOMPATIBLE
14:37:38 ninja failed with: exit status 1

#### failed to build some targets (02:19 (mm:ss)) ####

Build android failed!
root@snowrepo:/snow/android12-rk3588# 
root@snowrepo:/snow/android12-rk3588# 
root@snowrepo:/snow/android12-rk3588# 
root@snowrepo:/snow/android12-rk3588# 


```





android.hardware.radio移植报错

```
checkvintf I 02-16 17:51:45 2215869 2215869 VintfObject.cpp:58] getFrameworkHalManifest: Reading VINTF information.
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/manifest/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/android.frameworks.stats@1.0-service.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/android.hidl.allocator@1.0-service.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/android.system.suspend@1.0-service.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/manifest_android.frameworks.cameraservice.service@2.2.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/manifest_media_c2_software.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest/android.system.keystore2-service.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/product/etc/vintf/manifest.xml': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/manifest/': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest/': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 VintfObject.cpp:58] getDeviceHalManifest: Reading VINTF information.
checkvintf I 02-16 17:51:45 2215869 2215869 check_vintf.cpp:79] Sysprop ro.boot.product.vendor.sku=
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.drm@1.4-service.widevine.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.cas@1.2-service.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.gatekeeper@1.0-service.software.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.health@2.1.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.drm@1.2-service.clearkey.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.drm@1.4-service.clearkey.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/android.hardware.wifi@1.0-service.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/power-default.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_android.hardware.gnss@1.0.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/rockchip.hardware.rockit.hw@1.0-service.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/manifest/manifest_media_c2_V1_1.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 check_vintf.cpp:79] Sysprop ro.boot.product.hardware.sku=
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/odm/etc/vintf/manifest.xml': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/odm/etc/manifest.xml': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/vendor/odm/etc/vintf/manifest/': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 VintfObject.cpp:64] getDeviceHalManifest: Successfully processed VINTF information
checkvintf I 02-16 17:51:45 2215869 2215869 VintfObject.cpp:64] getFrameworkHalManifest: Successfully processed VINTF information
checkvintf I 02-16 17:51:45 2215869 2215869 VintfObject.cpp:58] getFrameworkCompatibilityMatrix: Reading VINTF information.
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 VintfObject.cpp:64] getFrameworkCompatibilityMatrix: Successfully processed VINTF information
checkvintf I 02-16 17:51:45 2215869 2215869 VintfObject.cpp:58] getDeviceCompatibilityMatrix: Reading VINTF information.
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/vendor/etc/vintf/compatibility_matrix.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 VintfObject.cpp:64] getDeviceCompatibilityMatrix: Successfully processed VINTF information
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/etc/vintf/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.3.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.5.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.4.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.6.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/compatibility_matrix.device.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:43] Fetch 'out/target/product/rk3588_docker/system/system_ext/etc/vintf/manifest.xml': OK
checkvintf I 02-16 17:51:45 2215869 2215869 HostFileSystem.cpp:54] List 'out/target/product/rk3588_docker/system/product/etc/vintf/': NAME_NOT_FOUND
checkvintf I 02-16 17:51:45 2215869 2215869 check_vintf.cpp:388] The following HALs in device manifest are not declared in FCM <= level 6: 
checkvintf I 02-16 17:51:45 2215869 2215869 check_vintf.cpp:391]   android.hardware.radio@1.6::ISap/slot1
checkvintf E 02-16 17:51:45 2215869 2215869 check_vintf.cpp:620] files are incompatible: The following instances are in the device manifest but not specified in framework compatibility matrix: 
checkvintf E 02-16 17:51:45 2215869 2215869 check_vintf.cpp:620]     android.hardware.radio@1.6::ISap/slot1
checkvintf E 02-16 17:51:45 2215869 2215869 check_vintf.cpp:620] Suggested fix:
checkvintf E 02-16 17:51:45 2215869 2215869 check_vintf.cpp:620] 1. Update deprecated HALs to the latest version.
checkvintf E 02-16 17:51:45 2215869 2215869 check_vintf.cpp:620] 2. Check for any typos in device manifest or framework compatibility matrices with FCM version >= 6.
checkvintf E 02-16 17:51:45 2215869 2215869 check_vintf.cpp:620] 3. For new platform HALs, add them to any framework compatibility matrix with FCM version >= 6 where applicable.
checkvintf E 02-16 17:51:45 2215869 2215869 check_vintf.cpp:620] 4. For device-specific HALs, add to DEVICE_FRAMEWORK_COMPATIBILITY_MATRIX_FILE or DEVICE_PRODUCT_COMPATIBILITY_MATRIX_FILE.: Success
INCOMPATIBLE
17:51:47 ninja failed with: exit status 1

#### failed to build some targets (02:14 (mm:ss)) ####

Build android failed!
```



![image-20250217093234812](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502170932106.png)



![image-20250217093747031](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502170937581.png)

![image-20250217095354864](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502170953186.png)





--------

```
filegroup {
    name: "libril-modem-lib-manifests",
    srcs: [
        "android.hardware.radio@1.6.xml",
        "android.hardware.radio.config@1.3.xml",
    ],
}



libril-modem-lib

libcuttlefish-ril-2
	- libril-modem-lib
	
libcuttlefish-rild
	- libril-modem-lib
	- libril-modem-lib-manifests
	- rild_cuttlefish.rc
```



```
vendor/ntimespace/etc/security/authorized_keys
vendor/ntimespace/commands
```

































10

```makefile
# ril
PRODUCT_PACKAGES += \
        rild \
        libspace-reference-ril \
        android.hardware.radio@1.0 \
        android.hardware.radio.deprecated@1.0.so \
        android.hardware.radio.config@1.0 \
        android.hardware.radio.config@1.0-service

PRODUCT_PROPERTY_OVERRIDES += \
        rild.libpath=/vendor/lib64/libspace-reference-ril.so \
        vendor.rild.libpath=/vendor/lib64/libspace-reference-ril.so

PRODUCT_PROPERTY_OVERRIDES += \
        ro.boot.noril=false \
        ro.telephony.default_network=22

PRODUCT_COPY_FILES += \
        $(LOCAL_PATH)/configs/default_radio.conf:system/etc/default_radio.conf
        
hardware/ril/rild/Android.mk:33:LOCAL_INIT_RC := rild.rc
        
====================================================================================


libril------------------------hardware/ril/libril/Android.mk
    ril.cpp \
    ril_event.cpp\
    RilSapSocket.cpp \
    ril_service.cpp \
    sap_service.cpp
    
    liblog \
    libutils \
    libcutils \
    libhardware_legacy \
    librilutils \
    android.hardware.radio@1.0 \
    android.hardware.radio@1.1 \
    libhidlbase \
    
    libprotobuf-c-nano-enable_malloc-32bit \


librilutils-------------------hardware/ril/librilutils/Android.bp
        "librilutils.c",
        "record_stream.c",
        "proto/sap-api.proto",


libreference-ril--------------hardware/ril/reference-ril/Android.mk
    reference-ril.c \
    atchannel.c \
    misc.c \
    at_tok.c
    
    liblog libcutils libutils libril librilutils libbase 

rild--------------------------hardware/ril/rild/Android.mk
	rild.c
	
	libcutils \
	libdl \
	liblog \
	libril
	librilutils
	
	
---------------------------------------------------------------------------------------------------
总结
rild
	-libril
	-librilutils
libreference-ril
	-libril
	-librilutils
	
    android.hardware.radio@1.0 \
    android.hardware.radio.deprecated@1.0.so \
    android.hardware.radio.config@1.0 \
    android.hardware.radio.config@1.0-service
	
```



12

```makefile
PRODUCT_PACKAGES += \
    libcuttlefish-ril-2 \
    libcuttlefish-rild
    
=============================================================
libril-modem-lib---------------------------------hardware/ntimespace/ril/reference-libril/Android.bp
        "ril.cpp",
        "RilSapSocket.cpp",
        "ril_config.cpp",
        "ril_event.cpp",
        "ril_service.cpp",
        "sap_service.cpp",
        
        "android.hardware.radio@1.0",
        "android.hardware.radio@1.1",
        "android.hardware.radio@1.2",
        "android.hardware.radio@1.3",
        "android.hardware.radio@1.4",
        "android.hardware.radio@1.5",
        "android.hardware.radio@1.6",
        "android.hardware.radio.config@1.0",
        "android.hardware.radio.config@1.1",
        "android.hardware.radio.config@1.2",
        "android.hardware.radio.config@1.3",
        "android.hardware.radio.deprecated@1.0",
        "libcutils",
        "libhardware_legacy",
        "libhidlbase",
        "liblog",
        "librilutils",
        "libutils",
        
        "libprotobuf-c-nano-enable_malloc"
name: "libril-modem-lib-manifests",
        "android.hardware.radio@1.6.xml",
        "android.hardware.radio.config@1.3.xml",
        
libcuttlefish-ril-2----------------------------hardware/ntimespace/ril/reference-ril/Android.bp
        "atchannel.c",
        "at_tok.c",
        "base64util.cpp",
        "misc.c",
        "config.c",
        "reference-ril.c",
        
        "libbase",
        "libcutils",
        "libcuttlefish_fs",
        "libcuttlefish_utils",
        "liblog",
        "librilutils",
        "libril-modem-lib",
        "libutils",

        "libqemu_pipe",
libcuttlefish-rild----------------------------hardware/ntimespace/rild/Android.bp
        "rild_cuttlefish.c",
        
        "libcutils",
        "libdl",
        "liblog",
        "libril-modem-lib",

init_rc: ["rild_cuttlefish.rc"],
 overrides: ["rild"],
 vintf_fragments: [":libril-modem-lib-manifests"],
 

---------------------------------------------------------------------------------------------------
总结
libcuttlefish-ril-2
	-libcutils
	-libril-modem-lib
libcuttlefish-rild
	-libril-modem-lib
```



[Android RIL结构分析与移植(1)_android 替换ril-CSDN博客](https://blog.csdn.net/seucbh84/article/details/13015487)

















```
root@snowrepo:/snow/android12-rk3588/hardware/interfaces/radio/1.2/default# tree
.
|-- Android.bp
|-- Radio.cpp
|-- Radio.h
|-- Sap.cpp
|-- Sap.h
|-- android.hardware.radio@1.2-radio-service.rc
|-- android.hardware.radio@1.2-sap-service.rc
|-- radio-service.cpp
`-- sap-service.cpp

0 directories, 9 files
root@snowrepo:/snow/android12-rk3588/hardware/interfaces/radio/1.2/default# 
```

```json
package {
    // See: http://go/android-license-faq
    // A large-scale-change added 'default_applicable_licenses' to import
    // all of the 'license_kinds' from "hardware_interfaces_license"
    // to get the below license kinds:
    //   SPDX-license-identifier-Apache-2.0
    default_applicable_licenses: ["hardware_interfaces_license"],
}

cc_binary {
    name: "android.hardware.radio@1.2-radio-service",
    init_rc: ["android.hardware.radio@1.2-radio-service.rc"],
    relative_install_path: "hw",
    vendor: true,
    srcs: [
        "Radio.cpp",
        "radio-service.cpp",
    ],
    shared_libs: [
        "libhidlbase",
        "liblog",
        "libutils",
        "android.hardware.radio@1.2",
        "android.hardware.radio@1.0",
        "android.hardware.radio@1.1",
    ],
}

cc_binary {
    name: "android.hardware.radio@1.2-sap-service",
    init_rc: ["android.hardware.radio@1.2-sap-service.rc"],
    relative_install_path: "hw",
    vendor: true,
    srcs: [
        "Sap.cpp",
        "sap-service.cpp",
    ],
    shared_libs: [
        "libhidlbase",
        "liblog",
        "libutils",
        "android.hardware.radio@1.2",
        "android.hardware.radio@1.0",
        "android.hardware.radio@1.1",
    ],
}

```







没有config.rc文件