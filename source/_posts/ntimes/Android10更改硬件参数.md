# 2种方法

本人了解到修改更改硬件参数方法有两种

1. 通过修改aosp的frameworks层的源码，在返回硬件参数时拦截返回值，通过替换的方式，欺骗软件
2. 通过修改安卓容器的4个prop文件，修改硬件参数。

方法一：好处是更改参数不会因为与真实参数不同而导致系统出错的风险，仅仅是欺骗java层以上的应用，坏处是不能动态集群式批量修改，每次修改需要重新编译镜像

方法二：可以动态批量给所有容器修改，并且每次修改仅需要重启就可生效。缺点，部分参数修改的与真实参数不一样会导致系统错误。

## 可修改的参数

### busybox vi /product/build.prop

品牌brand：     ro.product.product.brand=Redmi

设备Device：  ro.product.product.device=alioth

Manufacturer:  ro.product.product.manufacturer=Xiaomi

Model:        ro.product.product.model=M2012K11AC

Product:       [ro.product.product.name](http://ro.product.product.name)=alioth
指纹fingerprint 由brand+Device+ Product+安卓版本+ Build ID +Incremental+ Build Type+ Build Tags

![](http://wiki.ntimespace.com/download/attachments/13599974/image2024-2-1_17-56-54.png?version=1&modificationDate=1706781414818&api=v2 "软件研发中心 &gt; Android10更改硬件参数 &gt; image2024-2-1_17-56-54.png")

### busybox vi /system/build.prop

buildID：      [ro.build.id](http://ro.build.id)=SKQ1.211209.001

incremental： ro.build.version.incremental=22.2.7

security ：    ro.build.version.security_patch=2021-01-01

build.type：  ro.build.type=user1

builer_user：     ro.build.user=builder

builer_host：     ro.build.host=[m1-xm-ota-bd244.bj.idc.xiaomi.com](http://m1-xm-ota-bd244.bj.idc.xiaomi.com)

builer_tags           ro.build.tags=release-keys1

description： ro.build.description=alioth-user 12 SKQ1.211209.001 22.2.7 release-keys

![](http://wiki.ntimespace.com/download/attachments/13599974/image2024-2-1_17-57-7.png?version=1&modificationDate=1706781427887&api=v2 "软件研发中心 &gt; Android10更改硬件参数 &gt; image2024-2-1_17-57-7.png")

### busybox vi /vendor/build.prop

Board·：  ro.product.board=kona

 ![](http://wiki.ntimespace.com/download/thumbnails/13599974/image2024-2-1_17-57-16.png?version=1&modificationDate=1706781436267&api=v2 "软件研发中心 &gt; Android10更改硬件参数 &gt; image2024-2-1_17-57-16.png")

## 修改会出错误的参数

/product/build.prop

ro.build.version.sdk=29

ro.build.version.release=10

后果：大多数应用打开后异常未响应或退出

/vendor/build.prop

ro.board.platform=rk3588

后果：连不上该容器

## 需要商议的硬件参数

1. [Android--史上最全、最完整，获取设备信息、获取手机唯一标识_android 获取设备信息-CSDN博客](https://blog.csdn.net/u013290250/article/details/118580373)
2. [z244370114/DeviceLibray: 获取Android设备详细信息 (github.com)](https://github.com/z244370114/DeviceLibray)
3. [系统属性文件 ro.hardware值-CSDN博客](https://blog.csdn.net/singledevil0/article/details/119672702)
4. [编写android HAL举例: lights_android light hal-CSDN博客](https://blog.csdn.net/manshq163com/article/details/17318871?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-17318871-blog-82541732.235%5Ev43%5Epc_blog_bottom_relevance_base7&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-17318871-blog-82541732.235%5Ev43%5Epc_blog_bottom_relevance_base7&utm_relevant_index=2)
5. [Android硬件抽象Hardware库加载过程源码分析-CSDN博客](https://blog.csdn.net/iteye_13202/article/details/82541732?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-82541732-blog-119672702.235%5Ev43%5Epc_blog_bottom_relevance_base7&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-82541732-blog-119672702.235%5Ev43%5Epc_blog_bottom_relevance_base7&utm_relevant_index=5)
6. [深入讲解Android Property机制-CSDN博客](https://blog.csdn.net/stoic163/article/details/88815430)
7. [自定义的诱惑：教你修改build.prop的常用配置-迅维网—维修资讯 (chinafix.com)](https://www.chinafix.com/article-7622-1.html)

### Android ID：

* 它在首次设备启动时随机生成，并在设备恢复出厂设置时更改
* 这部分代码通常位于java文件中
* Android ID会被存储在设备的系统设置中，具体来说，它被存储在设备的SQLite数据库中，该数据库位于/data/data/com.android.providers.settings/databases/settings.db
* [应用程序通常会使用Android API来获取Android ID，例如Secure.getString(context.getContentResolver(), Settings.Secure.ANDROID_ID)](https://blog.csdn.net/u013290250/article/details/118580373)[^1^](https://blog.csdn.net/u013290250/article/details/118580373)

解决方法

![](http://wiki.ntimespace.com/download/attachments/13599974/image2024-2-1_17-57-50.png?version=1&modificationDate=1706781470766&api=v2 "软件研发中心 &gt; Android10更改硬件参数 &gt; image2024-2-1_17-57-50.png")

### ro.board.platform：

暂时没有能力修改

直接修改/vendor/build.prop的这个值会导致无法连接容器

然而因为ro.board.platform这个属性在Android系统的其他部分被使用，而这些部分可能没有使用SystemProperties.get()方法来获取它的值
无法从java层拦截替换

### ro.hardware：

![](http://wiki.ntimespace.com/download/attachments/13599974/image2024-2-1_17-58-1.png?version=1&modificationDate=1706781481846&api=v2 "软件研发中心 &gt; Android10更改硬件参数 &gt; image2024-2-1_17-58-1.png")

最终结果

![](http://wiki.ntimespace.com/download/attachments/13599974/image2024-2-1_17-58-24.png?version=1&modificationDate=1706781504654&api=v2 "软件研发中心 &gt; Android10更改硬件参数 &gt; image2024-2-1_17-58-24.png")

### serialno

ro.boot.serialno=dfdfa66f

ro.serialno=dfdfa66f

直接加进去system/build.prop

### model

ro.product.model和ro.product product.model会相互覆盖

# 6个prop文件的解释

./default.prop

./system/build.prop

./vendor/default.prop

./vendor/build.prop

./odm/etc/build.prop

./product/build.prop

1. [**./default.prop**](https://www.cnblogs.com/Tesi1a/p/7624059.html)[^1^](https://www.cnblogs.com/Tesi1a/p/7624059.html)[^2^](https://cloud.tencent.com/developer/article/2252343)[^3^](https://blog.csdn.net/u012041204/article/details/78942370): 这个文件通常位于Android系统的根目录下。它包含了一些默认的系统属性，这些属性主要控制着一些安全性的设置，例如是否可以用adb来进行调试。这个文件在系统启动后就会被加载，但是它的内容在重启后会恢复到原始状态，因为它是在boot.img中的。
2. [**./system/build.prop**](https://www.jianshu.com/p/098b8809d85d)[^4^](https://www.jianshu.com/p/098b8809d85d)[^5^](https://blog.csdn.net/shenfengchen/article/details/115482371): 这个文件是Android系统中的一个重要的属性文件，记录了系统的设置和改变。它包含了很多类型的信息，如编译信息（ro.build. *），设备信息（ro.product.* ），默认设置信息（ro.config. *），虚拟机信息（dalvik.vm.* ）等。
3. [**./vendor/default.prop**](https://www.cnblogs.com/Tesi1a/p/7624059.html)[^1^](https://www.cnblogs.com/Tesi1a/p/7624059.html)[^6^](https://devpress.csdn.net/v1/article/detail/116591430)[^7^](https://blog.csdn.net/qq_32072451/article/details/88740458): 这个文件和./default.prop类似，也是包含了一些默认的系统属性。这些属性是在编译脚本中生成的，通常控制着一些安全性的设置。
4. [**./vendor/build.prop**](https://blog.csdn.net/a546036242/article/details/119182420)[^8^](https://blog.csdn.net/a546036242/article/details/119182420)[^4^](https://www.jianshu.com/p/098b8809d85d): 这个文件和./system/build.prop类似，也是记录了系统的设置和改变。不过，从Android 9.0开始，Google推荐将厂家定制的属性添加到这个文件中，而不是./system/build.prop。
5. [**./odm/etc/build.prop**](https://source.android.google.cn/docs/core/architecture/bootloader/partitions/odm-partitions?hl=zh-cn)[^9^](https://source.android.google.cn/docs/core/architecture/bootloader/partitions/odm-partitions?hl=zh-cn): 这个文件位于ODM（Original Design Manufacturer，原始设计制造商）分区中，包含了ODM专用的组件和属性。这些属性可以让ODM为他们的特定设备自定义系统芯片（SoC）供应商的板级支持包（BSP）。
6. [**./product/build.prop**](https://www.cnblogs.com/pngcui/p/7193622.html)[^10^](https://www.cnblogs.com/pngcui/p/7193622.html)[^11^](https://blog.csdn.net/varistor/article/details/8822143)[^12^](https://blog.csdn.net/thl789/article/details/7014300): 这个文件位于product分区中，用于存储与特定产品相关的属性。从Android 9开始，Google引入了product分区，使得可以为不同的软件SKU使用同一个系统映像。

在Android系统中，以下的prop文件在**重启后会恢复**到原始状态：

* **./default.prop**
* **./vendor/default.prop**

这是因为这些文件是在boot.img中的，所以在系统启动后就会被加载，但是它的内容在重启后会恢复到原始状态。

而以下的prop文件在 **修改后会一直保存** ，即使重启也不会恢复到原始状态：

* **./system/build.prop**
* **./vendor/build.prop**
* **./odm/etc/build.prop**
* **./product/build.prop**

这是因为这些文件是在各自的分区中的，所以在系统启动后就会被加载，而且它的内容在重启后不会恢复到原始状态，除非进行了恢复出厂设置或者刷机等操作。

### /default.prop

* 这个文件通常位于Android系统的根目录下。它包含了一些默认的系统属性，这些属性主要控制着一些安全性的设置，例如是否可以用adb来进行调试。这个文件在系统启动后就会被加载，但是它的内容在重启后会恢复到原始状态，因为它是在img中的。

ro.debuggable=0：这是系统的调试开关。如果ro.debuggable为0，那么系统将不会开启调试模式12。

debug.atrace.tags.enableflags=0：这是用于启用跟踪功能的标志34。

dalvik.vm.image-dex2oat-Xms=64m和dalvik.vm.image-dex2oat-Xmx=64m：这两个参数是用来设置ART运行时在进行dex到oat转换时的初始堆大小和最大堆大小567。

dalvik.vm.dex2oat-Xms=64m和dalvik.vm.dex2oat-Xmx=512m：这两个参数是用来设置ART运行时在进行dex到oat转换时的初始堆大小和最大堆大小8567910。

dalvik.vm.usejit=true：这是用来启用或禁用JIT编译的开关1112。

dalvik.vm.usejitprofiles=true：这是用来启用或禁用JIT配置文件的开关512。

dalvik.vm.dexopt.secondary=true：这个参数的具体含义我没有找到相关的信息，可能是用于优化Dalvik虚拟机的某些设置1314。

dalvik.vm.appimageformat=lz4：这个参数可能是用来设置应用镜像的格式515。

ro.dalvik.vm.native.bridge=0：这个参数的具体含义我没有找到相关的信息，可能是用于设置Dalvik虚拟机的某些设置。

pm.dexopt.first-boot=quicken，pm.dexopt.boot=verify，pm.dexopt.install=speed-profile，[pm.dexopt.bg](http://pm.dexopt.bg)-dexopt=speed-profile，pm.dexopt.ab-ota=speed-profile，pm.dexopt.inactive=verify，pm.dexopt.shared=speed：这些参数是用来设置不同情况下的dex到oat的编译选项5。

dalvik.vm.dex2oat-resolve-startup-strings=true，dalvik.vm.dex2oat-max-image-block-size=524288，dalvik.vm.minidebuginfo=true，dalvik.vm.dex2oat-minidebuginfo=true：这些参数是用来设置dex到oat转换的一些选项5。

ro.iorapd.enable=false：这个参数的具体含义我没有找到相关的信息。

persist.sys.usb.config=none：这个参数可能是用来设置USB的配置。

### /system/build.prop

* 这个文件是Android系统中的一个重要的属性文件，记录了系统的设置和改变。它包含了很多类型的信息，如编译信息（build. *），设备信息（ro.product.* ），默认设置信息（ro.config. *），虚拟机信息（dalvik.vm.* ）等。

**这是一个Android设备的构建属性文件，它包含了关于设备的各种信息。下面是每一行的解释：**

* **ro.system.build.date=Thu Jan 4 18:50:29 CST 2024：系统构建的日期和时间。**
* **ro.system.build.date.utc=1704365429：系统构建日期的UTC时间戳。**
* **ro.system.build.fingerprint=rockchip/rk3588_docker/rk3588_docker:10/QD4A.200805.003/root01041850:user/release-keys：系统的唯一标识，包括设备品牌、设备名称、Android版本、构建ID等信息。**
* **[ro.system.build.id](http://ro.system.build.id)=QD4A.200805.555：系统构建的ID。**
* **ro.system.build.tags=release-keys：系统构建的标签，这里的release-keys表示这是一个正式发布的版本。**
* **ro.system.build.type=root：系统构建的类型。**
* **ro.system.build.version.incremental=eng.root.20240104.185037：系统构建的增量版本号。**
* **ro.system.build.version.release=10：系统构建的发布版本，这里是Android 10。**
* **ro.system.build.version.sdk=29：系统构建的SDK版本，这里是29。**
* **ro.product.system.brand=OPPO：设备的品牌，这里是OPPO。**
* **ro.product.system.device=OPPO R9s：设备的名称，这里是OPPO R9s。**
* **ro.product.system.manufacturer=OPPO：设备的制造商，这里是OPPO。**
* **ro.product.system.model=OPPO：设备的型号，这里是OPPO。**
* **[ro.product.system.name](http://ro.product.system.name)=OPPO R9s：设备的系统名称，这里是OPPO R9s。**
* **[ro.build.id](http://ro.build.id)=QD4A.200805.555：构建的ID。**
* **[ro.build.display.id](http://ro.build.display.id)=QD4A.200805.555 release-keys：用于在屏幕上显示的构建ID。**
* **ro.build.version.incremental=eng.root.20240104.185037：构建的增量版本号。**
* **ro.build.version.sdk=29：构建的SDK版本，这里是29。**
* **ro.build.version.preview_sdk=0：预览SDK的版本，这里是0。**
* **ro.build.version.preview_sdk_fingerprint=REL：预览SDK的指纹，这里是REL。**
* **ro.build.version.codename=REL：构建的代号，这里是REL。**
* **ro.build.version.all_codenames=REL：所有的构建代号，这里是REL。**
* **ro.build.version.release=10：构建的发布版本，这里是Android 10。**
* **ro.build.version.security_patch=2021-03-05：最后安全补丁的日期。**
* **ro.build.version.base_os=：基础操作系统的版本。**
* **ro.build.version.min_supported_target_sdk=23：最小支持的目标SDK版本，这里是23。**
* **ro.build.date=Thu Jan 4 18:50:29 CST 2024：构建的日期和时间。**
* **ro.build.date.utc=1704365429：构建日期的UTC时间戳。**
* **ro.build.type=user：构建的类型，这里是user。**
* **ro.build.user=root：构建的用户，这里是root。**
* **ro.build.host=dev：构建的主机，这里是dev。**
* **ro.build.tags=release-keys：构建的标签，这里的release-keys表示这是一个正式发布的版本。**
* **ro.build.flavor=rk3588_docker-user：构建的风味，这里是rk3588_docker-user。**
* **ro.product.cpu.abi=arm64-v8a：设备的CPU ABI，这里是arm64-v8a。**
* **ro.product.cpu.abilist=arm64-v8a,armeabi-v7a,armeabi：设备支持的CPU ABI列表。**
* **ro.product.cpu.abilist32=armeabi-v7a,armeabi：设备支持的32位CPU ABI列表。**
* **ro.product.cpu.abilist64=arm64-v8a：设备支持的64位CPU ABI列表。**
* **ro.product.locale=en-US：设备的区域设置，这里是en-US。**
* **ro.wifi.channels=：设备的Wi-Fi频道。**
* **ro.build.product=OPPO：构建的产品，这里是OPPO。**
* **ro.build.description=OPPO-user 10 QD4A.200805.003 eng.root.20240104.185037 release-keys：构建的描述。**
* **ro.treble.enabled=true：是否启用了Project Treble，这里是true。**
* **[net.bt.name](http://net.bt.name)=Android：蓝牙的名称，这里是Android。**

### /odm/etc/build.prop

* 这个文件位于ODM（Original Design Manufacturer，原始设计制造商）分区中，包含了ODM专用的组件和属性。这些属性可以让ODM为他们的特定设备自定义系统芯片（SoC）供应商的板级支持包（BSP）。
* ro.odm.product.cpu.abilist=arm64-v8a,armeabi-v7a,armeabi：这个属性定义了设备支持的CPU指令集，包括arm64-v8a，armeabi-v7a和armeabi。
* ro.odm.product.cpu.abilist32=armeabi-v7a,armeabi：这个属性定义了设备支持的32位CPU指令集，包括armeabi-v7a和armeabi。
* ro.odm.product.cpu.abilist64=arm64-v8a：这个属性定义了设备支持的64位CPU指令集，即arm64-v8a。

接下来的属性是由build/make/tools/buildinfo_common.sh自动生成的常见构建属性：

* ro.odm.build.date=Wed Jan 31 11:57:55 CST 2024：这个属性表示ODM构建的日期和时间。
* ro.odm.build.date.utc=1706673475：这个属性表示ODM构建的日期和时间的UTC形式。
* ro.odm.build.fingerprint=rockchip/rk3588_docker/rk3588_docker:10/QD4A.200805.003/dev01311157:user/release-keys：这个属性表示设备的构建指纹。
* [ro.odm.build.id](http://ro.odm.build.id)=QD4A.200805.003：这个属性表示ODM构建的ID。
* ro.odm.build.tags=release-keys：这个属性表示ODM构建的标签。
* ro.odm.build.type=user：这个属性表示ODM构建的类型。
* ro.odm.build.version.incremental=eng.dev.20240131.102356：这个属性表示ODM构建的增量版本。
* ro.odm.build.version.release=10：这个属性表示ODM构建的发布版本。
* ro.odm.build.version.sdk=29：这个属性表示ODM构建的SDK版本。

接下来的属性是设备的品牌和型号信息：

* ro.product.odm.brand=rockchip：这个属性表示设备的品牌，即rockchip。
* ro.product.odm.device=rk3588_docker：这个属性表示设备的设备名，即rk3588_docker。
* ro.product.odm.manufacturer=rockchip：这个属性表示设备的制造商，即rockchip。
* ro.product.odm.model=rk3588_docker：这个属性表示设备的型号，即rk3588_docker。
* [ro.product.odm.name](http://ro.product.odm.name)=rk3588_docker：这个属性表示设备的名称，即rk3588_docker。
* 

### /product/build.prop

* 这个文件位于product分区中，用于存储与特定产品相关的属性。从Android 9开始，Google引入了product分区，使得可以为不同的软件SKU使用同一个系统映像。

ro.product.build.date=Wed Jan 31 11:57:55 CST 2024：这个属性表示产品构建的日期和时间。

ro.product.build.date.utc=1706673475：这个属性表示产品构建的日期和时间的UTC形式。

ro.product.build.fingerprint=rockchip/rk3588_docker/rk3588_docker:10/QD4A.200805.003/dev01311157:user/release-keys：这个属性表示设备的构建指纹。

[ro.product.build.id](http://ro.product.build.id)=QD4A.200805.003：这个属性表示产品构建的ID。

ro.product.build.tags=release-keys：这个属性表示产品构建的标签。

ro.product.build.type=user：这个属性表示产品构建的类型。

ro.product.build.version.incremental=eng.dev.20240131.102356：这个属性表示产品构建的增量版本12。

ro.product.build.version.release=10：这个属性表示产品构建的发布版本。

ro.product.build.version.sdk=29：这个属性表示产品构建的SDK版本。

设备的品牌和型号信息：

ro.product.product.brand=rockchip：这个属性表示设备的品牌，即rockchip。

ro.product.product.device=rk3588_docker：这个属性表示设备的设备名，即rk3588_docker。

ro.product.product.manufacturer=rockchip：这个属性表示设备的制造商，即rockchip。

ro.product.product.model=rk3588_docker：这个属性表示设备的型号，即rk3588_docker。

[ro.product.product.name](http://ro.product.product.name)=rk3588_docker：这个属性表示设备的名称，即rk3588_docker。

ro.build.characteristics=tablet这个属性表示设备的特性，即tablet

### /vendor/build.prop

* 这个文件和./system/build.prop类似，也是记录了系统的设置和改变。不过，从Android 9.0开始，Google推荐将厂家定制的属性添加到这个文件中，而不是./system/build.prop。

ro.boot.dynamic_partitions=true：这个属性表示设备是否支持动态分区12。

ro.product.first_api_level=29：这个属性表示设备首次运行的Android API级别，这里是29，即Android 1012。

ro.vendor.build.security_patch=2021-03-05：这个属性表示安全补丁的日期12。

ro.vendor.product.cpu.abilist=arm64-v8a,armeabi-v7a,armeabi：这个属性定义了设备支持的CPU指令集12。

ro.vendor.product.cpu.abilist32=armeabi-v7a,armeabi：这个属性定义了设备支持的32位CPU指令集12。

ro.vendor.product.cpu.abilist64=arm64-v8a：这个属性定义了设备支持的64位CPU指令集12。

ro.product.board=rk30sdk：这个属性表示设备的主板名称12。

ro.board.platform=rk3588：这个属性表示设备的主板平台12。

ro.hwui.use_vulkan=：这个属性表示是否使用Vulkan进行硬件UI渲染12。

接下来的属性是由build/make/tools/buildinfo_common.sh自动生成的常见构建属性12：

ro.vendor.build.date=Wed Jan 31 11:57:55 CST 2024：这个属性表示供应商构建的日期和时间12。

ro.vendor.build.date.utc=1706673475：这个属性表示供应商构建的日期和时间的UTC形式12。

ro.vendor.build.fingerprint=rockchip/rk3588_docker/rk3588_docker:10/QD4A.200805.003/dev01311157:user/release-keys：这个属性表示设备的构建指纹12。

[ro.vendor.build.id](http://ro.vendor.build.id)=QD4A.200805.003：这个属性表示供应商构建的ID12。

ro.vendor.build.tags=release-keys：这个属性表示供应商构建的标签12。

ro.vendor.build.type=user：这个属性表示供应商构建的类型12。

ro.vendor.build.version.incremental=eng.dev.20240131.102356：这个属性表示供应商构建的增量版本12。

ro.vendor.build.version.release=10：这个属性表示供应商构建的发布版本12。

ro.vendor.build.version.sdk=29：这个属性表示供应商构建的SDK版本12。

接下来的属性是设备的品牌和型号信息12：

ro.product.vendor.brand=rockchip：这个属性表示设备的品牌，即rockchip12。

ro.product.vendor.device=rk3588_docker：这个属性表示设备的设备名，即rk3588_docker12。

ro.product.vendor.manufacturer=rockchip：这个属性表示设备的制造商，即rockchip12。

ro.product.vendor.model=rk3588_docker：这个属性表示设备的型号，即rk3588_docker12。

[ro.product.vendor.name](http://ro.product.vendor.name)=rk3588_docker：这个属性表示设备的名称，即rk3588_docker12。

接下来的属性是BOOTIMAGE_BUILD_PROPERTIES12：

ro.bootimage.build.date=Wed Jan 31 11:57:55 CST 2024：这个属性表示bootimage的构建日期和时间12。

ro.bootimage.build.date.utc=1706673475：这个属性表示bootimage的构建日期和时间的UTC形式12。

ro.bootimage.build.fingerprint=rockchip/rk3588_docker/rk3588_docker:10/QD4A.200805.003/dev01311157:user/release-keys：这个属性表示bootimage的构建指纹12。

最后，以下是一些额外的供应商构建属性12：

debug.hwui.use_partial_updates=false：这个属性表示是否使用部分更新进行硬件UI渲染12。

ro.product.ota.host=192.168.1.1:8888：这个属性表示OTA更新的服务器地址12。

ro.vendor.sdkversion=rk3588_ANDROID10.0_MID_V1.0：这个属性表示供应商的SDK版本12。

vendor.gralloc.disable_afbc=0：这个属性表示是否禁用AFBC12。

ro.ril.ecclist=112,911：这个属性表示紧急呼叫的电话号码列表12。

ro.opengles.version=196610：这个属性表示OpenGL ES的版本12。

wifi.interface=wlan0：这个属性表示WiFi的接口名称12。

ro.audio.monitorOrientation=true：这个属性表示是否监视音频的方向12。

debug.nfc.fw_download=false：这个属性表示是否下载NFC固件12。

[debug.nfc.se](http://debug.nfc.se)=false：这个属性表示是否使用NFC安全元素12。

vendor.hwc.compose_policy=1：这个属性表示硬件合成策略12。

sys.wallpaper.rgb565=0：这个属性表示壁纸的颜色格式12。

sf.power.control=2073600：这个属性表示SurfaceFlinger的电源控制12。

sys.rkadb.root=0：这个属性表示是否允许ADB root访问12。

ro.sf.fakerotation=false：这个属性表示是否启用假旋转12。

ro.tether.denied=false：这个属性表示是否禁止网络共享12。

sys.resolution.changed=false：这个属性表示系统分辨率是否已更改12。

ro.default.size=100：这个属性表示默认大小12。

ro.product.usbfactory=rockchip_usb：这个属性表示USB工厂模式的产品名称12。

wifi.supplicant_scan_interval=15：这个属性表示WiFi扫描间隔12。

ro.factory.tool=0：这个属性表示工厂工具的状态12。

ro.kernel.android.checkjni=0：这个属性表示是否启用JNI检查12。

ro.build.shutdown_timeout=6：这个属性表示关机超时时间12。

persist.enable_task_snapshots=false：这个属性表示是否启用任务快照12。

ro.vendor.frameratelock=true：这个属性表示是否启用帧率锁定12。

ro.config.ringtone=Ring_Synth_04.ogg：这个属性表示默认铃声12。

ro.config.notification_sound=pixiedust.ogg：这个属性表示默认通知声音12。

ro.carrier=unknown：这个属性表示运营商12。

ro.config.alarm_alert=Oxygen.ogg：这个属性表示默认闹钟声音12。

ro.rksdk.version=RK_ANDROID10-RKR14：这个属性表示SDK版本12。

ro.boot.vr=0：这个属性表示是否启用VR模式12。

ro.hardware.egl=mali：这个属性表示EGL硬件加速器12。

persist.sys.strictmode.visual=false：这个属性表示是否启用严格模式的视觉指示12。

ro.rk.bt_enable=true：这个属性表示是否启用蓝牙12。

ro.rk.flash_enable=true：这个属性表示是否启用闪光灯12。

ro.rk.hdmi_enable=true：这个属性表示是否启用HDMI12。

ro.factory.hasUMS=false：这个属性表示设备是否支持USB大容量存储12。

testing.mediascanner.skiplist=/mnt/shell/emulated/Android/：这个属性表示媒体扫描器的跳过列表12。

ro.factory.hasGPS=false：这个属性表示设备是否有GPS12。

ro.vendor.ethernet_settings=true：这个属性表示是否启用以太网设置12。

ro.factory.storage_suppntfs=true：这个属性表示存储是否支持NTFS12。

ro.factory.without_battery=false：这个属性表示设备是否有电池12。

persist.bluetooth.btsnoopenable=false：这个属性表示是否启用蓝牙调试12。

persist.bluetooth.btsnooppath=/sdcard/btsnoop_hci.cfa：这个属性表示蓝牙调试文件的路径12。

persist.bluetooth.btsnoopsize=0xffff：这个属性表示蓝牙调试文件的大小12。

persist.bluetooth.rtkcoex=true：这个属性表示是否启用蓝牙和WiFi的共存12。

bluetooth.enable_timeout_ms=11000：这个属性表示蓝牙启用超时12。

ro.rk.screenoff_time=60000：这个属性表示屏幕关闭时间12。

drm.service.enabled=true：这个属性表示是否启用DRM服务12。

ro.boot.noril=true：这个属性表示是否禁用无线电接口层12。

keyguard.no_require_sim=true：这个属性表示是否需要SIM卡来解锁12。

[ro.com](http://ro.com).android.dataroaming=true：这个属性表示是否启用数据漫游12。

ril.function.dataonly=1：这个属性表示是否只使用数据功能12。

ro.config.enable.remotecontrol=false：这个属性表示是否启用远程控制12。

ro.rk.hdmisetting=true：这个属性表示是否启用HDMI设置12。

ro.vendor.udisk.visible=true：这个属性表示是否显示U盘12。

ro.safemode.disabled=true：这个属性表示是否禁用安全模式12。

ro.rk.screenshot_enable=true：这个属性表示是否启用截屏12。

sys.status.hidebar_enable=false：这个属性表示是否启用隐藏状态栏12。

ro.target.product=tablet：这个属性表示目标产品类型12。

persist.sys.zram_enabled=1：这个属性表示是否启用ZRAM12。

dalvik.vm.heapstartsize=16m：这个属性表示Dalvik虚拟机的初始堆大小12。

dalvik.vm.heapgrowthlimit=192m：这个属性表示Dalvik虚拟机的堆增长限制12。

dalvik.vm.heapsize=512m：这个属性表示Dalvik虚拟机的最大堆大小12。

dalvik.vm.heaptargetutilization=0.75：这个属性表示Dalvik虚拟机的目标堆利用率12。

dalvik.vm.heapminfree=512k：这个属性表示Dalvik虚拟机的最小空闲堆大小12。

dalvik.vm.heapmaxfree=8m：这个属性表示Dalvik虚拟机的最大空闲堆大小12。

ro.sf.lcd_density=320：这个属性表示LCD密度12。

ro.wifi.sleep.power.down=true：这个属性表示WiFi是否在睡眠时关闭12。

[persist.wifi.sleep.delay.ms](http://persist.wifi.sleep.delay.ms)=0：这个属性表示WiFi睡眠延迟12。

[persist.bt](http://persist.bt).power.down=true：这个属性表示蓝牙是否在睡眠时关闭12。

vendor.hwc.device.primary=DSI：这个属性表示主显示设备12。

vendor.hwc.device.extend=HDMI-A,eDP：这个属性表示扩展显示设备12。

persist.vendor.framebuffer.main=1080x1920@60：这个属性表示主帧缓冲区的分辨率和刷新率12。

ro.vendor.rk_sdk=1：这个属性表示供应商SDK的版本12。

vendor.hwc.enable_display_configs=true：这个属性表示是否启用显示配置12。

ro.debuggable=1

ro.adb.secure=0

### /vendor/default.prop

* 这个文件和./default.prop类似，也是包含了一些默认的系统属性。这些属性是在编译脚本中生成的，通常控制着一些安全性的设置。

ro.vndk.version=29：这是Vendor Native Development Kit (VNDK)的版本号1。VNDK是一组库，被供应商分区或产品分区中的其他库或二进制文件在运行时用于动态加载1。

ro.zygote=zygote64_32：这个属性定义了Zygote进程的模式2。Zygote是Android系统创建新进程的核心进程2。zygote64_32表示启动两个Zygote进程，对应的执行程序分别是app_process64（主模式）和app_process322。

ro.logd.size.stats=64K：这个属性可能与Android的日志守护进程（logd）有关，但我没有找到具体的解释。

log.tag.stats_log=I：这个属性可能与Android的日志标签有关，但我没有找到具体的解释。

ro.enable_boot_charger_mode=0：这个属性可能与设备的充电模式有关，但我没有找到具体的解释。

ro.board.platform=rk3588：这个属性表示设备的硬件平台是RK35883。RK3588是Rockchip公司的一款强大的SoC（系统级芯片）3。

ro.target.product=tablet：这个属性表示设备的目标产品类型是平板电脑4。

ro.oem_unlock_supported=1：这个属性表示设备支持OEM解锁5。如果设备支持刷写解锁，ro.oem_unlock_supported将被设置为15。

ro.flash_img.enable=false：这个属性可能与设备的刷机功能有关，但我没有找到具体的解释。

ro.bionic.arch=arm64：这个属性表示设备的Bionic库（Android的C库、数学库和动态链接器）的架构是ARM646。

ro.bionic.cpu_variant=cortex-a76：这个属性表示设备的CPU变种是Cortex-A766。

ro.bionic.2nd_arch=arm：这个属性表示设备的第二架构是ARM6。

ro.bionic.2nd_cpu_variant=cortex-a76：这个属性表示设备的第二CPU变种是Cortex-A766。

persist.sys.dalvik.vm.lib.2=[libart.so](http://libart.so)：这个属性表示Dalvik虚拟机使用的库是libart.so6。

dalvik.vm.isa.arm64.variant=cortex-a76：这个属性表示Dalvik虚拟机的ARM64指令集架构的变种是Cortex-A766。

dalvik.vm.isa.arm64.features=default：这个属性表示Dalvik虚拟机的ARM64指令集架构的特性是默认的6。

dalvik.vm.isa.arm.variant=cortex-a76：这个属性表示Dalvik虚拟机的ARM指令集架构的变种是Cortex-A766。

dalvik.vm.isa.arm.features=default：这个属性表示Dalvik虚拟机的ARM指令集架构的特性是默认的6。

ro.minui.default_rotation=ROTATION_NONE：这个属性可能与设备的默认旋转设置有关，但我没有找到具体的解释。

ro.minui.pixel_format=RGBX_8888：这个属性可能与设备的像素格式有关，但我没有找到具体的解释。
