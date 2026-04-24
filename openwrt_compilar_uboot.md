# Criando o ambiente de compilação

## AR9331
```console
git clone https://github.com/mwarning/docker-openwrt-builder.git
cd docker-openwrt-builder
docker build -t openwrt_builder .
```

```console
mkdir ~/ubootMod
chown -R 1000:1000 ~/ubootMod
docker run -v ~/ubootMod:/home/user -it openwrt_builder /bin/bash
```

Dentro do container 

Baixar o **OpenWrt Toolchain for AR71xx MIPS (32-bit)**
```console
wget http://downloads.openwrt.org/attitude_adjustment/12.09/ar71xx/generic/OpenWrt-Toolchain-ar71xx-for-mips_r2-gcc-4.6-linaro_uClibc-0.9.33.2.tar.bz2

tar -xvf OpenWrt-Toolchain-ar71xx-for-mips_r2-gcc-4.6-linaro_uClibc-0.9.33.2.tar.bz2
```

```console

git clone https://github.com/ranma/u-boot_mod.git
sudo chown -R user u-boot_mod/
cd u-boot_mod
mkdir-p toolchain
cp -r ~/OpenWrt-Toolchain-ar71xx-for-mips_r2-gcc-4.6-linaro_uClibc-0.9.33.2/toolchain-mips_r2_gcc-4.6-linaro_uClibc-0.9.33.2/* ./toolchain/
chmod +x toolchain/bin/*
```

```console
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install libc6:i386 libncurses5:i386 libstdc++6:i386 zlib1g:i386
```
acrescentar no Makefile 

```console
export PATH := /home/user/u-boot_mod/toolchain/bin:$(PATH)
export CROSS_COMPILE = mips-openwrt-linux-uclibc-
```

```console
sudo apt install default-jre
```

# Compilando

```console

```

# Referencia
### https://github.com/pepe2k/u-boot_mod
### https://github.com/ranma/u-boot_mod
### https://github.com/unwireddevices/u-boot
### https://docs.u-boot.org/en/latest/build/index.html
