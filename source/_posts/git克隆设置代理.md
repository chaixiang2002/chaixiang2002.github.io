本机

```
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy https://127.0.0.1:7890
```

同网段

```
git config --global http.proxy http://192.168.30.176:7890
git config --global https.proxy https://192.168.30.176:7890
```



取消代理

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```



1. **SSH 代理配置**：

   - 如果你希望通过 SSH 使用代理，可以在 `~/.ssh/config` 文件中为 GitHub 配置代理。例如：

     plaintext

     复制

     ```
     Host github.com
         ProxyCommand nc -X connect -x 192.168.30.176:7890 %h %p
     ```

     这里 `nc` 是 `netcat` 工具，`-X connect` 表示使用 HTTP 代理，`-x` 指定代理地址和端口。