[AOSP次级镜像搭建 | CC的博客 (iz4.cc)](https://blog.iz4.cc/tutorial/2021/07/AOSP%E6%AC%A1%E7%BA%A7%E9%95%9C%E5%83%8F%E6%90%AD%E5%BB%BA/)

[AOSP | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/)-建立次级镜像

一个例子

git://192.168.30.62/~~.git~~ 

对应 /snow/aosp/external/openssh/.git

```
root@aosp-vm:/snow/aosp/external/openssh# git daemon --reuseaddr --base-path=. --export-all --verbose
```

```shell
root@aosp-vm:/snow/tmp# git clone  git://192.168.30.62/.git
Cloning into '192.168.30.62'...
remote: Enumerating objects: 61388, done.
remote: Counting objects: 100% (61388/61388), done.
remote: Compressing objects: 100% (14093/14093), done.
remote: Total 61388 (delta 47402), reused 61080 (delta 47247), pack-reused 0
Receiving objects: 100% (61388/61388), 20.91 MiB | 39.29 MiB/s, done.
Resolving deltas: 100% (47402/47402), done.
Note: switching to 'afe267d03e6dc520359e8129c9ae31fd38229384'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false
```

如果你已经下载好了AOSP源码，并且想要将其设置为Git服务器，你可以按照以下步骤操作：

1. **进入你的AOSP源码目录** ：首先，你需要在终端中进入你存放AOSP源码的目录。例如，如果你的源码在 `~/aosp`目录下，你可以使用以下命令：

```
   cd ~/aosp
```

1. **运行git daemon** ：然后，你可以在该目录下运行 `git daemon`命令。这将启动一个Git服务器，其他电脑就可以通过网络从你的电脑上获取或更新Git仓库。你可以使用以下命令来运行 `git daemon`：

```
   git daemon --reuseaddr --base-path=. --export-all --verbose
```

   这个命令的参数解释如下：

* `--reuseaddr`：允许重用本地地址和端口。
* `--base-path=.`：设置Git服务器的根目录为当前目录。
* `--export-all`：导出所有仓库，而不仅仅是那些带有 `git-daemon-export-ok`文件的仓库。
* `--verbose`：显示详细的操作信息。

请注意，`git daemon`命令会使你的电脑变成一个Git服务器，这可能会有安全风险。在运行这个命令之前，你需要确保你的电脑的网络环境是安全的。

希望这个信息能帮助你。如果你有其他问题，欢迎随时向我提问。😊

    其他人可以通过Git的`clone`命令从你的电脑上拉取代码。他们需要知道你的电脑的IP地址和你的AOSP源码的路径。

例如，如果你的电脑的IP地址是 `192.168.1.100`，并且你的AOSP源码在你的电脑上的路径是 `~/aosp`，那么他们可以使用以下命令来拉取代码：

```
git clone git://192.168.1.100/aosp
```

这个命令会在他们的电脑上创建一个名为 `aosp`的目录，并将你的AOSP源码复制到这个目录中。

请注意，他们需要在他们的电脑上安装Git，并且他们的电脑需要能够通过网络访问你的电脑。

希望这个信息能帮助你。如果你有其他问题，欢迎随时向我提问。😊

    这是正常的。`git daemon`命令会在后台运行，并等待其他电脑的连接。当你看到 `Ready to rumble`这个信息时，表示 `git daemon`已经成功启动，并正在等待连接。

你可以在新的终端窗口中继续执行其他命令，`git daemon`会在后台运行。如果你想停止 `git daemon`，你可以在终端中按 `Ctrl+C`。

请注意，只有当其他电脑尝试从你的电脑上拉取代码时，`git daemon`才会有新的输出。如果没有其他电脑连接到你的电脑，`git daemon`就会一直等待，不会有新的输出。

希望这个信息能帮助你。如果你有其他问题，欢迎随时向我提问。😊
