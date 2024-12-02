cat /userdata/arm-agent/log/arm-agent/arm-agent_20241031_48911.log 

48911是pid

> [2024-10-31 17:58:40:177] [INFO] ==> insOnline {"cmdCode":"insOnline","data":[{"hostIp":"192.168.168.34","sn":0,"statusCd":"S01"},{"hostIp":"192.168.168.34","sn":1,"statusCd":"S01"},{"hostIp":"192.168.168.34","sn":2,"statusCd":"S01"},{"hostIp":"192.168.168.34","sn":3,"statusCd":"S01"}],"hostIp":"192.168.168.34","reqType":0,"requestId":"C0A8A822BF0F0734EEA30004"}

S01是在线，S02是不在线







设备离线排除
![image-20241127112024974](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202411271120727.png)

getHostInsInfo，然后超时，是业务平台那里有问题