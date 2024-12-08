# manage-shell

1. 是 "-"   不是 "_"

2. .env

   ```yml
   MACVLAN_GATEWAY=192.168.168.1
   MACVLAN_SUBNET=192.168.168.0/24
   
   IP_1=192.168.168.51
   ...
   ```

3. template/android_network.yml

   ```yml
   # version: "3.8"
   networks:
     android-bri:
       ipam:
         driver: default
         config:
           - subnet: "172.20.0.0/16"
       name: android-bri
       driver_opts:
         com.docker.network.bridge.name: android-bri
     android-mac:
       driver: macvlan
       ipam:
         config:
           - subnet: ${MACVLAN_SUBNET}
             gateway: ${MACVLAN_GATEWAY}
       name: android-mac
       driver_opts:
         parent: eth0
   ```

   



---

# agent看问题

1. 

```
[2024-12-02 19:55:32:396] [INFO] WDeviceManageMgr::Init() androidctl_retcode.json failed
找不到文件，可能是manage-shell的目录错了，是 "-"   不是 "_"

```

2. conf/arm-agentConfig.json

   ```json
       "Server": {
           "ProxyIp": "192.168.168.167",
           "ProxyPort": 8000
       },
   ```

   可能是业务平台的服务器ip错了，开发环境、测试环境

3. 排除容器问题还是业务平台的问题

   ```c++
   [2024-12-02 18:11:07:405] [INFO] WDeviceManageInfo::Init m_IsOnline_Android:1  m_IsOnline_Stream:1
   ```

   1代表正常，其中安卓容器是判断bin/manage-shell/android_ctl.sh的startup_android（）的get_android_stat（）

   health_status=$(docker inspect --format='{{.State.Status}}' "$container_name")

4. 业务平台没有返回值

![image-20241203140526719](https://cdn.jsdelivr.net/gh/chaixiang2002/repo/picgo/img/202412031405766.png)

# stream看问题

1. 设备认证token无效

   streamlog

   ```yml
   [2024-12-02 18:16:21.191 42761][CurlSession][INFO] Post code is 200, response_ is : {"code":101022,"msg":"鉴权失败，deviceToken已过期","ts":"1733134581197"}
   ```

   conf/arm-streamConfig0.json,鉴权服务器设置错了，114是开发

   ```json
   "BussPlatformUrl":"http://192.168.168.114/cpCgw/sub/ins/ctrl/auth",
           "PollPlatformUrl":"http://192.168.168.114/cpCgw/sub/ins/ctrl/auth_token",
   ```

2. 协议错了，没有协议

   ```json
   "ChainFile": "../conf/ssl_certificate/sandbox.ntimespace.com_bundle.crt",
   "KeyFile": "../conf/ssl_certificate/sandbox.ntimespace.com.key",
   ```

   conf/ssl_certificate/sandbox.ntimespace.com_bundle.crt

   conf/ssl_certificate/sandbox.ntimespace.com.key

