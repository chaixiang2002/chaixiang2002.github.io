## 所有的坑在最下面说明

一、说明一下aosp任何编译的通用流程（无论是aosp还是redroid都是）

1. source build/envsetup.sh       #（在aosp根目录下），设置编译所需环境变量
2. lunch                                      #（输入序号或者产品名）选择想要编译的产品![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_15-51-14.png?version=1&modificationDate=1705650674450&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_15-51-14.png")
3. m                                            #编译该产品

## 二、从零开始编译Redroid10

## 编译Redroid10的大致流程（概要）

1. 下载aosp10源码
2. 下载redroid项目源码
3. 下载aosp10的补丁并打上补丁（redroid-patches）
4. 下载浏览器的apk
5. 创建ubuntu dockers容器（大家统一编译环境，到时候在这个容器里编译整个项目；redroid-builder）
6. 编译整个项目
7. 将编译好的镜像打包成docker镜像
8. 测试docker镜像是否能用（用打包好的镜像建一个docker容器，并检查该安卓容器）

### 完整且具体的编译步骤

0. 编译前准备相关软件（repo，git，git-fls）

apt install repo

vim /usr/bin/repo

REPO_UR 的值替换为 [https://gerrit-googlesource.proxy.ustclug.org/git-repo](https://gerrit-googlesource.proxy.ustclug.org/git-repo)     #换成中科大的源（这一步可跳过）

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_16-28-53.png?version=1&modificationDate=1705652933967&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_16-28-53.png")

sudo ln -s /usr/bin/python3 /usr/bin/python                                                                  #保证自己是python3，不是2

git config --global user.email "973731820@[qq.com](http://qq.com)"                                                     #如果git没有设置身份要进行这一步，如果有就不需要

git config --global [user.name](http://user.name) "ubuntu_ntimes"                                                              #如果git没有设置身份要进行这一步，如果有就不需要

apt install git-lfs                                                                                                               #千万不要忘记下载这个

#### 1.下载aosp10源码

cd 该项目的目录

repo init -u [git://mirrors.ustc.edu.cn/aosp/platform/manifest](git://mirrors.ustc.edu.cn/aosp/platform/manifest) -b android-10.0.0_r47 --depth=1                     #设置要下载的项目的地址，这里设置为android-10.0.0_r47，深度为1

2.下载redroid项目源码

git clone [https://github.com/remote-android/local_manifests.git](https://github.com/remote-android/local_manifests.git) .repo/local_manifests -b 10.0.0                  #设置添加要下载的项目的地址，这里添加[remote-android](https://github.com/remote-android/local_manifests.git)项目，版本是10

repo sync -c –j8                                                                                                                                                  #拉取所有项目的源码，-j8是8个线程

3.下载aosp10的补丁并打上补丁（redroid-patches）

git clone [https://github.com/remote-android/redroid-patches.git](https://github.com/remote-android/redroid-patches.git) ../redroid-patches                                     #下载补丁，下载到自己知道的位置

../redroid-patches/apply-patch.sh /root/code/aosp                                                                                          #打上补丁，打到项目根目录，记住一定一定一定要用绝对路径！！！！

4.下载浏览器的apk（不要忘了这一步！！！，确保安装了git-lfs）

cd external/chromium-webview/prebuilt/arm64/

git rev-parse --git-dir

git config --global --add safe.directory ~/code/aosp/external/chromium-webview/prebuilt/arm64             #地址记得换成自己实际的地址

git lfs pull

cd ../x86_64/

git lfs pull

5.创建ubuntu dockers容器（大家统一编译环境，到时候在这个容器里编译整个项目；redroid-builder）

git clone [https://github.com/remote-android/redroid-doc.git](https://github.com/remote-android/redroid-doc.git)                                                        #下载统一环境的构建文件Dockfile

cd redroid-doc/android-builder-docker/

vim Dockerfile                                                                                                                                   #修改一下Dockerfile,不修改会报错

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_16-55-2.png?version=1&modificationDate=1705654503049&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_16-55-2.png")

修改内容可以复制：
RUN getent group $groupid || groupadd -g $groupid $username 
    && id -u$username &>/dev/null || useradd -m -u $userid -g $groupid $username 
    && echo "$username ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
    && echo $username >/root/username
    && echo "$username:$username" | chpasswd && adduser $username sudo

docker build --build-arg userid=$(id -u) --build-arg groupid=$(id -g) --build-arg username=$(id -un) -t redroid-builder .                        #构建 该统一环境的 镜像

docker run -it --rm --hostname redroid-builder --name redroid-builder -v ~/code/[aosp:/src redroid-builder](http://aosp/src redroid-builder)                                             #运行该统一镜像，注意路径换成自己aosp根目录的地址     ，注意此时将进入该容器内

6.开始编译Redroid10（arm架构）

注意此时已经进入redroid-builder容器内，下面都在容器内的命令

1. source build/envsetup.sh       #（在aosp根目录下），设置编译所需环境变量![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_15-51-14.png?version=1&modificationDate=1705650674450&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_15-51-14.png")
2. lunch                                      #（输入序号或者产品名）选择想要编译的产品
3. m                                            #编译该产品

成功编译后，会有绿色字提醒成功

7.将编译好的镜像打包成docker镜像

注意此时要退出redroid-builder容器 exit

cd out/target/product/redroid_arm64/                                                            #这是编译成功镜像所在的位置

mount system.img system -o ro                                                                       #挂载system

mount vendor.img vendor -o ro                                                                       #挂载vendor

tar --xattrs -c vendor -C system --exclude="./vendor" . | docker import -c 'ENTRYPOINT ["/init", "androidboot.hardware=redroid"]' - redroid10arm                       #打包成dockers镜像

umount system  vendor                                                                                    #卸载system         vendor

8.测试docker镜像是否能用（用打包好的镜像建一个docker容器，并检查该安卓容器）

docker run -itd  --privileged --name redroid10arm_1 
    -v ./[redroid10arm_1:/data](http://redroid10arm_1/data) 
    -p 1101:5555
    redroid10arm
    androidboot.redroid_width=1080
    androidboot.redroid_height=1920
    androidboot.redroid_dpi=480
    androidboot.redroid_gpu_mode=guest \

# 所有的坑

1.第5步发现没有Dockerfile

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_18-52-38.png?version=1&modificationDate=1705661558482&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_18-52-38.png")

原因:Dockerfile在git clone [https://github.com/remote-android/redroid-doc.git](https://github.com/remote-android/redroid-doc.git)    项目中，你可能没有在redroid-doc/android-builder-docker/执行或者没有克隆该仓库，请仔细按说明步骤操作

2.第5步发现ubuntu容器构建不起来，向如下

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_18-47-18.png?version=1&modificationDate=1705661238654&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_18-47-18.png")

解决方法：

手动拉取镜像

docker pull ubuntu:20.04

3.第5步发现用户已存在，如图

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_18-56-52.png?version=1&modificationDate=1705661812421&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_18-56-52.png")

解决方法：请修改Dockerfile

vim Dockerfile                                           #修改一下Dockerfile,不修改会报错

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_16-55-2.png?version=1&modificationDate=1705654503049&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_16-55-2.png")

修改内容可以复制：
RUN getent group $groupid || groupadd -g $groupid $username 
    && id -u$username &>/dev/null || useradd -m -u $userid -g $groupid $username 
    && echo "$username ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
    && echo $username >/root/username
    && echo "$username:$username" | chpasswd && adduser $username sudo

4.第6步，编译报错，Apk非法文件，无法解压

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_19-1-41.png?version=1&modificationDate=1705662101820&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_19-1-41.png")

没有拉取浏览器apk,解决方法请看第4步。

5.第三步补丁打不进去

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_19-3-59.png?version=1&modificationDate=1705662239431&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_19-3-59.png")

解决方法，请用绝对路径，不可以使用相对路径

6.如何检测补丁是否成功打上去

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_19-9-13.png?version=1&modificationDate=1705662553800&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_19-9-13.png")

到system/core/init/first_stage_init.cpp，看看是否和图片上一样，一样说明打了补丁，如果多了一个LOG（Fetal）,说明根本没有打上补丁，请执行第3步

7.安卓dockers容器运行就闪退，journalctl -f，如图

![](http://wiki.ntimespace.com/download/attachments/9997017/image2024-1-19_19-13-57.png?version=1&modificationDate=1705662838283&api=v2 "软件研发中心 &gt; 从AOSP10到Redroid10的完整编译教程（含踩坑记录） &gt; image2024-1-19_19-13-57.png")

请看看上个坑，是到system/core/init/first_stage_init.cpp的问题

8.关于Aosp清除和完全清除

make clean和[make clobber](https://blog.csdn.net/pcsxk/article/details/52594223)
