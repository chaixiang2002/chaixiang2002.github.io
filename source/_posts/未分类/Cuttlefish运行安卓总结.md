- [安卓逆向环境指北 rk3588 orangepi5b macM1 cuttlefish redroid - FW_ltlly - 博客园 (cnblogs.com)](https://www.cnblogs.com/FW-ltlly/p/18014692)
- [开始使用  |  Android 开源项目  |  Android Open Source Project](https://source.android.com/docs/devices/cuttlefish/get-started?hl=zh-cn)


1. 查看系统内核是否支持kvm和虚拟化

```
grep -c -w "vmx\|svm"/proc/cpuinfo	#宿主机x86
find /dev -name kvm			#宿主机arm
```


## 启动 Cuttlefish


```
sudo apt install -y git devscripts equivs config-package-dev debhelper-compat golang curl
git clone https://github.com/google/android-cuttlefish
cd android-cuttlefish
for dir inbase frontend;do
  pushd $dir
  # Install build dependencies
  sudo mk-build-deps -i
  dpkg-buildpackage -uc -us
  popd
done
sudo dpkg -i ./cuttlefish-base_*_*64.deb|| sudo apt-get install -f
sudo dpkg -i ./cuttlefish-user_*_*64.deb|| sudo apt-get install -f
sudo usermod -aG kvm,cvdnetwork,render $USER
sudo reboot
```


```
这里面有go语言环境的坑，修改以下配置 (有网络报错就执行这一步代理，没有就不用)

vim android-cuttlefish/frontend/src/goutil

# 将下面这一行注释掉，添加后面的两行
# export GOPROXY="proxy.golang.org|proxy.golang.org|direct"
export GO111MODULE=on
export GOPROXY=https://goproxy.io
```

## 下载构件

[aosp-main-throttled | Branch Grid (android.com)](https://ci.android.com/builds/branches/aosp-main-throttled/grid?legacy=1)

[Artifacts (android.com)](https://ci.android.com/builds/submitted/11693997/aosp_cf_arm64_only_phone-trunk_staging-userdebug/latest)

**提示** ：对于 ARM，请使用分支 `aosp-main-throttled` 和设备目标 `aosp_cf_arm64_only_phone-trunk_staging-userdebug`。

aosp_cf_x86_64_phone-img-xxxxxx.zip

cvd-host_package.tar.gz

## 解压运行

```
mkdir cf
cd cf
tar -xvf /path/to/cvd-host_package.tar.gz
unzip /path/to/aosp_cf_x86_64_phone-img-.zip
```


## Cuttlefish！ 启动！

```
HOME=$PWD ./bin/launch_cvd --daemon		#普通
HOME=$PWD ./bin/launch_cvd --start_webrtc 	#网络webtrc
```

webrtc启动，可以访问**https://宿主机ip:8443**


## 停止 Cuttlefish


```
HOME=$PWD ./bin/stop_cvd
```


## 默认adb端口


```
.\adb.exe connect 192.168.30.165:6520
List of devices attached
127.0.0.1:6520  device
127.0.0.1:6521  device
127.0.0.1:6522  device
127.0.0.1:6523  device
127.0.0.1:6524  device
127.0.0.1:6525  device
127.0.0.1:6526  device
127.0.0.1:6527  device
```


## 启动多租户 Cuttlefish 实例


```
launch_cvd --num_instances=8 --daemon
```
