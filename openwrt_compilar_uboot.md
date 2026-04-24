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

```console
git clone https://github.com/pepe2k/u-boot_mod.git
sudo chown -R user u-boot_mod/
cd u-boot_mod
```
Baixar o **OpenWrt Toolchain for AR71xx MIPS (32-bit)**
```console
wget https://downloads.openwrt.org/chaos_calmer/15.05.1/ar71xx/generic/OpenWrt-SDK-15.05.1-ar71xx-generic_gcc-4.8-linaro_uClibc-0.9.33.2.Linux-x86_64.tar.bz2

tar -xvf OpenWrt-SDK-15.05.1-ar71xx-generic_gcc-4.8-linaro_uClibc-0.9.33.2.Linux-x86_64.tar.bz2
```

# Compilando

```console

```

# Referencia
### https://github.com/pepe2k/u-boot_mod
### https://github.com/ranma/u-boot_mod
### https://github.com/unwireddevices/u-boot
### https://docs.u-boot.org/en/latest/build/index.html
