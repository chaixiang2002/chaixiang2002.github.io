查询方法
dumpsys connectivity | grep -E 'DNS|Dns'



----

device/rockchip/rk3588/rk3588_docker_overseas/init.redroid.rc

vendor/rockchip/common/docker_android/ipconfigstore

device/rockchip/rk3588/rk3588_docker/rk3588_docker.mk

```makefile
# redorid add
PRODUCT_PACKAGES += \
	binder_alloc \
	ipconfigstore \

PRODUCT_PACKAGES += \
	camera.$(TARGET_BOARD_HARDWARE) \
	camera.device@1.0-impl \
	camera.device@3.2-impl \
	android.hardware.camera.provider@2.4-impl \
	android.hardware.camera.provider@2.4-service

PRODUCT_COPY_FILES += \
	$(LOCAL_PATH)/init.redroid.rc:$(TARGET_COPY_OUT_VENDOR)/etc/init/init.redroid.rc \
	$(LOCAL_PATH)/chmod.sh:$(TARGET_COPY_OUT_VENDOR)/bin/chmod.sh \
	$(LOCAL_PATH)/fstab.rk30board:$(TARGET_COPY_OUT_VENDOR)/etc/fstab.rk30board \
	$(LOCAL_PATH)/host_network.sh:$(TARGET_COPY_OUT_VENDOR)/bin/host_network.sh \
	$(LOCAL_PATH)/console:$(TARGET_COPY_OUT_SYSTEM)/bin/console \

# redorid add end
```

device/rockchip/rk3588/rk3588_docker/init.redroid.rc

device/rockchip/rk3588/rk3588_docker/chmod.sh                       设置各个设备文件权限

device/rockchip/rk3588/rk3588_docker/fstab.rk30board

device/rockchip/rk3588/rk3588_docker/host_network.sh

device/rockchip/rk3588/rk3588_docker/console                          设置环境变量

----

目前现状：

rk3588:RK_ANDROID10-RKR14-20241217-guozhen镜像有效值

ro.boot.redroid_net_ndns=2

ro.boot.redroid_net_dns1=218.30.118.6

ro.boot.redroid_net_dns2=123.125.81.6



无效值：

ro.container.net_dns.num=2

ro.container.net_dns1=223.5.5.5

ro.container.net_dns2=223.6.6.6

----

最终解决方法：
cp -r vendor/ntimespace/ipconfigstore