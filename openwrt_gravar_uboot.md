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
tftpboot 0x81000000 uboot.bin
```

```console
erase.b 0xbf020000 +0x3c0000
cp.b 0x81000000 0xbf020000 0x3c0000
reset
```

```console

```

```console

```

```console

```

```console

```

# Referencias
