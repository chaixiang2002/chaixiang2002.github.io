为什么gitlab上传的sshkey，每次pull 还有输入用户名和密码？

在 GitLab 中配置 SSH 密钥后，如果每次 `git pull` 仍然要求输入用户名和密码，可能是因为以下原因：

1. **远程仓库 URL 使用的是 HTTPS 而不是 SSH**：当你添加远程仓库时，如果 URL 是以 `https://` 开头的，那么 Git 会使用 HTTPS 而不是 SSH。因此，即使你已经配置了 SSH 密钥，它也不会生效。你可以检查并更改远程仓库的 URL 来解决这个问题。  
   - 检查当前远程仓库 URL:
     ```bash
     git remote -v
     ```
   - 如果看到的是 `https://`，可以将其更改为 SSH URL：
     ```bash
     git remote set-url origin git@gitlab.com:username/repository.git
     ```
   - 其中 `username/repository.git` 是你自己的仓库路径。

2. **SSH Key 未正确添加到 GitLab**：确保你已将正确的公钥 (`~/.ssh/id_rsa.pub`) 添加到 GitLab 的 SSH Key 设置中。如果公钥没有正确添加，GitLab 无法识别你的身份。
   
- 在 GitLab 中，进入 `Preferences` -> `SSH Keys`，然后确保你的公钥正确无误地粘贴到了那里。
   
3. **SSH Agent 没有运行或没有加载 SSH Key**：如果你没有在 SSH agent 中添加私钥，Git 无法使用它进行身份验证。你可以通过以下命令添加你的 SSH 私钥到 SSH agent：
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_rsa
   ```
   这将启动 SSH agent 并添加你的 SSH 私钥。

4. **SSH 配置文件设置不正确**：检查你的 SSH 配置文件 (`~/.ssh/config`) 是否正确配置了 GitLab 的设置。如果没有配置，可以添加类似如下的配置：
   ```
   Host gitlab.com
       HostName gitlab.com
       User git
       IdentityFile ~/.ssh/id_rsa
   ```

你可以先检查这些问题，确保 SSH 密钥配置正确后，再尝试 `git pull`。