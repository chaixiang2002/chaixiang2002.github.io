aosp10的system/core/init/init.cpp

```cpp
static void InstallSignalFdHandler(Epoll* epoll) {
    // Applying SA_NOCLDSTOP to a defaulted SIGCHLD handler prevents the signalfd from receiving
    // SIGCHLD when a child process stops or continues (b/77867680#comment9).
    const struct sigaction act { .sa_handler = SIG_DFL, .sa_flags = SA_NOCLDSTOP };
    sigaction(SIGCHLD, &act, nullptr);

    sigset_t mask;
    sigemptyset(&mask);
    sigaddset(&mask, SIGCHLD);

    if (!IsRebootCapable()) {
        // If init does not have the CAP_SYS_BOOT capability, it is running in a container.
        // In that case, receiving SIGTERM will cause the system to shut down.
        sigaddset(&mask, SIGTERM);
    }

    if (sigprocmask(SIG_BLOCK, &mask, nullptr) == -1) {
        PLOG(FATAL) << "failed to block signals";
    }

    // Register a handler to unblock signals in the child processes.
    const int result = pthread_atfork(nullptr, nullptr, &UnblockSignals);
    if (result != 0) {
        LOG(FATAL) << "Failed to register a fork handler: " << strerror(result);
    }

    signal_fd = signalfd(-1, &mask, SFD_CLOEXEC);
    if (signal_fd == -1) {
        PLOG(FATAL) << "failed to create signalfd";
    }

    if (auto result = epoll->RegisterHandler(signal_fd, HandleSignalFd); !result) {
        LOG(FATAL) << result.error();
    }
}
```

这个函数 `InstallSignalFdHandler` 主要用于设置信号处理程序和信号阻塞机制，以便在进程中正确处理特定信号，尤其是在创建子进程时。

### 主要功能
1. **设置默认的 SIGCHLD 处理程序**：
   ```cpp
   const struct sigaction act { .sa_handler = SIG_DFL, .sa_flags = SA_NOCLDSTOP };
   sigaction(SIGCHLD, &act, nullptr);
   ```
   这段代码将 `SIGCHLD` 信号的处理程序设置为默认处理程序，并应用 `SA_NOCLDSTOP` 标志，以防止在子进程停止或继续时接收到该信号。

2. **创建信号集并阻塞信号**：
   ```cpp
   sigset_t mask;
   sigemptyset(&mask);
   sigaddset(&mask, SIGCHLD);
   ```
   创建一个空的信号集并将 `SIGCHLD` 信号添加到该集合中。接下来，可能会根据条件添加其他信号。

3. **判断是否在容器中运行**：
   ```cpp
   if (!IsRebootCapable()) {
       sigaddset(&mask, SIGTERM);
   }
   ```
   这里调用 `IsRebootCapable()` 函数来判断当前进程是否具有重启能力。如果返回 `false`，则表示进程可能在容器中运行。在这种情况下，`SIGTERM` 信号被添加到阻塞的信号集中。这是为了防止在容器中接收到 `SIGTERM` 导致系统关机。

4. **阻塞信号**：
   ```cpp
   if (sigprocmask(SIG_BLOCK, &mask, nullptr) == -1) {
       PLOG(FATAL) << "failed to block signals";
   }
   ```
   通过 `sigprocmask` 函数，阻塞上述信号集中的信号（`SIGCHLD` 和可能的 `SIGTERM`）。这意味着在当前进程中，这些信号在被处理之前不会被传递。

5. **注册 `pthread_atfork` 函数**：
   ```cpp
   const int result = pthread_atfork(nullptr, nullptr, &UnblockSignals);
   ```
   注册 `UnblockSignals` 函数，在进程进行 `fork` 时自动执行该函数以解除对这些信号的阻塞。

6. **创建信号文件描述符**：
   ```cpp
   signal_fd = signalfd(-1, &mask, SFD_CLOEXEC);
   ```
   创建一个信号文件描述符，用于接收阻塞的信号。`signalfd` 允许将信号作为文件事件处理。

7. **注册处理程序**：
   ```cpp
   if (auto result = epoll->RegisterHandler(signal_fd, HandleSignalFd); !result) {
       LOG(FATAL) << result.error();
   }
   ```
   将信号文件描述符注册到 `epoll` 事件循环中，以便能够处理相关的信号事件。

### 总结
- **`!IsRebootCapable()`**：用来判断当前进程是否具备重启能力，以决定是否在信号集内添加 `SIGTERM` 信号。若在容器中运行，通常不希望在收到 `SIGTERM` 时关机，因此将其添加到阻塞列表中。
- **`sigaddset(&mask, SIGTERM)`**：如果进程在容器中，则阻止 `SIGTERM` 信号，这样可以防止在不应终止时意外关闭系统。

这个函数的整体目的是在进程创建子进程时，确保信号处理的稳定性和可靠性，尤其是在容器环境中。



### 解决方案

```cpp
if (!IsRebootCapable()) {
    sigaddset(&mask, SIGTERM);//一定要执行这一句
}
```

