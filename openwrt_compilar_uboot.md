# Criando o ambiente de compilação

## AR9331
```console
git clone https://github.com/mwarning/docker-openwrt-builder.git
cd docker-openwrt-builder
docker build -t openwrt_builder .
```

```console
mkdir ~/mybuild
chown -R user:user ~/ubootMod
docker run -v ~/ubootMod:/home/user -it openwrt_builder /bin/bash
```

# Compilando

```console

```

# Referencia
### https://github.com/pepe2k/u-boot_mod
### https://github.com/ranma/u-boot_mod
### https://github.com/unwireddevices/u-boot
### https://docs.u-boot.org/en/latest/build/index.html
