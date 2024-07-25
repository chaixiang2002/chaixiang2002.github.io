### 一、测试redrod-wifi



1. 发现rederoid-rockchip项目支持虚拟wifi

2. 要求内核支持mac80211_hwsim和切换iptables-legacy

3. 要求docker pull iceblacktea/redroid-arm64:12.0.0-240328 ->引出docker使用clash代理

   [docker用linux的clash加速 - chaixiang的个人博客](http://124.71.45.252:8090/archives/1720684412117)

```
 dd if=./boot_MAC80211_HWSIM.img of=/dev/disk/by-partlabel/boot
 
 update-alternatives --set iptables /usr/sbin/iptables-legacy
 update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
 
 reboot
 
docker run -itd --privileged \
    --name redroid \
    -v /snow/redroid_data/rd_e:/data \
    -v /dev/mali0:/dev/mali0 \
    -p 5555:5555 \
    iceblacktea/redroid-arm64:12.0.0-240328 \
    androidboot.redroid_gpu_mode=mali \
    androidboot.redroid_virtual_wifi=1
```

### 二、尝试集成redroid-rockchip的wifi到rk

```
https://github.com/redroid-rockchip/vendor_redroid_ext.git

https://github.com/redroid-rockchip/device_redroid.git
```

![image-20240711203626579](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407112036988.png)

在device里引入vendor



报错1：

![image-20240711203745068](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407112037219.png)

![image-20240711203805537](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407112038922.png)





报错2：

![image-20240711204301047](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407112043486.png)

![image-20240711204313670](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407112043781.png)



报错3：

![image-20240711205230044](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407112052685.png)

这个错误信息表示在构建Android系统时，Makefile遇到了问题。具体来说，`build/make/core/Makefile:28`和`build/make/core/base_rules.mk:482`中都定义了同一个目标`out/target/product/rk3588_docker/vendor/etc/wifi/wpa_supplicant.conf`，这导致了冲突。

在Makefile中，如果一个目标被定义了多次，那么只有最后一次定义的命令会被执行。但是，如果使用了双冒号规则（`::`）来定义目标，那么每个定义都会被执行。在这种情况下，如果试图在一个使用了单冒号规则（`:`）的目标上再次定义命令，就会出现你看到的错误。

![image-20240711210916936](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407112109704.png)

解决这个问题的方法通常是**找到并删除或修改重复的目标定义**。你需要检查你的`Makefile`和`base_rules.mk`，看看为什么会有重复的目标定义，并进行相应的修改。

```
# build/make/core/Makefile:28:

product_copy_files_ignored :=
$(foreach cf,$(unique_product_copy_files_pairs), \
    $(eval _src := $(call word-colon,1,$(cf))) \
    $(eval _dest := $(call word-colon,2,$(cf))) \
    $(call check-product-copy-files,$(cf),$(_dest)) \
    $(if $(filter $(unique_product_copy_files_destinations),$(_dest)), \
        $(eval product_copy_files_ignored += $(cf)), \
        $(eval _fulldest := $(call append-path,$(PRODUCT_OUT),$(_dest))) \
        $(if $(filter %.xml,$(_dest)),\
            $(eval $(call copy-xml-file-checked,$(_src),$(_fulldest))),\
            $(if $(and $(filter %.jar,$(_dest)),$(filter $(basename $(notdir $(_dest))),$(PRODUCT_LOADED_BY_PRIVILEGED_MODULES))),\
                $(eval $(call copy-and-uncompress-dexs,$(_src),$(_fulldest))), \
                $(if $(filter init%rc,$(notdir $(_dest)))$(filter %/etc/init,$(dir $(_dest))),\
                    $(eval $(call copy-init-script-file-checked,$(_src),$(_fulldest))),\
                    $(eval $(call copy-one-file,$(_src),$(_fulldest)))))) \
        $(eval unique_product_copy_files_destinations += $(_dest))))
```

1. `build/make/core/Makefile:28`的代码是用来处理产品复制文件的。这段代码遍历所有的产品复制文件对（`unique_product_copy_files_pairs`），检查每个文件对是否已经存在于目标位置。如果文件对的目标位置已经存在于`unique_product_copy_files_destinations`列表中，那么这个文件对就会被添加到`product_copy_files_ignored`列表中。否则，这个文件对的源文件就会被复制到目标位置，并且目标位置会被添加到`unique_product_copy_files_destinations`列表中。这段代码还处理了一些特殊情况，比如目标文件是XML文件、JAR文件或者init脚本文件。



```
# build/make/core/base_rules.mk:482

ifneq (true,$(LOCAL_UNINSTALLABLE_MODULE))
ifneq ($(LOCAL_INSTALLED_MODULE),$(my_default_test_module))
$(LOCAL_INSTALLED_MODULE): PRIVATE_POST_INSTALL_CMD := $(LOCAL_POST_INSTALL_CMD)
$(LOCAL_INSTALLED_MODULE): $(LOCAL_BUILT_MODULE)
	@echo "Install: $@"
	$(copy-file-to-new-target)
	$(PRIVATE_POST_INSTALL_CMD)
endif
```

1. `build/make/core/base_rules.mk:482`的代码是用来处理模块安装的。这段代码首先检查模块是否可以被卸载，如果可以，那么就不会执行安装命令。然后，这段代码检查模块是否是默认的测试模块，如果是，那么也不会执行安装命令。如果模块既不可以被卸载，也不是默认的测试模块，那么这段代码就会执行安装命令，将构建好的模块复制到安装位置，并执行后安装命令（`POST_INSTALL_CMD`）。

androidboot.redroid_virtual_wifi=1 ?

external/wpa_supplicant_8

![image-20240712174808415](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407121748574.png)



### 第1次尝试运行

![image-20240712200947395](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407122009704.png)

![image-20240712201007373](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407122010558.png)



查找原因
![image-20240712201057513](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407122010630.png)







## wpa_supplicant

wpa_supplicant	服务端

wpa_cli					客户端

```
wpa_cli -i wlan0 -p /data/misc/wifi/sockets/
-i指的是网卡接口
-p值得是wap_supplicant.conf所在的路径
```

[Android wifi探究一：初步认识wpa_supplicant与wifi框架梳理 - 消费电子 - SuperIC社区_ - Powered by Discuz!](https://bbs.superic.com/forum.php?mod=viewthread&tid=4847)

/vendor/bin/wpa_cli

![image-20240715164039428](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202407151640825.png)







## 所有wifi相关的模块

这些模块名（如`createns2`、`dhcpclient2`、`libdhcpclient2`、`execns2`、`create_radios2`、`wpa_supplicant`、`hostapd`）大部分是与网络功能相关的模块，尤其是在Android系统和嵌入式系统中，它们通常用于网络连接和管理。下面是它们的详细解释及可能的关系：

### 1. `createns2`
- **描述**：`createns2`可能是一个创建网络命名空间（network namespace）的模块或工具。网络命名空间是Linux内核的一项功能，允许隔离网络栈（网络设备、IP地址、路由表等）。
- **用途**：它用于创建独立的网络环境，可以在其中运行应用程序，使其网络流量与主机的其余部分隔离开来。

### 2. `dhcpclient2`
- **描述**：`dhcpclient2`是一个DHCP客户端模块。
- **用途**：DHCP（Dynamic Host Configuration Protocol）客户端用于向DHCP服务器请求动态分配的IP地址和其他网络配置参数（如网关和DNS服务器）。

### 3. `libdhcpclient2`
- **描述**：`libdhcpclient2`可能是`dhcpclient2`的一个库文件。
- **用途**：提供DHCP客户端功能的库，可以被其他应用程序或服务调用，以实现动态IP地址配置。

### 4. `execns2`
- **描述**：`execns2`可能是一个用于在指定的网络命名空间中执行命令或应用程序的工具。
- **用途**：类似于Linux中的`ip netns exec`命令，用于在特定的网络命名空间中运行进程。

### 5. `create_radios2`
- **描述**：`create_radios2`可能是一个与无线电（WiFi、蓝牙等）相关的模块或工具，用于配置或创建无线电设备。
- **用途**：用于配置无线网络接口或创建虚拟无线网络环境。

### 6. `wpa_supplicant`
- **描述**：`wpa_supplicant`是一个广泛使用的WiFi客户端应用程序。
- **用途**：用于管理无线网络连接，支持WPA和WPA2加密。它可以处理WiFi的扫描、连接、认证等工作。
- **关系**：`wpa_supplicant`通常与网络命名空间和DHCP客户端配合使用。例如，在一个独立的网络命名空间中运行`wpa_supplicant`，然后使用`dhcpclient2`获取IP地址。

### 7. `hostapd`
- **描述**：`hostapd`是一个用于设置WiFi热点（AP，Access Point）的守护进程。
- **用途**：使设备能够充当无线接入点，提供WiFi连接给其他设备。支持WPA/WPA2加密。
- **关系**：`hostapd`与`wpa_supplicant`的功能互补。`wpa_supplicant`是客户端，`hostapd`是服务端。两者可以分别用于不同的设备或同一设备的不同网络接口，以实现完整的WiFi网络管理。

### 总结
这些模块主要涉及到网络管理和无线连接配置。在一个典型的嵌入式系统或Android系统中，它们可能这样协作：

- **命名空间管理**：使用`createns2`创建一个独立的网络命名空间。
- **执行命令**：使用`execns2`在该命名空间中运行命令。
- **无线网络连接**：在命名空间中运行`wpa_supplicant`以管理WiFi连接。
- **DHCP**：使用`dhcpclient2`获取动态IP地址。
- **库文件**：`libdhcpclient2`提供给其他应用程序使用的DHCP功能。
- **无线电配置**：`create_radios2`用于配置无线网络接口。
- **无线接入点**：`hostapd`设置无线接入点，使其他设备能够连接。

通过这些模块，系统可以实现灵活和强大的网络配置和管理能力。