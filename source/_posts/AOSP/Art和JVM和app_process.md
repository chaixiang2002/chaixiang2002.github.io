## Dalvik:Android的JVM

做出的改变

- 多个Class融进一个Dex文件			：节省存储空间
- Dex文件可以多个进程共享              ：节省内存
- 应用程序运行前对字节码检验          ：节省启动应用程序1的时间
- 字节码优化                                         ：程序运行更快
- 多进程间共享代码只读                      ：防篡改



## Art:取代Dalvik虚拟机

多出来的优点

- AOT技术，Dex还是字节码，AOT会根据目标平台编译成机器码



格外补充：

- Dalvik有种叫JIT的技术，将频繁执行的字节码翻译成机械码，但是他比起AOT，只是在程序运行的时候把频繁执行的部分翻译，这会加重cpu的负担。AOT是运行前就逐步把字节码翻译成机械码
- 有一个精简的编译器叫dex2oat，apk发布是发布dex，用户安装运行时应用会被dex2oat编译成oat(机械码)



## app_process:安卓特化的Java程序启动器

主要区别和说明如下：

1. **启动方式不同**
   在标准 Java 环境下，“java -jar myjar.jar”直接调用 JDK 提供的 java 命令来加载并执行 jar 包中的 main() 方法；而在 Android 中，并没有独立的 java 命令。app_process 是 Android 系统中的一个原生可执行文件，主要负责启动整个 Java 虚拟机（ART 或 Dalvik）以及相关的运行时环境。它不仅可以用来运行你自己编译好的 dex（或 apk 中的 dex）文件，还承担了系统进程初始化（例如 zygote 进程的启动）的重任。

   [ljd1996.github.io](https://ljd1996.github.io/2019/11/11/app-process使用/)

   

2. **参数和环境配置**
   使用 app_process 启动 Java 代码时，需要通过设置环境变量 CLASSPATH 来指定要运行的 dex 或 apk 文件，并且在命令行中指定启动类（即包含 main() 方法的类）。例如：

   ```bash
   export CLASSPATH=/sdcard/myapp.dex
   app_process /system/bin com.example.MyMainClass
   ```

   这与“java -jar myjar.jar”类似，但内部实现上，app_process 需要先初始化 ART 虚拟机，再进行 native 方法注册、环境配置等一系列工作，然后再调用指定类的 main() 方法。

   [blog.csdn.net](https://blog.csdn.net/mcsbary/article/details/108357846)

   

3. **系统服务与安全性**
   app_process 除了可以用于运行普通的 Java 应用外，它还是系统启动流程中的关键组成部分，比如用于启动 zygote 进程、system_server 进程等，这些进程负责启动和管理 Android 系统的大部分服务。因而，app_process 内部还包含了对安全、权限、进程管理等方面的诸多处理，而这些都是普通的“java -jar”命令所不涉及的。



## zygote的启动

##### **什么要设计两个服务：zygote 和 zygote_secondary**

1. **支持多架构（64位和32位）**

   - **zygote64_32** 服务使用 `/system/bin/app_process64`，它是为 64 位系统架构提供支持的 zygote 进程。这意味着它可以启动 64 位应用和服务，并且可以为 64 位应用程序提供共享内存空间和资源。
   - **zygote_secondary** 服务使用 `/system/bin/app_process32`，它用于支持 32 位系统架构。对于运行 32 位应用的设备，zygote_secondary 是必不可少的。

   Android 支持多种架构（包括 32 位和 64 位），因此需要两个独立的 zygote 服务来分别为不同架构的应用程序提供支持。每个 zygote 服务将根据其架构分别启动，并且为相应架构的应用提供资源和初始化。

2. **性能和资源隔离**
   为了优化性能，避免不同架构的应用程序之间相互影响，AOSP 采用了将 64 位和 32 位应用程序分别启动在不同的 zygote 进程中。这可以减少不同架构之间的内存和资源冲突，提高启动效率并减少潜在的错误。

------

##### **启动参数解析**

我们来逐一解析每个启动参数的作用。

##### **zygote 服务 (zygote64_32)**

```
bash复制编辑service zygote /system/bin/app_process64 -Xzygote /system/bin --zygote --start-system-server --socket-name=zygote
    class main
    priority -20
    user root
    group root readproc reserved_disk
    socket zygote stream 660 root system
    socket usap_pool_primary stream 660 root system
    onrestart exec_background - system system -- /system/bin/vdc volume abort_fuse
    onrestart write /sys/power/state on
    onrestart restart audioserver
    onrestart restart cameraserver
    onrestart restart media
    onrestart restart netd
    onrestart restart wificond
    task_profiles ProcessCapacityHigh MaxPerformance
    critical window=${zygote.critical_window.minute:-off} target=zygote-fatal
```

1. **/system/bin/app_process64**
   这是实际启动 Zygote 进程的可执行文件路径，`app_process64` 是为 64 位系统准备的。
2. **-Xzygote**
   此参数指示 app_process 启动 zygote 模式。这是 Android 系统启动的特殊模式，启用后，zygote 进程将通过 `fork()` 创建新的应用进程。
3. **/system/bin**
   这指定了父进程（zygote）的当前工作目录，通常是 `/system/bin`，即大部分系统命令的存放位置。
4. **--zygote**
   这个参数告知 app_process 启动一个 Zygote 进程，并进行相应的初始化，以便为所有后续应用进程提供环境。
5. **--start-system-server**
   这个参数启动系统服务器（`system_server`），这是 Android 系统中负责管理各种系统服务的关键进程。它是系统中不可缺少的一部分，管理如 ActivityManagerService、WindowManagerService 等核心服务。
6. **--socket-name=zygote**
   这是为 Zygote 进程创建的 Unix 域套接字名称，用于进程间通信。其他进程（如 app 或 system_server）将通过此套接字与 Zygote 进程进行通信。
7. **class main**
   启动时指定要执行的 Java 类的入口点。这里指定了 `main`，表示 zygote 进程会执行 Java 类中的 `main()` 方法。
8. **priority -20**
   这设置了 zygote 进程的优先级。`-20` 是一个高优先级的值，意味着 zygote 进程会优先于大多数其他进程，保证其在系统启动时优先执行。
9. **user root, group root**
   这些选项指定了 zygote 进程的用户和组权限，通常是 root 用户和 root 组。
10. **socket zygote stream 660 root system**
    创建一个名为 `zygote` 的 Unix 域套接字，允许 `root` 和 `system` 用户进行读写操作。这个套接字用于进程间通信。
11. **onrestart exec_background**
    定义了 zygote 进程重启时要执行的命令。这里是一个后台命令，用于执行系统命令如中止某些挂载操作。
12. **onrestart write /sys/power/state on**
    在进程重启时，执行系统命令开启电源管理。
13. **onrestart restart audioserver**
    如果 zygote 进程重启，也会重启音频服务（audioserver）。
14. **task_profiles ProcessCapacityHigh MaxPerformance**
    为 zygote 进程指定任务配置文件，这里是将 `zygote` 设置为高性能模式，优先保证其启动和执行效率。
15. **critical window=${zygote.critical_window.minute:-off} target=zygote-fatal**
    设置了 zygote 进程的关键窗口参数，定义了当 zygote 进程出现严重错误时的响应行为。

------

##### **zygote_secondary 服务 (zygote_secondary)**

```
bash复制编辑service zygote_secondary /system/bin/app_process32 -Xzygote /system/bin --zygote --socket-name=zygote_secondary --enable-lazy-preload
    class main
    priority -20
    user root
    group root readproc reserved_disk
    socket zygote_secondary stream 660 root system
    socket usap_pool_secondary stream 660 root system
    onrestart restart zygote
    task_profiles ProcessCapacityHigh MaxPerformance
```

与 `zygote` 服务的参数基本相同，但有以下不同点：

1. **/system/bin/app_process32**
   这是为 32 位架构设计的 zygote 进程启动文件。
2. **--enable-lazy-preload**
   启用延迟预加载功能，这意味着在启动 zygote 进程时并不会立刻加载所有的类，而是延迟到实际需要的时候再加载，以节省启动时的内存和资源。
3. **--socket-name=zygote_secondary**
   这个套接字名称用于 32 位架构的 zygote 进程。与主 zygote 进程的通信不同，它使用的是 `zygote_secondary` 套接字。
4. **onrestart restart zygote**
   如果 `zygote_secondary` 进程重启，会导致主 zygote 进程重新启动。







### 示例input的启动

```shell
793b2c01bf4f:/ #  cat /system/bin/input
#!/system/bin/sh
# Script to start "input" on the device, which has a very rudimentary
# shell.
#
base=/system
export CLASSPATH=$base/framework/input.jar
exec app_process $base/bin com.android.commands.input.Input "$@"

793b2c01bf4f:/ # 
```

