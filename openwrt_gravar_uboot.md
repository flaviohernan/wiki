# CPU / roteador
## AR9331 / WR720 16MB flash 64MB RAM

```console
sudo netdiscover -S -f -i enp9s0
```

```console
setenv ipaddr 192.168.1.111
setenv serverip 192.168.1.100
```

```console
setenv serverip 192.168.1.100; setenv ipaddr 192.168.1.1
tftpboot 0x81000000 uboot_for_tp-link_tl-wr720n_v3_CH.bin
```

Resposta do roteador
```console
dup 1 speed 1000
Using eth1 device
TFTP from server 192.168.1.100; our IP address is 192.168.1.1
Filename 'uboot_for_tp-link_tl-wr720n_v3_CH.bin'.
Load address: 0x81000000
Loading: #########################
done
Bytes transferred = 125952 (1ec00 hex)
```

```console
erase 0x9F000000 +0x20000
cp.b 0x81000000 0xbf020000 0x3c0000
reset
```

```console
First 0x0 last 0x1 sector size 0x10000
   1
Erased 2 sectors

```

```console
cp.b 0x81000000 0x9F000000 0x1ec00
```

```console

```

```console

```

# Referencias
