# 添加 Product

[写给应用开发的 Android Framework 教程——玩转 AOSP 篇之添加 Product - 掘金 (juejin.cn)](https://juejin.cn/post/7203958049983529015)



* build/target：aosp 提供的 product 配置文件保存在这个目录下，我们选择的 aosp_x86_64-eng Product 就配置在这个目录下。
* device：芯片及方案厂商提供的 product 配置文件保存在这个目录下


针对我们选择的 aosp_x86_64-eng，我们主要关注以下几个文件：

* `/board/generic_x86_64/BoardConfig.mk` ： 用于硬件相关配置
* `/product/AndroidProducts.mk`   `/product/aosp_x86_64.mk`：用于配置 Product



### **include 和 inherit-product 的区别** ：

* 假设 `PRODUCT_VAR := a` 在 A.mk 中, `PRODUCT_VAR := b` 在 B.mk 中。
* 如果你在 A.mk 中 include B.mk，你最终会得到 `PRODUCT_VAR := b`。
* 但是如果你在 A.mk inherit-product B.mk，你会得到 `PRODUCT_VAR := a b`。并 inherit-product 确保您不会两次包含同一个 makefile 。



### **通用变量**


```makefile
PRODUCT_BRAND := Android

PRODUCT_NAME := sdk_phone_x86_64

PRODUCT_DEVICE := generic_x86_64

PRODUCT_MODEL := Android SDK built for x86_64
```

常用的**路径变量**

* SRC_TARGET_DIR 其值为 build/target
* LOCAL_DIR 代表当前目录


### 设置系统属性和拷贝文件

* PRODUCT_COPY_FILES： 用于完成拷贝，可以将源码中的文件拷贝到编译好的分区文件中
* PRODUCT_PROPERTY_OVERRIDES： 用于设置系统属性(覆盖)
