# Relayz

sudo apt update && sudo apt upgrade -y

sudo apt -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker-archive-keyring.gpg

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

sudo apt update && sudo apt upgrade -y

sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
newgrp docker

docker version
docker compose version

reboot

sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget
curl -s https://api.github.com/repos/docker/compose/releases/latest | grep browser_download_url  | grep docker-compose-linux-x86_64 | cut -d '"' -f 4 | wget -qi -
chmod +x docker-compose-linux-x86_64
sudo mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose

docker-compose version
sudo usermod -aG docker $USER
newgrp docker

mkdir -p ~/.zsh/completion
curl -L https://raw.githubusercontent.com/docker/compose/master/contrib/completion/zsh/_docker-compose > ~/.zsh/completion/_docker-compose
fpath=(~/.zsh/completion $fpath)
autoload -Uz compinit && compinit -i
exec $SHELL -l


nano docker-compose.yml

version: '3'  
services:
  web:
    image: nginx:latest
    ports:
     - "8080:80"
    links:
     - php
  php:
    image: php:7-fpm


docker-compose up -d
docker-compose stop
docker-compose rm -f

docker run --rm -it  --name test alpine:latest /bin/sh
cat /etc/os-release
exit

docker-compose up -d
