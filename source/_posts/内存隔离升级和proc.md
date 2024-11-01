



1. apt install lxcfs
2. systemctl start  lxcfs
3. 修改 vim /userdata/arm-agent/bin/manage-shell/docker-compose.yml
   - 映射      - "/var/lib/lxcfs/proc/meminfo:/proc/meminfo:rw
   - 3.2修改    deploy:
           resources:
             limits:
               memory: 3600m  

4. android_ctl.sh reset 2 --image=rk3588:RK_ANDROID10-RKR14-huangkb09061837

#### 怎么云机的proc/meminfo还是宿主机的？

- system/core/init/first_stage_init.cpp

```cpp
#define MAKE_STR(x) __STRING(x)
  // CHECKCALL(mount("proc", "/proc", "proc", 0, "hidepid=2,gid=" MAKE_STR(AID_READPROC)));
#undef MAKE_STR
```



内存是

external/toybox/toys/other/free.c
void free_main(void)

[sys.c - kernel/sys.c - Linux source code v5.10.226 - Bootlin](https://elixir.bootlin.com/linux/v5.10.226/source/kernel/sys.c#L2576)

static int [do_sysinfo](https://elixir.bootlin.com/linux/v5.10.226/C/ident/do_sysinfo)(struct [sysinfo](https://elixir.bootlin.com/linux/v5.10.226/C/ident/sysinfo) *info)

[si_meminfo](https://elixir.bootlin.com/linux/v5.10.226/C/ident/si_meminfo)(info);

https://elixir.bootlin.com/linux/v5.10.226/source/mm/page_alloc.c void [si_meminfo](https://elixir.bootlin.com/linux/v5.10.226/C/ident/si_meminfo)(struct [sysinfo](https://elixir.bootlin.com/linux/v5.10.226/C/ident/sysinfo) *val)

linux/v5.10.226/source/include/linux/mm.h static inline unsigned long [totalram_pages](https://elixir.bootlin.com/linux/v5.10.226/C/ident/totalram_pages)(void)

linux/v5.10.226/source/include/asm-generic/atomic-long.h [atomic_long_read](https://elixir.bootlin.com/linux/v5.10.226/C/ident/atomic_long_read)(const [atomic_long_t](https://elixir.bootlin.com/linux/v5.10.226/C/ident/atomic_long_t) *v)

我开发是，就一句话，然后我自己琢磨，做到一半，他们想到哪个具体的场景就来说，做着着才能明确具体要求，还要我自己反复确认

![lxcfs](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202410151519973.webp)

# 容器资源视图隔离

[lxcfs 是什么？ lxcfs 实现对容器资源视图隔离的最佳实践容器技术提供了不同于传统虚拟机技术的环境隔离方式。 - 掘金 (juejin.cn)](https://juejin.cn/post/6847902216511356936)