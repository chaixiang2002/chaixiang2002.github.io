- git clone https://github.com/chaixiang2002/clash-for-linux.git





docker pull 加上代理

[【Docker】新手记一次为docker挂代理加速docker pull笔记 – 一桐のBlog (ytmc.fun)](http://ytmc.fun:55555/?p=146)

```toml
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:7890"
Environment="HTTPS_PROXY=http://127.0.0.1:7890"
Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.example.com"
```

vim /usr/lib/systemd/system/docker.service