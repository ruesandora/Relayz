<h1 align="center">Relayz</h1>

> Aktif olduğunuz her gün boyunca 10 RELY token alırsınız.

> Diğer sorular rehberin sonundadır.

> Önemli linkler: [Duyuru](https://t.me/RuesAnnouncement) - [Sohbet](https://t.me/RuesChat) -  [WP Kanalı](https://whatsapp.com/channel/0029VaBcj7V1dAw1H2KhMk34) - [Discord](https://discord.gg/huEG2JNj)

<h1 align="center">Donanım</h1>

> En muhim olanı internettir, [Hetzner](https://github.com/ruesandora/Hetzner) kullanıyorum.

```console
# Minimum
2 CPU 4 RAM - Debian 10 - 11 - 12

# Önerilen
4 CPU 8 RAM - Debian 11
```

<h1 align="center">Kurulum</h1>

> [Buradan](https://testnet.mynearwallet.com/) bir near testnet wallet'ı oluşturunuz.

> Daha sonra [buraya](https://relayz.io/welcome/ruesandora0.testnet) cüzdanı bağlayıp bir profil oluşturunuz.

```console
# Güncellemeler
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget

# swap alanı açalım
sudo fallocate -l 5240M /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# Gerekli kütüphaneler ve docker kurulumu
sudo apt -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common

# debian uyumlu dockeri indirelim.
curl -fsSL https://download.docker.com/linux/debian/gpg

# !! y seçeneğini seçiyoruz !!
sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker-archive-keyring.gpg

# Tek komut (enter çıkarsa enterleyin çıkmazsa no problem)
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

# Tekrar güncelleme
sudo apt update && sudo apt upgrade -y
```

<h1 align="center">Docker ayarlamaları</h1>

```console
# Docker compose ve gerekli ayarlar.
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
newgrp docker
```

```console
# Güncellemler ve wgeti yüklüyoruz.
sudo apt update && sudo apt upgrade -y

# docker-compose ayarlamaları
curl -s https://api.github.com/repos/docker/compose/releases/latest | grep browser_download_url  | grep docker-compose-linux-x86_64 | cut -d '"' -f 4 | wget -qi -
chmod +x docker-compose-linux-x86_64
sudo mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose

sudo mkdir -p /etc/bash_completion.d/
sudo curl -L https://raw.githubusercontent.com/docker/compose/master/contrib/completion/bash/docker-compose -o /etc/bash_completion.d/docker-compose
source /etc/bash_completion.d/docker-compose

echo -e "version: '3'\nservices:\n  web:\n    image: nginx:latest\n    ports:\n     - \"8080:80\"\n    links:\n     - php\n  php:\n    image: php:7-fpm" > docker-compose.yml
```

<h1 align="center">Docker testi</h1>

```console
# docker testimizi yapıyoruz
docker-compose up -d
docker-compose stop
docker-compose rm -f

# Bu komutu giriyoruz
docker run --rm -it  --name test alpine:latest /bin/sh

# açılan konsola bu iki komutu sırayla giriyoruz:
cat /etc/os-release
exit
```

<h1 align="center">Node'umuzu çalıştıralım</h1>

```console
# gerekli dosyamızı indirip unzip yapalım.
wget https://relayz.io/resources/files/binaries/node-cli-x64.zip
sudo apt install unzip
unzip node-cli-x64.zip

# izinleri verelim
mv node-cli-x64 node-cli
chmod +x node-cli

# ruesandora.testnet kısmını kendi cüzdan isminizle değiştirip enterleyin.
./node-cli init ruesandora.testnet

# çıkan 2 seçenek olacak, ilkini seçip yeni private key oluşturun.
# komuttan sonra size bir link verecek (rengi pembe büyük ihtimalle), bunu oluşurduğunuz near cüzdanı sayfasında arama çubuğuna yapıştırın.
# Daha sonra şifrenizi girip onaylama işlemlerini yapın
# 3-4 dakika kadar bekleyin 
# Sonrasında sunucunuza geri dönüp enter'e basın.

# Tebrikler.

# !! NOT: Sunucuzda ki .secret.json u yedekleyin lütfen !!
```

> Node'unuzu buradan [online](https://relayz.io/network/nodes) olup olmadığını kontrol edebilirsiniz.

> Soracağınız diğer sorular [burada](https://relayz.io/network/overview) mevcuttur.

> Relayz'ın [ortaklarından](https://foresightnews.pro/article/detail/26887) birisi Lifeform'dur, Lifeform'un en büyük yatırımcısı Binance Labsdır, bunuda bırakayım.

