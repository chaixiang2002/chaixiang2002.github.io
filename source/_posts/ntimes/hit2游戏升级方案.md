# 1、目标：

目标配置:4开，hit2游戏正常跑，不出现无响应状态。

验证结果：目前跑了4片宿主机，4开hit2，目前能正常跑起来，一周已经未出现无响应和回到桌面的情况。

游戏可能会由于低内存，被系统kill，但是可以拉起来。

验证遗留问题：游戏偶尔会被未知进程杀死，怀疑是脚本。

## 2、方案

## 2.1  文件系统替换

数据盘由ext4替换成f2fs, 具体执行：使用新初始化脚本，重新初始化宿主机。

初始化脚本版本：现网版本

检查：登录宿主机，执行命令：more /etc/fstab

PARTLABEL=rootfs   /         ext4   rw,relatime,data=ordered 0 1
/dev/vg_data/userdata /userdata ext4 defaults 0 2
/dev/vg_data/root /root ext4 defaults 0 2
/dev/vg_data/thin_lv_android_0 /userdata/container/android_data/data_0 f2fs defaults 0 2
/dev/vg_data/thin_lv_android_1 /userdata/container/android_data/data_1 f2fs defaults 0 2
/dev/vg_data/thin_lv_android_2 /userdata/container/android_data/data_2 f2fs defaults 0 2
/dev/vg_data/thin_lv_android_3 /userdata/container/android_data/data_3 f2fs defaults 0 2
/userdata/container/swapfile none swap sw 0 0

## 2.2  cpu资源隔离(建议由业务平台下发)

1、cpu使用1-7核

2、每台云手机最大使用核数：1.6

检查： 登录宿主机，more  /userdata/arm-agent/bin/manage-shell/.env

# CPU绑核的初始化设置，格式：

# - 指定区间：0-7

# - 逐一指定：0,4,6

CPUSET_DEFAULT=1-7

# 安卓CUP时间片占用比例，

# 如果CPUSET_DEFAULT指定了6个核，CPUS_COMMON设置3，则表示可以利用这6个核的50%性能

# 如果设置0，则表示不限制

CPUS_COMMON=1.6

#cpu资源隔离

#X代表 0、1、2、3，云手机序号

CPUS_X=1.6
CPUSET_X=1-7

## 2.3 交换区：7G

1、要求重启宿主机，还生效。

2、建立交换区命令

sudo fallocate -l 7G /userdata/swapfile
sudo chmod 600 /userdata/swapfile
sudo mkswap /userdata/swapfile
sudo swapon /userdata/swapfile
sudo swapon --show
free -h

## 2.4 设置VPN和脚本-退出重启

客户自行操作

## 2.5 设置VPN和脚本-低内存保活

云机执行

s9 config -a am.persistentApps=com.hugan.nekobox,[com.wii2hit.mm](http://com.wii2hit.mm)

## 2.6 缓存回收由1个小时改成5分钟

执行命令：

echo '[Unit]
Description=Run drop-caches.service once 5 min

[Timer]
OnBootSec=5min
OnUnitActiveSec=5min

[Install]
WantedBy=timers.target
' > /usr/lib/systemd/system/drop-caches.timer

echo '[Unit]
Description=Drop system caches

[Service]
Type=oneshot
ExecStart=/sbin/sysctl -w vm.drop_caches=3

[Install]
WantedBy=multi-user.target
' > /usr/lib/systemd/system/drop-caches.service

systemctl daemon-reload
systemctl enable drop-caches.service
systemctl enable drop-caches.timer
systemctl start drop-caches.service
systemctl start drop-caches.timer

systemctl status drop-caches.service
systemctl status drop-caches.timer

检查：

在宿主机上执行命令：

dmesg -T |grep drop  查看两条记录间隔是否为5分钟。
