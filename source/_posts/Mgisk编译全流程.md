步骤总览

1. git vpn代理
2. gradle vpn代理
3. git开启core.symlinks
4. 下载magisk源码
5. python环境：3.8
6. jdk环境：21
7. sdk：下载Android SDK
8. Rust准备
9. ndk： ./build.py ndk



### git vpn代理

本机

```
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy https://127.0.0.1:7890
```

同网段

```
git config --global http.proxy http://192.168.30.176:7890
git config --global https.proxy https://192.168.30.176:7890
```

### git开启core.symlinks

git config --global core.symlinks true

### 下载magisk源码

```
git clone --recurse-submodules https://github.com/KitsuneMagisk/Magisk.git
```

### jdk环境

sudo apt install openjdk-17-jdk       注意所有apt命令时要先切换Python 2.7才能使用，

```shell
echo 'export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
```

### 下载配置Android SDK

```bash
wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip

mkdir -p ~/Android/Sdk
unzip commandlinetools-linux-11076708_latest.zip -d /snow/Android/Sdk

echo 'export ANDROID_HOME=/snow/Android/Sdk' >> ~/.bashrc
echo 'export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools' >> ~/.bashrc
```

注意；要把~/Android/Sdk/cmdline-tools目录下 所有内容 移动到 ~/Android/Sdk/cmdline-tools/latest，记得要创建Android/Sdk/cmdline-tools/latest目录。

### gradle vpn代理

修改项目根目录下：gradle.properties

```toml
systemProp.http.proxyHost=192.168.30.176
systemProp.http.proxyPort=7890
systemProp.https.proxyHost=192.168.30.176
systemProp.https.proxyPort=7890
```

### python环境

`update-alternatives`是一个用于管理多个版本软件的工具，可以方便地切换Python版本。

1. **安装Python 3.8**： 如果系统中尚未安装Python 3.8，可以通过以下命令安装：

   bash复制

   ```bash
   sudo apt update
   sudo apt install python3.8
   ```

2. **配置`update-alternatives`**： 将Python 2.7和Python 3.8添加到`update-alternatives`中：

   bash复制

   ```bash
   sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
   sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 2
   ```

3. **切换Python版本**： 使用以下命令切换默认的Python版本：

   bash复制

   ```bash
   sudo update-alternatives --config python
   ```

   系统会列出所有可用的Python版本及其优先级，输入对应的编号即可切换。

### ndk

```
./build.py ndk
```



### 正式全编译

```
./build.py -v all
```



















# 易错点

#### ANDROID_SDK_ROOT未设置

![image-20250305183418634](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503051834446.png)

解决方法：echo 'export ANDROID_SDK_ROOT=/snow/Android/Sdk' >>  ~/.bashrc



#### 项目指定cargo与glibc版本不兼容

![image-20250305184338098](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503051843342.png)



#### 安卓SDK协议没有同意

![image-20250306120307365](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503061203860.png)

/snow/Android/Sdk/cmdline-tools/latest/bin/sdkmanager --licenses





没有GCC

![image-20250307011755608](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503070117732.png)

 sudo apt install -y build-essential clang









JDK版本不兼容

![image-20250307014816298](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503070148271.png)

```
sudo apt install openjdk-21-jdk 
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

要求jdk21

