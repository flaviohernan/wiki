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


## comandos docker



```console

docker exec -it <container_id_or_name> bash

```

```console
docker attach <container_id_or_name>


```

```console
docker run -it <image_name> /bin/bash


```

```console

To leave and keep the container running (Detach):
If you used docker run -it or docker attach, use the escape sequence:
Ctrl + P then Ctrl + Q
Note: This only works if the container was started with interactive (-i) and tty (-t) flags.

To leave and stop the container:
If you are in the container's main process (PID 1):
Type exit or press Ctrl + D.

To leave a docker exec session:
Type exit or press Ctrl + D. This will return you to your host terminal without stopping the container. 


```
