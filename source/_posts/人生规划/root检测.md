这段代码中的 `stat("/system/bin/su", &info)` 主要用于检查文件或符号链接 `/system/bin/su` 是否存在并且是一个符号链接。下面是对这部分代码的详细解释：

### `stat` 函数

`stat` 是一个系统调用，用于获取文件的状态信息。它的原型是：

```cpp
int stat(const char *pathname, struct stat *statbuf);
```

- **`pathname`**：文件或目录的路径（这里是`/system/bin/su`）。
- **`statbuf`**：指向 `struct stat` 结构体的指针，用于存储返回的文件状态信息。

`stat` 函数调用会返回 0 表示成功，如果失败会返回 -1，并设置 `errno` 以指示错误原因。

### `struct stat`

`struct stat` 是一个包含文件状态信息的结构体，其定义如下：

```cpp
struct stat {
    dev_t     st_dev;     // 设备ID
    ino_t     st_ino;     // inode号码
    mode_t    st_mode;    // 文件类型和权限
    nlink_t   st_nlink;   // 硬链接数
    uid_t     st_uid;     // 文件所有者
    gid_t     st_gid;     // 文件所在组
    dev_t     st_rdev;    // 设备类型（如果是设备文件）
    off_t     st_size;    // 文件大小（字节）
    time_t    st_atime;   // 上次访问时间
    time_t    st_mtime;   // 上次修改时间
    time_t    st_ctime;   // 上次状态变化时间
    // 其他平台相关的字段...
};
```

### `st_mode` 字段

`st_mode` 是 `stat` 结构体中的一个字段，用于存储文件的类型和权限信息。`st_mode` 中的高位包含文件类型信息（普通文件、目录、符号链接等），低位包含文件的访问权限信息（读、写、执行等）。

### `S_ISLNK` 宏

`S_ISLNK` 是一个宏，用来检查 `st_mode` 是否表示一个符号链接。它的定义是：

```cpp
#define S_ISLNK(m) (((m) & S_IFMT) == S_IFLNK)
```

- `S_IFMT` 是文件类型的掩码。
- `S_IFLNK` 表示符号链接类型。

通过 `S_ISLNK(info.st_mode)`，我们可以检查文件是否是符号链接。

### 代码解析

```cpp
if (stat("/system/bin/su", &info) == 0 && S_ISLNK(info.st_mode)) {
    success = true;
    break;
}
```

1. **`stat("/system/bin/su", &info)`**：调用 `stat` 获取 `/system/bin/su` 文件的信息。如果 `stat` 返回 0，说明文件存在，并且其状态信息已经成功保存在 `info` 结构体中。
2. **`S_ISLNK(info.st_mode)`**：检查 `info.st_mode` 是否表示一个符号链接。如果 `/system/bin/su` 是一个符号链接，这个条件将为真。
3. **`success = true;`**：如果上述两个条件都满足，表示 `/system/bin/su` 已经存在并且是一个符号链接，因此设置 `success = true`，表示操作成功。
4. **`break;`**：退出 `while` 循环，因为我们已经成功创建了符号链接，后续的重试逻辑不再需要执行。

### 总结

这段代码主要用于验证 `/system/bin/su` 是否成功地作为符号链接存在，且指向正确的位置。`stat` 用于获取文件的详细信息，而 `S_ISLNK` 用于判断文件是否是符号链接。如果符号链接正确创建（或已经存在），则将 `success` 设置为 `true`，并跳出循环。