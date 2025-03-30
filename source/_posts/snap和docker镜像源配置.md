snap安装的应用和apt安装的应用不同。

snap安装的应用是在一个沙盒中，默认的配置文件也会普通应用的配置文件不同





### 普通安装设置docker国内镜像源

针对Docker客户端版本大于 1.10.0 的用户

您可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://docker.m.daocloud.io"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

### snap安装设置docker国内镜像源

Snap 应用的配置文件通常位于 `/var/snap/docker/current/config/`，但直接编辑可能不生效。建议优先使用 `snap set` 命令。
若仍需手动操作：

1. **定位 Docker 的 Snap 配置目录**

   bash

   复制

   ```
   cd /var/snap/docker/current/config/
   ```

2. **编辑 `daemon.json` 文件**

   bash

   复制

   ```
   sudo nano daemon.json
   ```

   添加以下内容：

   json

   复制

   ```
   {
     "registry-mirrors": ["https://your_code.mirror.aliyuncs.com"]
   }
   ```

3. **重启 Docker 服务**

   bash

   复制

   ```
   sudo snap restart docker
   ```





如何验证docker镜像地址是否有效

```
  204  curl -I https://docker.mirrors.ustc.edu.cn/v2/
  208  curl -I https://mirror.baidubce.com
  209  curl -I baidu.com
  210  curl -I https://docker.mirrors.ustc.edu.cn
  211  curl -I https://hub-mirror.c.163.com
  213  curl -I https://jm1vrbet.mirror.aliyuncs.com
  238  curl -I https://docker-hub-mirror.obs.cn-north-1.myhuaweicloud.com
  240  curl -I https://docker.m.daocloud.io

403错误，说明不能用
root@vm:~# curl -I https://jm1vrbet.mirror.aliyuncs.com
HTTP/2 403 
date: Sat, 08 Mar 2025 13:42:58 GMT
content-type: text/plain
content-length: 189

404错误，说明不能用
root@vm:~# curl -I https://docker-hub-mirror.obs.cn-north-1.myhuaweicloud.com
HTTP/1.1 404 Not Found
Server: OBS
Date: Sat, 08 Mar 2025 13:44:26 GMT
Content-Length: 0
Connection: close
x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
x-amz-request-id: 000001957600000484C853BCAF93588A
x-amz-error-code: NoSuchBucket
x-amz-error-message: The specified bucket does not exist
x-amz-error-detail-BucketName: docker-hub-mirror
x-amz-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

302 代表可以VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV|
root@vm:~# curl -I https://docker.m.daocloud.io
HTTP/2 302 
server: nginx
date: Sat, 08 Mar 2025 13:46:41 GMT
content-type: text/html
content-length: 138
location: https://github.com/DaoCloud/public-image-mirror
```

目前 https://docker.m.daocloud.io是可以用的