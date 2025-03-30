### 编译AOSP内核时出现错误的原因可能是缺少必要的依赖库或头文件

![image-20250316233904819](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503162339069.png)

解决方法：

1. **安装 OpenSSL 开发包**
   确保系统中安装了 OpenSSL 的开发包。在基于 Debian/Ubuntu 的系统上，可以通过以下命令安装：

   bash

   复制

   ```shell
   sudo apt-get update
   sudo apt-get install libssl-dev
   ```