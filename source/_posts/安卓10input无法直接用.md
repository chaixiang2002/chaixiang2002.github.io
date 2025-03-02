但是通过adb shell input命令有效



Android10和Android12input

![image-20250208174030164](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502081740970.png)



问题原因Root用户的环境变量太少了

![image-20250210164932353](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502101649823.png)



测试问题分析的正确

```shell
#!/system/bin/sh
# Script to start "input" on the device, which has a very rudimentary
# shell.
#

# 设置环境变量
export ANDROID_DATA=/data
export RK_ADEPT_ACTIVATION_FILE=/mnt/sdcard/.adobe-digital-editions/activation.xml
export RK_ADOBE_DE_DOC_FOLDER=/mnt/sdcard/Digital\ Editions
export ADOBE_FONTS_DIR=/system/fonts/adobefonts/
export RK_ADEPT_DEVICE_TYPE=mobile
export RK_ADEPT_DEVICE_SALT_FILE=/mnt/sdcard/.adobe-digital-editions/devicesalt
export ANDROID_RUNTIME_ROOT=/apex/com.android.runtime
export ANDROID_TZDATA_ROOT=/apex/com.android.tzdata
export HOME=/
export EBOOK_PAGE_VISIBLE_NUMBER=2
export ANDROID_ASSETS=/system/app
export BOOTCLASSPATH="/apex/com.android.runtime/javalib/core-oj.jar:/apex/com.android.runtime/javalib/core-libart.jar:/apex/com.android.runtime/javalib/okhttp.jar:/apex/com.android.runtime/javalib/bouncycastle.jar:/apex/com.android.runtime/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/android.test.base.jar:/apex/com.android.conscrypt/javalib/conscrypt.jar:/apex/com.android.media/javalib/updatable-media.jar"
export ANDROID_BOOTLOGO=1
export ANDROID_STORAGE=/storage
export DOWNLOAD_CACHE=/data/cache
export LOGNAME=shell
export SYSTEMSERVERCLASSPATH="/system/framework/services.jar:/system/framework/ethernet-service.jar:/system/framework/wifi-service.jar:/system/framework/com.android.location.provider.jar"
export DEX2OATBOOTCLASSPATH="/apex/com.android.runtime/javalib/core-oj.jar:/apex/com.android.runtime/javalib/core-libart.jar:/apex/com.android.runtime/javalib/okhttp.jar:/apex/com.android.runtime/javalib/bouncycastle.jar:/apex/com.android.runtime/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/android.test.base.jar"
export EXTERNAL_STORAGE=/sdcard
export SHELL=/system/bin/sh
export RK_ADOBE_DE_MOBILE=1
export RK_ADEPT_DEVICE_FILE=/mnt/sdcard/.adobe-digital-editions/device.xml
export ASEC_MOUNTPOINT=/mnt/asec
export USER=shell
export PATH="/sbin:/system/sbin:/product/bin:/apex/com.android.runtime/bin:/system/bin:/system/xbin:/odm/bin:/vendor/bin:/vendor/xbin:/data/misc/overlay_misc/upper"
export ANDROID_ROOT=/system
export CURL_CA_BUNDLE=/system/etc/cacert.pem

base=/system
export CLASSPATH=$base/framework/input.jar
exec app_process $base/bin com.android.commands.input.Input "$@"
```





红手指的ROOT用户的环境变量

```shell

$ sudo whoami
root
$ sudo input
Usage: input [<source>] [-d DISPLAY_ID] <command> [<arg>...]

The sources are: 
      dpad
      keyboard
      mouse
      touchpad
      gamepad
      touchnavigation
      joystick
      touchscreen
      stylus
      trackball

-d: specify the display ID.
      (Default: -1 for key event, 0 for motion event if not specified.)
The commands and default sources are:
      text <string> (Default: touchscreen)
      keyevent [--longpress] <key code number or name> ... (Default: keyboard)
      tap <x> <y> (Default: touchscreen)
      swipe <x1> <y1> <x2> <y2> [duration(ms)] (Default: touchscreen)
      draganddrop <x1> <y1> <x2> <y2> [duration(ms)] (Default: touchscreen)
      press (Default: trackball)
      roll <dx> <dy> (Default: trackball)
      event <DOWN|UP|MOVE> <x> <y> (Default: touchscreen)
$ sudo env
_=/system/bin/env
ANDROID_DATA=/data
CURL_CA_BUNDLE=/system/etc/cacert.pem
HOME=/
DEX2OATBOOTCLASSPATH=/apex/com.android.runtime/javalib/core-oj.jar:/apex/com.android.runtime/javalib/core-libart.jar:/apex/com.android.runtime/javalib/okhttp.jar:/apex/com.android.runtime/javalib/bouncycastle.jar:/apex/com.android.runtime/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/android.test.base.jar
ANDROID_RUNTIME_ROOT=/apex/com.android.runtime
ANDROID_TZDATA_ROOT=/apex/com.android.tzdata
EXTERNAL_STORAGE=/sdcard
ANDROID_ROOT=/system
ANDROID_BOOTLOGO=1
ANDROID_ASSETS=/system/app
SHELL=/system/bin/sh
BOOTCLASSPATH=/apex/com.android.runtime/javalib/core-oj.jar:/apex/com.android.runtime/javalib/core-libart.jar:/apex/com.android.runtime/javalib/okhttp.jar:/apex/com.android.runtime/javalib/bouncycastle.jar:/apex/com.android.runtime/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/android.test.base.jar:/apex/com.android.conscrypt/javalib/conscrypt.jar:/apex/com.android.media/javalib/updatable-media.jar
ANDROID_STORAGE=/storage
PATH=/sbin:/system/sbin:/product/bin:/apex/com.android.runtime/bin:/system/bin:/system/xbin:/odm/bin:/vendor/bin:/vendor/xbin:/data/.mci/
SYSTEMSERVERCLASSPATH=/system/framework/services.jar:/system/framework/ethernet-service.jar:/system/framework/wifi-service.jar:/system/framework/com.android.location.provider.jar
ASEC_MOUNTPOINT=/mnt/asec
DOWNLOAD_CACHE=/data/cache
```

