**一.源码位置路径**

    模块路径：system/core/lmkd/

    主代码路径：system/core/lmkd/lmkd.c

![](http://wiki.ntimespace.com/download/thumbnails/31590247/image2024-9-5_9-46-36.png?version=1&modificationDate=1725500796599&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_9-46-36.png")

**二.lmkd 启动过程源码分析**

1. lmkd进程启动

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_9-51-49.png?version=1&modificationDate=1725501110053&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_9-51-49.png")

** 2. lmkd→main()：入口函数**

LMKD进程的入口main函数，主要初始化该模块相关参数、消息事件

![](http://wiki.ntimespace.com/download/thumbnails/31590247/image2024-9-5_10-1-27.png?version=1&modificationDate=1725501687500&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_10-1-27.png")

**3.lmkd→init()：初始化**

step 1. 创建epoll

创建了一个epoll实例，整个lmkd的消息处理都是依赖epoll 机制来管理

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_10-4-51.png?version=1&modificationDate=1725501892153&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_10-4-51.png")

step 2. 初始化socket lmkd

   lmkd端的socket通信进行初始化，这个socket用于与AMS模块通信，socket连接成功后，响应事件处理由**ctrl_connect_handler**函数处理。

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_10-7-49.png?version=1&modificationDate=1725502069589&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_10-7-49.png")

**step 3. 确定是否用LMK 驱动程序**

  Android 以前版本使用内存LMK 驱动程序来监控系统内存情况，从Kernel 4.12开始，LMK驱动程序从上游内核中移除，由应用空间的 lmkd 执行内存监控和进程终止任务。
 通过函数access 确认旧的节点是否还存在，用以确认kernel 是否还在用LMK 驱动程序。之所以有这样的处理，应该是Android 为了兼容旧版本kernel。目前Android10上，该节点已不存在。

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_10-9-44.png?version=1&modificationDate=1725502184505&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_10-9-44.png")

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_10-10-43.png?version=1&modificationDate=1725502244038&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_10-10-43.png")

**step 4. 初始化PSI**

**4.1 PSI介绍**

PSI **（** Pressure Stall Information ）提供了一种评估系统资源压力的方法。系统有三个基础资源：CPU、Memory 和 IO，无论这些资源配置如何增加，似乎永远无法满足软件的需求。一旦产生资源竞争，就有可能带来延迟增大，使用户体验到卡顿。

如果没有一种相对准确的方法检测系统的资源压力程度，有两种后果。一种是资源使用者过度克制，没有充分使用系统资源；另一种是经常产生资源竞争，过度使用资源导致等待延迟过大。准确的检测方法可以帮忙资源使用者确定合适的工作量，同时也可以帮助系统制定高效的资源调度策略，最大化利用系统资源，最大化改善用户体验。

Facebook 在 2018 年开源了一套解决重要计算集群管理问题的 Linux 内核组件和相关工具，PSI 是其中重要的资源度量工具，它提供了一种实时检测系统资源竞争程度的方法，以竞争等待时间的方式呈现，简单而准确地供用户以及资源调度者进行决策

PSI 相关源代码核心功能都在  kernel/sched/psi.c 文件中实现

**4.2、PSI 用户接口定义**

每类资源的压力信息都通过 proc 文件系统的独立文件来提供，路径为 /proc/pressure/cpu, memory, and io.

其中 CPU 压力信息格式如下：

some avg10=2.98 avg60=2.81 avg300=1.41 total=268109926

memory 和 io 格式如下：

some avg10=0.30 avg60=0.12 avg300=0.02 total=4170757

full avg10=0.12 avg60=0.05 avg300=0.01 total=1856503

avg10、avg60、avg300 分别代表 10s、60s、300s 的时间周期内的阻塞时间百分比。total 是总累计时间，以毫秒为单位。

some 这一行，代表至少有一个任务在某个资源上阻塞的时间占比，full 这一行，代表所有的非idle任务同时被阻塞的时间占比，这期间 cpu 被完全浪费，会带来严重的性能问题。我们以 IO 的 some 和 full 来举例说明，假设在 60 秒的时间段内，系统有两个 task，在 60 秒的周期内的运行情况如下图所示：

![](https://i-blog.csdnimg.cn/blog_migrate/9fe4b1f3675ed2d0d299e258dd40d9d2.png)![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_10-55-48.png?version=1&modificationDate=1725504948305&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_10-55-48.png")

红色阴影部分表示任务由于等待 IO 资源而进入阻塞状态。Task A 和 Task B 同时阻塞的部分为 full，占比 16.66%；至少有一个任务阻塞（仅 Task B 阻塞的部分也计算入内）的部分为 some，占比 50%。

some 和 full 都是在某一时间段内阻塞时间占比的总和，阻塞时间不一定连续，如下图所示：

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_10-56-54.png?version=1&modificationDate=1725505014908&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_10-56-54.png")

IO 和 memory 都有 some 和 full 两个维度，那是因为的确有可能系统中的所有任务都阻塞在 IO 或者 memory 资源，同时 CPU 进入 idle 状态。

**4.3、LMKD初始化PSI**

**   下面代码可以看到，psi监控了/proc/pressure/memory 这个节点，并定义了三种memory pressure levels ： VMPRESS_LEVEL_LOW ,VMPRESS_LEVEL_MEDIUM,VMPRESS_LEVEL_CRITICAL，并且对应设置了对应的内存堵塞上报压力的阀值psi_thresholds,**

**当系统内存堵塞达到设置的阀值，PSI 会自动上报,并调用设置的处理函数mp_event_common进行处理**

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_11-1-40.png?version=1&modificationDate=1725505301236&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-1-40.png")![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_11-2-43.png?version=1&modificationDate=1725505364149&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-2-43.png")

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_11-8-10.png?version=1&modificationDate=1725505690832&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-8-10.png")

![](http://wiki.ntimespace.com/download/thumbnails/31590247/image2024-9-5_11-9-17.png?version=1&modificationDate=1725505758019&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-9-17.png")

**4. lmkd→mainloop：epoll消息处理**

从main函数代码看，初始化完成会调用mainloop(),mainloop主要是通过epoll_wait阻塞线程，有消息响应后，再分发消息给对应的handler处理对应逻辑。

![](http://wiki.ntimespace.com/download/thumbnails/31590247/image2024-9-5_11-23-11.png?version=1&modificationDate=1725506591488&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-23-11.png")

**5. lmkd→mp_event_common()**

   处理内存压力上报的 event事件，决定kill 进程的策略

策略：首先会去读取 这两个节点的值

#defineMEMCG_MEMORY_USAGE"/dev/memcg/memory.usage_in_bytes"
#defineMEMCG_MEMORYSW_USAGE"/dev/memcg/memory.memsw.usage_in_bytes"

然后会去算这两个的百分比，判断是不是需要给内存压力level降级，然后根据level找到对应的min adj的值，再调用 find_and_kill_process() kill 高于这个adj值的进行

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_11-36-9.png?version=1&modificationDate=1725507369771&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-36-9.png")

![](http://wiki.ntimespace.com/download/thumbnails/31590247/image2024-9-5_11-38-46.png?version=1&modificationDate=1725507526334&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-38-46.png")

![](http://wiki.ntimespace.com/download/attachments/31590247/image2024-9-5_11-48-10.png?version=1&modificationDate=1725508091094&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-48-10.png")

![](http://wiki.ntimespace.com/download/thumbnails/31590247/image2024-9-5_11-47-0.png?version=1&modificationDate=1725508021152&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-47-0.png")

****6. lmkd→find_and_kill_process()****

找到高于min adj的进程，并kill，其中 #define OOM_SCORE_ADJ_MAX       1000

![](http://wiki.ntimespace.com/download/thumbnails/31590247/image2024-9-5_11-54-42.png?version=1&modificationDate=1725508482303&api=v2 "软件研发中心 &gt; android10 lowmemorykill 模块源码和策略分析 &gt; image2024-9-5_11-54-42.png")

**三.总结**

    从上述lmkd 源码分析，android10 目前不再 采用内存LMK 驱动程序来监控系统内存情况，用了新的PSI 压力失速信息 来监控内存压力level，

然后再通过压力level对应的oomadj的值去kill高于 这个adj 的进程，从而达到释放内存减轻内存压力的目的
