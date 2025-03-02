改动点

```makefile
# add ssh server
PRODUCT_PACKAGES += \
        libssh \
        ssh \
        sftp \
        scp \
        sshd \
        sshd_config \
        ssh-keygen \
        start-ssh
PRODUCT_COPY_FILES += vendor/ntimespace/etc/security/authorized_keys:system/etc/security/authorized_keys.default
PRODUCT_COPY_FILES += vendor/ntimespace/commands/init/init.sshd.rc:system/etc/init/init.sshd.rc
```

device/ntimespace/ntimespace_prod.mk

external/openssh/start-ssh

vendor/ntimespace/commands



缺少某标签

```shell

root@snowrepo:/snow/android12-rk3588/out/target/product/rk3588_docker/vendor# readelf -a bin/sshd | grep stat
00000003d4c8  003400000402 R_AARCH64_JUMP_SL 0000000000000000 stat@LIBC + 0
00000003d4e8  002f00000402 R_AARCH64_JUMP_SL 0000000000000000 fstat@LIBC + 0
00000003da70  00de00000402 R_AARCH64_JUMP_SL 0000000000000000 ssh_packet_set_state + 0
00000003daa0  00ec00000402 R_AARCH64_JUMP_SL 0000000000000000 ssh_packet_get_state + 0
00000003df28  018b00000402 R_AARCH64_JUMP_SL 0000000000000000 lstat@LIBC + 0
00000003e000  01a900000402 R_AARCH64_JUMP_SL 0000000000000000 statvfs + 0
00000003e008  019a00000402 R_AARCH64_JUMP_SL 0000000000000000 fstatvfs + 0
    47: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND fstat@LIBC (2)
    52: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND stat@LIBC (2)
   222: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND ssh_packet_set_state
   236: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND ssh_packet_get_state
   395: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND lstat@LIBC (2)
   410: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND fstatvfs
   425: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND statvfs
root@snowrepo:/snow/android12-rk3588/out/target/product/rk3588_docker/vendor# strings bin/sshd | grep stat | grep act
root@snowrepo:/snow/android12-rk3588/out/target/product/rk
root@snowrepo:/snow/android12-rk3588/out/target/product/rk
root@snowrepo:/snow/android12-rk3588/out/target/product/rk3588_docker/vendor# strings bin/sshd | grep stat | grep active
strings: 'bin/sshd': No such file
root@snowrepo:/snow/android12-rk3588/out/target/product/rk3588_docker/vendor# 
```







![image-20250220180405559](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502201804066.png)