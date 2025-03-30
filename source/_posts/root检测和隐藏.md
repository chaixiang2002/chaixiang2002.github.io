1. 文件检查：看系统里有没有“/system/bin/su”或“/system/xbin/su”文件。
2. 权限判断：检查“/system”目录是不是可读写。
3. 命令测试：执行“id”命令，出现“uid=0 (root)”或者执行“su”命令后能访问特殊文件，可能已经ROOT。
4. 属性查看：读取“ro.secure”属性，值为0可能ROOT；对比Build指纹和官方的是否不同。

```
nsenter -t 4674 -m -- ls /system/bin/su
nsenter -t 4674 -m -- ls /system/xbin/su
nsenter -t 4674 -m -- ls su

nsenter -t 4674 -m -- touch system/aa   

nsenter -t 4674 -m -- id  

nsenter -t 4674 -m -- getprop ro.secure   
```



！！！！！！！原理是 mount方法和overlay 针对pid的挂载！！！！！！！！！！！！！！！！！！