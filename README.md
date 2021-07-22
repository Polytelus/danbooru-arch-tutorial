# Installation of Danbooru on Arch Linux

## Setting up the program

#### Set your environment variables. Just copy and paste the commands below on your terminal.
```bash
export RUBY_VERSION=2.7.0

export GITHUB_INSTALL_SCRIPTS=https://raw.githubusercontent.com/danbooru/danbooru/master/script/install

export VIPS_VERSION=8.7.0
```

#### Those are the packages you'll have to install. I'd recommend an installation of yay as some of these require the AUR. And I also recommend that you install each package separately.
```bash
yay -S zlib glib2

yay -S base-devel automake openssl openssl-1.0 libxml2 libxslt ncurses readline6 readline7 readline flex bison ragel memcached libmemcached git curl libcurl-openssl-1.0 imagemagick sendmail nginx openssh redis coreutils ffmpeg mkvtoolnix npm

yay -S postgresql postgresql-libs

yay -S lcms2 libjpeg-turbo expat giflib libpng libexif

yay -S gcc
```
##### Install yarn and nodejs via **NPM**:
```bash
sudo npm install -g yarn
sudo npm install -g nodejs 
```
#### Now configure and build libvips. You can install the one from arch's repositories, but building it is better most of the time.
```bash
cd /tmp
wget -q https://github.com/libvips/libvips/releases/download/v$VIPS_VERSION/vips-$VIPS_VERSION.tar.gz
tar xzf vips-$VIPS_VERSION.tar.gz
cd vips-$VIPS_VERSION
./configure --prefix=/usr
make
make install
ldconfig
```
#### The next step is to set up an user. 
##### NOTE: You can install it on your current user, but please don't install as ROOT.
```bash
useradd -m danbooru
chsh -s /bin/bash danbooru
usermod -G danbooru,sudo danbooru
```
