booloader->kernel->init->zygoto->system_server->services_manager->launcher

booloader

从芯片预定义ROM开始执行，将引导程序加载到RAM，初始化硬件，建立起内存映射表，为内核环境做准备

Kernel
安卓内核启动，会设置缓存、被保护存储器、计划列表  初始化好各种设备驱动程序和数据结构，等等然后寻找init程序启动



init进程

是第一个进程，根据init.c  文件夹建立，挂载，rc文件解析，设置安卓系统属性，启动服务