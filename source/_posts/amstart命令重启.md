09-06 01:17:41.034076 53127 53795 I ActivityManager: Sending shutdown broadcast...
09-06 01:17:41.034165 53127 53795 I ActivityManager: Shutting down activity manager...

### `am restart`

- **全称**：`am` 是 Activity Manager 的缩写，`restart` 是其中的一个子命令。
- **作用**：`am restart` 主要是重启 Android 的 **System Server**，而不是整个设备。这相当于重新启动 Android 系统的核心服务，但不会重启 Linux 内核。
- **效果**：执行 `am restart` 后，Android 系统的界面会短暂变黑然后重新加载，类似于“系统刷新”。这种重启方式不会影响正在运行的 Linux 内核和底层硬件初始化，但可能会重启所有系统级应用和服务。
- **应用场景**：这种方式常用于开发和测试时，快速重启系统服务以应用更改（例如 framework 修改），而不必等待设备完全重启。

### 2. `reboot`

- **全称**：Linux 系统命令，直接调用底层的内核来进行重启操作。
- **作用**：`reboot` 是完全的重启，会关闭所有正在运行的应用程序、服务，重新启动操作系统和硬件。
- **效果**：该命令执行后，设备会从硬件级别重新启动，包括 BIOS/Bootloader，内核重新加载，系统启动。这是一次完整的设备重启，相当于“冷启动”。
- **应用场景**：设备需要彻底重启以解决系统问题、应用系统更新，或者完全重置运行状态时使用。