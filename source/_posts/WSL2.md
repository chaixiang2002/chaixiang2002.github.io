[Winodws Subsystem for Linux（WSL）安装教程 - iCode504个人博客](https://www.icode504.com/posts/42.html)

[Windows上快速安装WSL2教程-阿里云开发者社区](https://developer.aliyun.com/article/886462)AAAAA



微软商店（Microsoft Store）打开记得关闭梯子

```sh
sudo apt install python3-pip python3-setuptools python3-wheel
pip3 install apt-smart
apt-smart -l
apt-smart -a

sudo apt update
sudo apt install openssh-server

```



## 更换WSL2存储位置

[更改WSL2的存放路径_wsl存储位置-CSDN博客](https://blog.csdn.net/CSDN_Huang1/article/details/124092336)

问题：
wsl默认存放路径为C盘，可根据需求将其导出到其他空间较大的盘符。

更改方式：
查看已安装的WSL的名称和版本，在Powershell中输入以下命令：
wsl -l --all -v

导出系统到指定位置，wsl --export <系统名> <导出目录>
wsl --export Ubuntu-20.04 D:\wsl-ubuntu-20.04.tar

删除当前C盘中的wsl系统
wsl --unregister Ubuntu-20.04

导入系统到指定位置，wsl --import <系统名> <安装位置> <tar文件目录> WSL版本号
wsl --import Ubuntu-20.04 D:\WSL2_Ubuntu D:\wsl-ubuntu-20.04.tar --version 2

配置之前的默认登录用户，ubuntu2004.exe config --default-user <用户名>
ubuntu2004.exe config --default-user wanyel





## 如何扩展 WSL 2 虚拟硬盘的大小

若要将 Linux 发行版的 VHD 大小扩展到超过**默认的 1TB 上限**（所分配的磁盘空间量），请执行以下步骤。 *（对于尚未更新的早期 WSL 版本，此最大默认值可能设置为 512GB 或 256GB）。*

[如何管理 WSL 磁盘空间 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/disk-space)

1. 使用 `wsl.exe --shutdown` 命令终止所有 WSL 实例

2. 将目录路径复制到与计算机上安装的 Linux 发行版关联的 *ext4.vhdx* 文件。 如需帮助，请参阅[如何查找 Linux 发行版的 vhdx 文件和磁盘路径](https://learn.microsoft.com/zh-cn/windows/wsl/disk-space#how-to-locate-the-vhdx-file-and-disk-path-for-your-linux-distribution)。

3. 使用管理员权限打开 Windows 命令提示符，然后输入以下命令来打开 [diskpart](https://learn.microsoft.com/zh-cn/windows-server/administration/windows-commands/diskpart) 命令解释器：

   Windows 命令提示符复制

   ```cmd
   diskpart
   ```

4. 现在会出现一个 `DISKPART>` 提示。 输入以下命令，将 `<pathToVHD>` 替换为与 Linux 发行版关联的 `ext4.vhdx` 文件的目录路径（步骤 2 中复制的）。

   Windows 命令提示符复制

   ```cmd
   Select vdisk file="<pathToVHD>"
   ```

5. 显示与此虚拟磁盘关联的详细信息，包括**虚拟大小**，表示当前分配给 VHD 的大小上限：

   Windows 命令提示符复制

   ```cmd
   detail vdisk
   ```

6. 需要将**虚拟大小**转换为 MB。 例如，如果**虚拟大小为 512 GB**，则等于 **512000 MB**。 你输入的新值必须大于此原始值。 要将 512 GB 的虚拟大小加倍到 1024 GB，需以 MB 为单位输入值：**1024000**。 请注意，不要输入高于实际需要的值，因为减小虚拟磁盘大小的过程要复杂得多。

7. 使用 Windows 命令提示符 `DISKPART>` 提示输入要分配给此 Linux 发行版的新的大小上限值：

   Windows 命令提示符复制

   ```cmd
   expand vdisk maximum=<sizeInMegaBytes>
   ```

8. 退出 `DISKPART>` 提示：

   Windows 命令提示符复制

   ```cmd
   exit
   ```

9. 启动此 Linux 发行版。 *（确保它在 WSL 2 中运行。可以使用以下命令确认这一点：`wsl.exe -l -v`。不支持 WSL 1）。*

10. 通过从 WSL 发行版命令行运行这些命令，让 WSL 知道它可以扩展此发行版的文件系统大小。 可能会看到以下消息，它响应第一个 mount 命令：“/dev: /dev 上未装载任何内容。”可以放心地忽略此消息。

    Bash复制

    ```bash
    sudo mount -t devtmpfs none /dev
    mount | grep ext4
    ```

11. 复制此项的名称，该名称类似于：`/dev/sdX`（X 表示任何其他字符）。 在下面的示例中，X 的值是 b：

Bash复制

```bash
   sudo resize2fs /dev/sdb <sizeInMegabytes>M
```

在上述示例中，我们将 vhd 大小更改为 **2048000**，因此命令将为：`sudo resize2fs /dev/sdb 2048000M`。

 备注

可能需要安装 resize2fs。 如果是这样，可以使用此命令进行安装：`sudo apt install resize2fs`。

输出将类似于以下内容：

Bash复制

```bash
resize2fs 1.44.1 (24-Mar-2021)
Filesystem at /dev/sdb is mounted on /; on-line resizing required
old_desc_blocks = 32, new_desc_blocks = 38
The filesystem on /dev/sdb is now 78643200 (4k) blocks long.
```

此 Linux 发行版的虚拟驱动器 (ext4.vhdx) 现已成功扩展到新的大小。

 重要

建议不要使用 Windows 工具或编辑器来修改、移动或访问 `AppData` 文件夹中与 WSL 相关的文件。 这样做可能会导致 Linux 分发版损坏。 如果要从 Windows 访问 Linux 文件，可通过路径 `\\wsl$\<distribution-name>\` 进行访问。 打开 WSL 分发版，然后输入 `explorer.exe .` 来查看此文件夹。 若要了解详细信息，请查看博客文章：[从 Windows 访问 Linux 文件](https://devblogs.microsoft.com/commandline/whats-new-for-wsl-in-windows-10-version-1903/#accessing-linux-files-from-windows)。

---

固定ip的目前方法
每次执行shell固定ip（还是子网）

```shell
#!/bin/bash
#  ~/wsl-ip

# 默认设置
STATIC_IP="172.23.62.100"  # 设置目标固定IP
GATEWAY="172.23.48.1"      # 设置网关
NETMASK="20"               # 子网掩码

# 检查网络接口
INTERFACE=$(ip route | grep '^default' | awk '{print $5}')
if [ -z "$INTERFACE" ]; then
    echo "未找到默认网络接口！请确保WSL网络正常连接。"
    exit 1
fi

# 配置静态IP
echo "正在为接口 $INTERFACE 配置静态IP $STATIC_IP..."
sudo ip addr flush dev $INTERFACE
sudo ip addr add $STATIC_IP/$NETMASK dev $INTERFACE
sudo ip route add default via $GATEWAY

# 验证结果
echo "新IP地址："
ip addr show dev $INTERFACE | grep "inet "

echo "WSL的IP地址已更改为 $STATIC_IP，网关为 $GATEWAY。"
```

[解决 WSL 开机网卡信息变动问题](https://minsonlee.github.io/2020/11/set-private-ip-for-wsl)

wsl_ip.bat

```bat
@REM https://minsonlee.github.io/2020/11/set-private-ip-for-wsl

@REM # `WSL 2`新增网卡
@REM # - 设置私有IP网段为192.168.33.10
@REM # - 广播地址为192.168.169.15
@REM # - 网卡名称为 eth0
@REM # - 设置网卡标签 eth0:1
wsl -u root ip addr add 192.168.33.10 broadcast 192.168.169.15 dev eth0 label eth0:1

@REM # 设置宿主机网卡`vEthernet (WSL)`地址为 `192.168.33.1`-需要管理员权限
netsh interface ip add address "vEthernet (WSL)" 192.168.33.1 255.255.255.240

wsl bash -c "echo snow | sudo -S service ssh restart"

```

物理机上执行

![image-20241223091954839](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202412230919780.png)