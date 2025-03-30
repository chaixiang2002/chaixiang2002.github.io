### 方法 1：使用`update-alternatives`切换Python版本

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

