- [Magisk移植 - 梦过无声 - 博客园 (cnblogs.com)](https://www.cnblogs.com/tangshunhui/p/17136867.html)
- [android|Magisk注入Zygisk的过程-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/1330934)

[Magisk support · Issue #207 · remote-android/redroid-doc (github.com)](https://github.com/remote-android/redroid-doc/issues/207)

https://ivonblog.com/posts/magisk-hide-root/

[Magisk support · Issue #207 · remote-android/redroid-doc (github.com)](https://github.com/remote-android/redroid-doc/issues/207)



[Magisk过SafetyNet谷歌验证 - 哔哩哔哩 (bilibili.com)](https://www.bilibili.com/read/cv12047253/)

### prepare();

xmkdir("/data", 0755);
    xmount("tmpfs", "/data", "tmpfs", 0, "mode=755");

    cp_afc("/init", "/data/magiskinit");
    cp_afc("/.backup", "/data/.backup");
    cp_afc("/overlay.d", "/data/overlay.d");

### patch_rw_root();

    mount_list.emplace_back("/data");  //添加到mount_list,等下要umount的
    mkdir("/root", 0777);
    clone_attr("/sbin", "/root");
    link_path("/sbin", "/root");

    // 给init.rc 打补丁,添加magisk的开机启动
    patch_init_rc("/init.rc", "/init.p.rc", "/sbin");
    rename("/init.p.rc", "/init.rc");
    ...
    // 创建/magisk-tmp
    // 找到分区块,在/data/.magisk/block下mknod, 然后挂载到/data/.magisk/mirror
    // 将/data bind 挂载到/magisk-tmp , /sbin挂载为tmpfs ,将/magisk-tmp再bind /sbin 套娃
    xmkdir(PRE_TMPDIR, 0);
    setup_tmp(PRE_TMPDIR);
    chdir(PRE_TMPDIR);
    ...
    chdir("/");

    // Dump magiskinit as magisk
    cp_afc(REDIR_PATH, "/sbin/magisk");

exec_init();

for (auto &p : reversed(mount_list)) {
         if (xumount2(p.data(), MNT_DETACH) == 0)
             LOGD("Unmount [%s]\n", p.data());
    }
    execv("/init", argv);
    exit(1);
