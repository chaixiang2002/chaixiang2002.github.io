- [make menuconfig出现flex:not found_/bin/sh: flex not found-CSDN博客](https://blog.csdn.net/lufei12345678/article/details/134981658)
- /data/ubuntu/LubanCat_Linux_rk3588_SDK_20230913
- /data/ubuntu/LubanCat_Linux_rk3588_SDK_20230913/kernel/arch/arm64/configs
- /data/ubuntu/LubanCat_Linux_rk3588_SDK_20230913/kernel/arch/arm64/configs/lubancat_linux_rk3588_defconfig
- /data/ubuntu/LubanCat_Linux_rk3588_SDK_20230913/kernel .config
- make menuconfig


kernael/.config
make config
最终 dd写进去
lunch 2

1. cd /data/ubuntu/LubanCat_Linux_rk3588_SDK_20230913
2. export ARCH=arm64
3. cd kernel && make menuconfig              （root）
4. /  搜索
5. 到根目录 ./build.sh lunch 2
   ./build.sh
