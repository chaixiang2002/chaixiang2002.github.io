Google官方出场镜像

[Nexus 和 Pixel 设备的出厂映像  | Google Play services  | Google for Developers](https://developers.google.com/android/images?hl=zh-cn)

代号和细分版本号可查看以下链接

https://source.android.com/setup/start/build-numbers?hl=zh_cn

谷歌手机设备驱动下载地址

https://developers.google.com/android/drivers

---

|      | android-12.0.0_r34 | Android12 | Pixel 3、Pixel 3 XL |
| ---- | ------------------ | --------- | ------------------- |
|      |                    |           |                     |

```shell
repo init -u git://mirrors.ustc.edu.cn/aosp/platform/manifest -b android-12.0.0_r34 --depth=1
repo sync -c
repo status

网络可通的情况下下载Google和高通的驱动，https://developers.google.com/android/drivers?hl=zh-cn找对应驱动
wget https://dl.google.com/dl/android/aosp/google_devices-blueline-sp1a.210812.016.c2-47172864.tgz?hl=zh-cn
wget https://dl.google.com/dl/android/aosp/qcom-blueline-sp1a.210812.016.c2-7c544085.tgz?hl=zh-cn

./extract-qcom-crosshatch.sh   运行解压出来的脚本 并输入I ACCEPT
./extract-google_devices-blueline.sh

# 编译
. build/envsetup.sh 
lunch aosp_blueline-user
m

# 刷系统
export ANDROID_PRODUCT_OUT=/snow/android-12.0.0_r34/out/target/product/blueline
adb devices
adb reboot bootloader
sleep 4

fastboot flashall -w  #在fastboot flashall -w输入结束后，如果出现“wait for any devices”，把这个pixel3设备分配给Linux系统，因为此时重启了要重新分配，此时手机会进入fastbootd模式，不要动手机，正在写入，写完或者失败会自己开机

```

[Ubuntu20.04 编译Android 10源码 并烧录源码到pixel3的避坑指南Ubuntu20.Ubuntu2 - 掘金](https://juejin.cn/post/6942379112266727455)