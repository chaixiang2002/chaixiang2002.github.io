### Firefly roc_rk3588s_pc 开发板 OHOS 适配代码下载与编译

#### 1. 安装依赖工具

在 Ubuntu 18.04 上安装所需工具，执行以下命令：

```bash
sudo apt-get update && sudo apt-get install \
binutils git git-lfs gnupg flex bison gperf build-essential \
zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 \
lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev \
ccache libgl1-mesa-dev libxml2-utils xsltproc unzip m4 \
bc gnutls-bin python3.8 python3-pip ruby
```

> 说明：根据你的操作系统版本，适当调整安装命令。

#### 2. 获取标准系统源码

**前提条件：**

1. 注册 Gitee 账号。
2. 注册 Gitee SSH 公钥（参考 Gitee 帮助中心）。
3. 安装并配置 Git 客户端和 Git LFS。

```bash
git config --global user.name "yourname"
git config --global user.email "your-email-address"
git config --global credential.helper store
```

4. 安装 Gitee repo 工具：

方法一：

```bash
curl -s https://gitee.com/oschina/repo/raw/fork_flow/repo-py3 > /usr/local/bin/repo
chmod a+x /usr/local/bin/repo
pip3 install -i https://repo.huaweicloud.com/repository/pypi/simple requests
```

方法二：

```bash
curl -s https://gitee.com/oschina/repo/raw/fork_flow/repo-py3 > ./repo
chmod a+x ./repo
pip3 install -i https://repo.huaweicloud.com/repository/pypi/simple requests
```

**获取各版本源码操作步骤：**

- **下载 4.0-Release 版本代码**

```bash
./repo init -u https://gitee.com/openharmony/manifest.git -b OpenHarmony-4.0-Release --no-repo-verify
./repo sync -c
./repo forall -c 'git lfs pull'
```

**执行 prebuilts**

在源码根目录下执行脚本，安装编译器及二进制工具：

```bash
sudo bash build/prebuilts_download.sh
```

下载的 prebuilts 二进制默认存放在与 OpenHarmony 同目录下的 `OpenHarmony_2.0_canary_prebuilts` 目录下。

根据错误日志总结，另外所需工具安装：

```bash
sudo apt install openjdk-11-jdk
sudo apt-get install libxt-dev
sudo apt-get install libx11-dev
sudo apt install xorg-dev
sudo apt install libssl-dev
sudo apt install liblz4-tool
sudo apt install genext2fs
sudo apt install default-jdk
sudo apt install libtinfo5
sudo apt install u-boot-tools
sudo apt install mtools
sudo apt install mtd-utils
sudo apt install scons
sudo apt install gcc-arm-none-eabi
sudo apt install gcc-arm-linux-gnueabi
```

需要修改根目录下面的代码：

- `hos_4.0/drivers/hdf_core/adapter/khdf/linux/osal/src/osal_time.c` 函数添加 `void` 参数：

```c
uint64_t OsalGetSysTimeMs(void)
{
    OsalTimespec time;
    (void)memset_s(&time, sizeof(time), 0, sizeof(time));
    (void)OsalGetTime(&time);
    return (time.sec * HDF_KILO_UNIT + OsalDivS64(time.usec, HDF_KILO_UNIT));
}
```

- `ohos_4.0/drivers/peripheral/audio/hal/hdi_binder/server/src/hdf_audio_input_event.c` 将 `%llu` 改为 `%lu`：

```c
static void *AudioPnpInputStart(void *useless)
{
    int ret;
    (void)useless;
    const char *threadName = "pnp_headset";
    pthread_t threadInstance = pthread_self();
    AUDIO_FUNC_LOGI("threadInstance:%{public}lu", (uint64_t)threadInstance);

    if (pthread_setname_np(threadInstance, threadName) != 0) {
        AUDIO_FUNC_LOGE("Setname failed!");
        return NULL;
    }

    AUDIO_FUNC_LOGI("audio input start.");
    if (AudioPnpInputOpen() != HDF_SUCCESS) {
        return NULL;
    }

    do {
        ret = AudioPnpInputPollAndRead();
        if (ret != HDF_SUCCESS) {
            AUDIO_FUNC_LOGE("[AudioPnpInputPollAndRead] failed!");
            return NULL;
        }
    } while (g_bRunThread);

    return NULL;
}
```

#### 3. 编译

在 Linux 环境中进入源码根目录，执行以下命令进行版本编译：

```bash
sudo ./build.sh --product-name roc_rk3588s_pc --ccache
```

编译生成的文件将归档在 `out/rk3588s/` 目录下，固件输出在 `out/rk3588s/packages/phone/images/` 目录下。

#### 错误方法调试

可以通过反编译的方式定位具体报错堆栈：

1. 拷贝 `vmlinux` 文件（`./out/kernel/OBJ/linux-5.10/vmlinux`）到 `prebuilts/gcc/linux-x86/aarch64/gcc-linaro-7.5.0-2019.12-x86_64-aarch64-linux-gnu/bin` 中。
2. 进入该目录，执行：

```bash
./aarch64-linux-gnu-gdb vmlinux
```

3. 输入 `list *__clk_register+0x60` 输出：故障位置。

#### 在 `out/kernel/src` 修改配置选项：

```bash
sudo make CROSS_COMPILE=/data/panhy/ohos_opi5/prebuilts/gcc/linux-x86/aarch64/gcc-linaro-7.5.0-2019.12-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu- ARCH=arm64 menuconfig
```

然后再将out/kernel/obj下的.config拷贝到ohos_4.0/device/board/firefly/roc_rk3588s_pc/kernel/config/rk3588s_standard_defconfig之中，重新编译