   97  curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
   98  curl https://www.google.com
   99  sudo apt-get update
  100  sudo apt-get install --reinstall ca-certificates
  101  curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/debian/gpg | sudo tee /etc/apt/trusted.gpg.d/docker.asc
  102  sudo apt-get update
  103  sudo apt-get install docker-ce
  104  sudo apt-get remove docker docker-engine docker.io containerd runc  # 如果已有其他版本的 Docker
  105  sudo mkdir -p /etc/apt/keyrings
  106  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc
  107  echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  108  sudo apt-get update
  109  sudo apt-get install docker-ce
  110  sudo docker --version
  111  history