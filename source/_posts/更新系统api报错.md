编译报错，要求隐藏api或更新api文档

![image-20241231175258309](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202412311752968.png)





 make api-stubs-docs-update-current-api更新api文档

![image-20241231175430361](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202412311754380.png)

报找不到android-support-multidex

错误原因，我们的源码缺少android-support-multidex

缺失的库源码在/linux_data/rockchip_android_src/android_10_bak/frameworks/multidex/library/Android.bp