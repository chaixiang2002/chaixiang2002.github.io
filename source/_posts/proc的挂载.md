根据你提供的代码，我们可以逐步分析其功能和等效的命令：

### 代码分析

```c
#define AID_READPROC 3009
#define MAKE_STR(x) __STRING(x)
CHECKCALL(mount("proc", "/proc", "proc", 0, "remount,hidepid=2,gid=" MAKE_STR(AID_READPROC)));
#undef MAKE_STR
```

1. **`#define AID_READPROC 3009`**: 这行定义了一个常量 `AID_READPROC`，它的值是 `3009`。
2. **`#define MAKE_STR(x) __STRING(x)`**: 这是一个宏定义，它将传入的参数 `x` 转换为字符串。因此，`MAKE_STR(AID_READPROC)` 会被替换为 `"3009"`。
3. **`CHECKCALL(mount("proc", "/proc", "proc", 0, "remount,hidepid=2,gid=" MAKE_STR(AID_READPROC)));`**: 这行代码调用 `mount()` 系统调用，重新挂载 `/proc` 文件系统，并应用以下选项：
   - `remount`: 表示重新挂载已经挂载的文件系统。
   - `hidepid=2`: 在 `/proc` 文件系统中，隐藏所有非当前进程拥有的 PID 文件。
   - `gid=3009`: 设置 `gid`（组 ID），这个值等于 `AID_READPROC`，即 `3009`。这通常意味着设置某个特定组的权限。
4. **`#undef MAKE_STR`**: 取消了宏 `MAKE_STR` 的定义。

### 等效的 Shell 命令

这段代码的等效命令是：

```sh
mount -o remount,hidepid=2,gid=3009 /proc
```

### 解释

- `remount`: 重新挂载一个已经挂载的文件系统。
- `hidepid=2`: 这是 `proc` 文件系统的挂载选项，表示隐藏非当前进程拥有的 PID 文件。
- `gid=3009`: 这个选项设置文件系统挂载时的组 ID，表示使用组 ID `3009`。

总结：代码等价于在 shell 中执行的 `mount` 命令，重新挂载 `/proc` 文件系统，并设置相应的挂载选项。

  mount -o remount,rw,hidepid=2  /proc  





### 问题的解决

```cpp
    CHECKCALL(mount("proc", "/proc", "proc", 0, "remount,hidepid=2,gid=" MAKE_STR(AID_READPROC)));   //参数错误
    CHECKCALL(mount("proc", "/proc", "proc", MS_REMOUNT, "hidepid=2,gid=" MAKE_STR(AID_READPROC)));  //参数正确

```

