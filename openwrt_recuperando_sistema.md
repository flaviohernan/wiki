## EAP225 Outdoor V3

# Resumo

Alguns firmwares oficiais estão dando problema aqui
só consegui openwrt-25.12.1-ath79-generic-tplink_eap225-outdoor-v3-squashfs-sysupgrade

factory e initramfs no 25, não funcionou.

Basicamente, usei o tftp do uboot para carregar 
openwrt-23.05.0-ath79-tplink_eap225-outdoor-v3-initramfs-kernel 
na RAM do roteador e inicializar.
Depois que o LuCi subiu fiz o upgrade do sistema usando 
openwrt-25.12.1-ath79-generic-tplink_eap225-outdoor-v3-squashfs-sysupgrade


# no Uboot

```console
setenv serverip 192.168.1.100; setenv ipaddr 192.168.1.1

```
```console
tftpboot 0x81000000 openwrt-23.05.0-ath79-tplink_eap225-outdoor-v3-initramfs-kernel.bin

```
** para testar a imagem rapidamente sem gravar na flash

```console
bootelf 0x81000000

```


** para gravar na flash executar esses dois comandos
```console
erase 0x9f040000 +$filesize

```
```console
cp.b 0x81000000 0x9f040000 $filesize

```
```console
reset
```




# No PC

```console
ssh-keygen -f '/home/flavio/.ssh/known_hosts' -R 192.168.1.1

```
```console
ssh -oPubkeyAcceptedAlgorithms=+ssh-rsa -o HostKeyAlgorithms=ssh-rsa -oKexAlgorithms=+diffie-hellman-group1-sha1 root@192.168.1.1

```
```console
scp -O -oHostKeyAlgorithms=+ssh-rsa ./openwrt-23.05.0-ath79-tplink_eap225-outdoor-v3factory.bin root@192.168.1.1:/tmp/

```

** No roteador
```console
sysupgrade -F /tmp/openwrt-23.05.0-ath79-tplink_eap225-outdoor-v3factory.bin
```

## Referencia

### https://forum.openwrt.org/t/bricked-eap225-wall-trying-to-flash-back-to-original-firmware/143061/25?page=2

### https://github.com/abusse/openwrt-eap225-outdoor
