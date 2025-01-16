### /system/bin/su针对当前程序可见的挂载原理

等价于命令

```shell
$ ln -s /system/xbin/s9su /data/overlay_misc/upper/su
$ sudo mount -t overlay overlay -o lowerdir=/system/bin,upperdir=/data/overlay_misc/upper,workdir=/data/overlay_misc/workdir /system/bin

```

- **`lowerdir=/system/bin`**：指定 `/system/bin` 作为底层目录，原始系统文件存放位置。
- **`upperdir=/data/overlay_misc/upper`**：指定 `/data/overlay_misc/upper` 为上层目录，它包含了修改内容（如 `su` 的符号链接）。
- **`workdir=/data/overlay_misc/workdir`**：指定工作目录，用于存储 `overlay` 文件系统的临时数据。

挂载后，`/system/bin` 目录的内容会被 `overlay` 文件系统覆盖，并且上层目录的文件会覆盖底层目录中的同名文件。在这个例子中，`/system/bin/su` 会被 `/data/overlay_misc/upper/su`（指向 `/system/xbin/s9su` 的符号链接）覆盖。

### 核心原理

overlay文件系统

![18fde6a569ca14c3da4a84b7a041ee2c.png](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202501132103278.jpeg)

mount-t overlay -o lowerdir=/lower,upperdir=/upper,workdir=/work overlay /merged

上面的命令可以将"lowerdir"和"upper"目录堆叠到/merged目录，"workdir"工作目录要求是和"upperdir"目录同一类型文件系统的空目录。

也可以省略upperdir和workdir参数，但/merged为只读属性了：

mount-t overlay -o lowerdir=/upper:/lower overlay /merged

也可支持多lowerdir目录堆叠：

mount-t overlay -o lowerdir=/lower1:/lower2:/lower3,upperdir=/upper,workdir=/workoverlay /merged

lowerdir的多层目录使用":"分隔开，其中层级关系为/lower1> /lower2 > /lower3。
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。

原文链接：https://blog.csdn.net/feelabclihu/article/details/120793237

![image-20250113210504200](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202501132105213.png)





### 对原理的验证

```shell
ps -ef |grep troot

nsenter -t 34131 -m -- ls -al /system/bin/su
mkdir -p /data/local/overlay_misc                                                                           
mkdir -p /data/local/overlay_misc/workdir                                                                    
mkdir -p /data/local/overlay_misc/upper                                                                      
ln -s /system/xbin/s9su /data/local/overlay_misc/upper/su   
nsenter -t 34131 -m -- mount -t overlay overlay -o lowerdir=/system/bin,upperdir=/data/local/overlay_misc/upper,workdir=/data/local/overlay_misc/workdir /system/bin
nsenter -t 34131 -m -- ls -al /system/bin/su



ps -ef |grep troot

nsenter -t 58089 -m -- ls -al /system/bin/su
mkdir -p /data/local/overlay_misc                                                                           
mkdir -p /data/local/overlay_misc/workdir                                                                    
mkdir -p /data/local/overlay_misc/upper                                                                      
ln -s /system/xbin/s9su /data/local/overlay_misc/upper/su   
nsenter -t 58089 -m -- mount -t overlay overlay -o lowerdir=/system/bin,upperdir=/data/local/overlay_misc/upper,workdir=/data/local/overlay_misc/workdir /system/bin
nsenter -t 58089 -m -- ls -al /system/bin/su
```

验证成功！