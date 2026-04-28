# Criando o ambiente de compilação

## Instalando docker
* https://docs.docker.com/engine/install/ubuntu/
* https://docs.docker.com/engine/install/debian/

## Baixando o container do openwrt

```console
git clone https://github.com/mwarning/docker-openwrt-builder.git
cd docker-openwrt-builder
docker build -t openwrt_builder .
```

```console
mkdir ~/mybuild
chown -R 1000:1000 ~/mybuild
docker run -v ~/mybuild:/home/user -it openwrt_builder /bin/bash
```

Dentro do container executar

```console
git clone -b v24.10.6 --single-branch https://github.com/openwrt/openwrt
sudo chown -R user openwrt/
cd openwrt
```

```console
./scripts/feeds update -a
./scripts/feeds install -a
```


```console


```

```console


```

```console


```

```console


```
