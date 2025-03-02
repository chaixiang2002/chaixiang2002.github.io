

ServiceManager的构建-核心代码结构（简化讲解版）

```c++
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/ioctl.h>
#include <unistd.h>
#include <linux/binder.h>

// 打开 Binder 驱动
int binder_open() {
    int fd = open("/dev/binder", O_RDWR);
    if (fd < 0) {
        perror("Failed to open binder driver");
        exit(1);
    }
    return fd;
}

// 设置自己为 Binder 上下文管理者
void binder_set_as_context_manager(int fd) {
    int ret = ioctl(fd, BINDER_SET_CONTEXT_MGR, 0);
    if (ret < 0) {
        perror("Failed to set as context manager");
        exit(1);
    }
}

// 处理 Binder 请求
void svcmgr_handler(struct binder_transaction_data *txn) {
    // 根据 txn->code 处理不同的请求
    switch (txn->code) {
        case SVC_MGR_ADD_SERVICE:
            // 处理服务注册请求
            break;
        case SVC_MGR_CHECK_SERVICE:
            // 处理服务查询请求
            break;
        default:
            // 其他请求
            break;
    }
}

// 进入 Binder 循环
void binder_loop(int fd) {
    struct binder_write_read bwr;
    while (1) {
        // 读取 Binder 驱动中的数据
        bwr.read_size = sizeof(bwr.read_buffer);
        bwr.read_consumed = 0;
        bwr.read_buffer = malloc(bwr.read_size);

        int ret = ioctl(fd, BINDER_WRITE_READ, &bwr);
        if (ret < 0) {
            perror("Failed to read from binder");
            exit(1);
        }

        // 解析并处理 Binder 请求
        struct binder_transaction_data *txn = (struct binder_transaction_data *)bwr.read_buffer;
        svcmgr_handler(txn);

        // 释放缓冲区
        free(bwr.read_buffer);
    }
}

int main() {
    // 1. 打开 Binder 驱动
    int fd = binder_open();

    // 2. 设置自己为 Binder 上下文管理者
    binder_set_as_context_manager(fd);

    // 3. 进入 Binder 循环，处理请求
    binder_loop(fd);

    return 0;
}
```

1. 打开/dev/binder驱动,ioctl方法发送BINDER_SET_CONTEXT_MGR命令，设置自己为管家
2. 进入binder_loop循环开始工作，不停的ioctl方法发送BINDER_WRITE_READ读写数据，把数据交给svcmgr_handler方法处理
3. SVC_MGR_ADD_SERVICE、SVC_MGR_CHECK_SERVICE、SVC_MGR_GET_SERVICE、SVC_MGR_LIST_SERVICE，不同的处理

核心结构体

struct binder_write_read bwr；



---

ServiceManager工作 核心代码结构（简化版）

```c++
// 服务信息结构体
struct svcinfo {
    const char *name;      // 服务名称
    struct binder_ref *ref; // Binder 引用
    struct svcinfo *next;  // 链表指针
};

// 全局服务列表
struct svcinfo *svclist = NULL;

// 请求处理方法
int svcmgr_handler(struct binder_state *bs, struct binder_transaction_data *txn) {
    switch (txn->code) {
        case SVC_MGR_ADD_SERVICE:
            // 处理服务注册请求
            add_service(txn->data, txn->offsets);
            break;
        case SVC_MGR_CHECK_SERVICE:
            // 处理服务查询请求
            check_service(txn->data, txn->offsets);
            break;
        default:
            // 其他请求
            break;
    }
    return 0;
}

// 注册服务
void add_service(const char *name, struct binder_ref *ref) {
    struct svcinfo *si = malloc(sizeof(*si));
    si->name = name;
    si->ref = ref;
    si->next = svclist;
    svclist = si;
}

// 查询服务
struct binder_ref *check_service(const char *name) {
    struct svcinfo *si = svclist;
    while (si) {
        if (strcmp(si->name, name) == 0) {
            return si->ref;
        }
        si = si->next;
    }
    return NULL;
}
```

he



```cpp
//service_manager,c
int main(){
    struct binder_state *bs;
    bs=binder_open(128*1024);
    binder_become_context_manager(bs);
    void *svcmgr_handler=BINDER_SERVICE_MANAGER;// 0?
    binder_loop(bs,svcmgr_handler);
}


struct binder_state *binder_open(unsigned mapsize)
{
    struct binder_state *bs;
    bs=malloc(sizeof(*bs));
    bs->fd=open("/dev/binder",O_RDWR);
    bs->mappsize=mapsize;
    bs->mapped=mmap(NULL,mapsize,PROT_READ,MAP_PRIVATE,bs->fd,0);
 	...
fail_map:
    close(bs->fd);
fail_open:
    free(bs);
    return 0;
}
```

- 被映射到进程空间的内存起始地址 由binder驱动决定
- 映射大小为128KB
- 映射区只读
- 映射区改变是私有
- 从文件起始地址开始映射



struct