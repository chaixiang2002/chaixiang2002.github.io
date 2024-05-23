[Magisk安装教程 - Magisk中文网 (magiskcn.com)](https://magiskcn.com/)


3、提取 **boot.img** ：[payload-dumper-go-boot](https://magiskcn.com/payload-dumper-go-boot)（如果系统包有  **boot.img** ，可以跳过此步骤）E:\snow\project\magisk\update

4、手机插电脑，文件传输模式，复制 **boot.img** 到手机 **Download** 目录

5、手机下载 **Magisk** APP 安装：[Magisk-download](https://magiskcn.com/magisk-download)

6、打开Magisk，①：安装 – ②：选择 boot.img – ③：开始修补文件 – ④：修补完成（修补生成 magisk_patched-xxx.img 文件在 Download 目录）



Root方法：

```
./adb -s 852HLDTN23VAE shell
M1852:/ $ su
```

屏幕上点击授权


/vendor/build.prop
/vendor/default.prop
/vendor/package/CTA/system/vendor/vendor.prop
/vendor/package/ChinaMobile/system/vendor/vendor.prop
/vendor/package/ChinaTelecom/system/vendor/vendor.prop
/vendor/package/ChinaUnicom/system/vendor/vendor.prop
/vendor/package/Default/system/build.prop
/vendor/package/Default/system/vendor/default.prop
/vendor/package/EUCommon/system/vendor/vendor.prop
/vendor/package/TelefonicaGermany/system/vendor/vendor.prop
/vendor/package/VodafoneGroup/system/vendor/vendor.prop
/vendor/package/VodafoneUK/system/vendor/vendor.prop
/vendor/package/default.prop
/system/build.prop

/persist/speccfg/vendor_persist.prop
/persist/speccfg/vendor_ro.prop
/default.prop
