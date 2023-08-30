# Relayz

> [Buradan](https://testnet.mynearwallet.com/) bir near testnet wallet'ı oluşturunuz.

```console
# Sunucu güncellemesini bir çok kez yapabiliriz şaşırmayalım bunun için:
sudo apt update && sudo apt upgrade -y

# Gerekli kütüphaneler ve docker kurulumu
sudo apt -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker-archive-keyring.gpg

# Tek komut ( \ ibaresi komutun devamını belirtir)
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

# Tekrar güncelleme
sudo apt update && sudo apt upgrade -y
```

```console
# Docker compose ve gerekli ayarlar.
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
newgrp docker

# Versionlar v2.24.4 veya benzer bir version çıkmalıdır. 
docker version
docker compose version

# reboot attıktan bir kaç dakika sonrasında sunucumuza giriş yapabilir
reboot
```

![image](https://github.com/ruesandora/Relayz/assets/101149671/708c90c9-8d66-45a6-bd0b-a499659b4ad1)

```console
# Güncellemler ve wget'i yüklüyoruz.
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget

# docker-compose ayarlamaları
curl -s https://api.github.com/repos/docker/compose/releases/latest | grep browser_download_url  | grep docker-compose-linux-x86_64 | cut -d '"' -f 4 | wget -qi -
chmod +x docker-compose-linux-x86_64
sudo mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose

docker-compose version

# exec komutuna kadar değişkendir problem yaşarsanız devam edebilirsiniz.
sudo usermod -aG docker $USER
newgrp docker

sudo curl -L https://raw.githubusercontent.com/docker/compose/master/contrib/completion/bash/docker-compose -o /etc/bash_completion.d/docker-compose
source /etc/bash_completion.d/docker-compose
```
```console
# nano ile docker-compose.yml içine giriyoruz
nano docker-compose.yml

# bu kısmı komple kopyalayıp yapıştırıp ctrl + x + y ile kaydedip çıkıyoruz.
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
```
```console
# docker testimizi yapıyoruz
docker-compose up -d
docker-compose stop
docker-compose rm -f

# Bu komuttan sonra açılan alpine konsoluna..
docker run --rm -it  --name test alpine:latest /bin/sh
# ..önce cat komutu daha sonra exit girip çıkıyoruz.
cat /etc/os-release
exit
# cat komutunda alpine logları gözükür.

# Docker kurulumumuz burada tamamlanıyor.
docker-compose up -d
```

```console
# Yukarıda dediğim gibi ram ve cpu maksimum seviye geliyor, 1 GB swap açalım sunucumuzu rahatlatalım.
sudo fallocate -l 1024M /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# htop ile 1024M Swp görüyorsanız htopta okey
```

```console
# gerekli dosyamızı indirip unzip yapalım.
wget https://relayz.io/resources/files/binaries/node-cli-x64.zip
sudo apt install unzip
unzip node-cli-x64.zip
# gerekli dizine girelim
cd output/x86_64-unknown-linux-gnu

# ruesandora.testnet kısmını kendi cüzdan isminizle değiştirip enterleyin.
./node-cli init ruesandora.testnet

# çıkan 2 seçenek olacak, ilkini seçip yeni private key oluşturun.
# komuttan sonra size bir link verecek (rengi pembe büyük ihtimalle), bunu oluşurduğunuz near cüzdanı sayfasında arama çubuğuna yapıştırın.
# Testnet cüzdanınızdan Relayz için size ait private key'i onaylayın.
# Sonrasında sunucunuza geri dönüp enter'e basın.

# Tebrikler.

# Hiç çalışmayan sunucunuz görselde ki gibi ram veya cpu yiyorsa sıkıntı yoktur
# Ayrıca buradan isminizi görebilirsiniz: https://relayz.io/network/nodes
```

![image](https://github.com/ruesandora/Relayz/assets/101149671/0c5255f9-ddfc-40e7-b01f-3ea11452c9a0)


