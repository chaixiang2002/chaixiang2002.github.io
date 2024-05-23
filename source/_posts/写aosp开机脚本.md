
1. 编写sh脚本
2. 编写rc脚本

```
on boot
    exec root root -- /system/bin/sh -c /system/bin/script.sh false

on property:sys.boot_completed=1
    exec root root -- /system/bin/sh -c /system/bin/script.sh true

```

3. 将rc添加到系统中

   ```
   # boot_scripts
   PRODUCT_COPY_FILES += \
           vendor/ntimespace/scripts/s9.boot.rc:system/etc/init/s9.boot.rc \
           vendor/ntimespace/scripts/script.sh:system/bin/script.sh
   ```


### rc的执行

/init.rc是主要的.rc文件，由init可执行文件在开始执行时加载。它负责系统的初始设置。

在加载主目录/init.rc后,init立即加载包含在/{system,vendor,odm}/etc/init/目录中的所有文件。
