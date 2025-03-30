问题：

```shell
root@vm:/home/snow/Magisk# fdisk -l
Disk /dev/loop0: 73.89 MiB, 77479936 bytes, 151328 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/loop1: 139.55 MiB, 146333696 bytes, 285808 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/loop2: 44.44 MiB, 46596096 bytes, 91008 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/loop3: 44.45 MiB, 46604288 bytes, 91024 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sda: 931.51 GiB, 1000204886016 bytes, 1953525168 sectors
Disk model: VMware Virtual S
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 64BD0B84-7F0B-4644-8639-F0A6EF7F5AA6

Device       Start        End    Sectors   Size Type
/dev/sda1     2048       4095       2048     1M BIOS boot
/dev/sda2     4096    4198399    4194304     2G Linux filesystem
/dev/sda3  4198400 1953521663 1949323264 929.5G Linux filesystem


Disk /dev/mapper/ubuntu--vg-ubuntu--lv: 100 GiB, 107374182400 bytes, 209715200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
root@vm:/home/snow/Magisk# df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              2.8G  1.7M  2.8G   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   98G   22G   71G  24% /
tmpfs                               14G     0   14G   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          2.0G   96M  1.7G   6% /boot
tmpfs                              2.8



为什么我1T的硬盘，可是文件系统缺这么少？是不是少挂载分区了？
```





#### 步骤 1：创建新的逻辑卷（可选）

如果你希望将 `/dev/sda3` 的空间用于一个新的逻辑卷并挂载到 `/snow`，可以按照以下步骤操作：

1. 创建一个新的逻辑卷：

   bash

   复制

   ```
   sudo lvcreate -n snow-lv -l 100%FREE ubuntu-vg
   ```

   这里 `snow-lv` 是新逻辑卷的名称，`ubuntu-vg` 是卷组名称。

2. 格式化逻辑卷：

   bash

   复制

   ```
   sudo mkfs.ext4 /dev/ubuntu-vg/snow-lv
   ```

3. 挂载逻辑卷到 `/snow`：

   bash

   复制

   ```
   sudo mount /dev/ubuntu-vg/snow-lv /snow
   ```

4. 检查挂载结果：

   bash

   复制

   ```
   df -h
   ```

5. 设置开机自动挂载：
   编辑 `/etc/fstab` 文件：

   bash

   复制

   ```
   sudo nano /etc/fstab
   ```

   添加以下内容：

   plaintext

   复制

   ```
   /dev/ubuntu-vg/snow-lv /snow ext4 defaults 0 2
   ```

   保存并退出。

6. 测试配置：

   bash

   复制

   ```
   sudo mount -a
   ```

------

#### 步骤 2：调整权限（可选）

如果你希望普通用户（如 `snow`）可以访问 `/snow`，可以更改挂载点的所有者：

bash

复制

```
sudo chown snow:snow /snow
```