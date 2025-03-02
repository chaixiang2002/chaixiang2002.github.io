```
02-25 19:08:29.063  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:30.071  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:31.091  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:32.086  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:33.118  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:34.091  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:35.079  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:36.095  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:37.104  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
02-25 19:08:38.088  3204  3229 E app_process: Failed to clone handle: numFds=2, data[0]=44, data[1]=45
^C
130|d52a362c15a2:/ # ps -ef|grep 3204
shell         3204  3202 2 17:59:16 ?     00:01:36 app_process / com.genymobile.scrcpy.Server 2.1.1 video_bit_rate=4000000 log_level=verbose max_size=1080 lock_video_orientation=0 audio=false scid=00002663
shell         3219  3204 0 17:59:17 ?     00:00:00 app_process / com.genymobile.scrcpy.CleanUp AAAAAP////8CAAAA
root          7463  7432 10 19:08:45 pts/0 00:00:00 grep 3204
d52a362c15a2:/ # 

```

```
ls -l /proc/3204/fd
```

**文件描述符泄漏**

- 如果系统中存在文件描述符泄漏（即文件描述符没有被正确关闭），可能会导致文件描述符耗尽，从而无法分配新的文件描述符。



结果：1万个fd