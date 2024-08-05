1af6e2c93411:/ # /system/xbin/curl cip.cc
IP      : 206.237.81.228
地址    : 美国  美国

数据二  : 美国 | Cogent

数据三  : 美国 | 科进

URL     : http://www.cip.cc/206.237.81.228
1af6e2c93411:/ # ^D
root@antdock:~# dexe.sh 1^C
root@antdock:~# docker exec -it android_0 /system/xbin/curl cip.cc
IP      : 206.237.81.228
地址    : 美国  美国

数据二  : 美国 | Cogent

数据三  : 美国 | 科进

URL     : http://www.cip.cc/206.237.81.228
root@antdock:~# docker exec -it android_1 /system/xbin/curl cip.cc
IP      : 38.102.188.3
地址    : 美国  美国

数据二  : 美国 | 华盛顿Cogent通信公司

数据三  : 美国加利福尼亚 | 科进

URL     : http://www.cip.cc/38.102.188.3
root@antdock:~# docker exec -it android_2 /system/xbin/curl cip.cc
IP      : 38.102.188.3
地址    : 美国  美国

数据二  : 美国 | 华盛顿Cogent通信公司

数据三  : 美国加利福尼亚 | 科进

URL     : http://www.cip.cc/38.102.188.3
root@antdock:~# 