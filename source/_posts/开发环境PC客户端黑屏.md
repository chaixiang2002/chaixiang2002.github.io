1. 安卓客户端正常能看，但是pc客户端黑屏
2. agent日志 容器 和stream都正常
3. stream日志没有报错



实际原因：

![image-20250227175148067](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502271751859.png)

![image-20250227175229746](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502271752502.png)

ssl证书不对

安卓客户端不校验，ssl证书故stream正常推流

PC客户端必须校验，stream拒绝推流







---

如何调试客户端

65535

![image-20250228104044972](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502281040245.png

![image-20250228104142774](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202502281041831.png)