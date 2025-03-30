![image-20250321105017202](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503211050147.png)

docker exec -it android_0 sh

这个shell进程并不是init进程的子进程，而是单独来自docker容器进程的子进程，与init进程是平级关系

因此在。rc文件中的export的环境变量，docker exec -it android_0 sh获取不了



### 那在这个shell在执行/system/xbin/s9su

![image-20250321120013080](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503211200487.png)



那在这个shell在执行sh

![image-20250321120336596](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202503211203898.png)