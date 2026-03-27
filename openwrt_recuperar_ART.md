
```console
root@DD-WRT:~# cat /proc/mtd
dev:    size   erasesize  name
mtd0: 00020000 00010000 "RedBoot"
mtd1: 003c0000 00010000 "linux"
mtd2: 002c0000 00010000 "rootfs"
mtd3: 00010000 00010000 "ddwrt"
mtd4: 00010000 00010000 "nvram"
mtd5: 00010000 00010000 "board_config"
mtd6: 00400000 00010000 "fullflash"
mtd7: 00020000 00010000 "fullboot"
```

Output TL-WR941ND V3.6
```console
root@OpenWrt:/# dmesg
...
[    0.592566] m25p80 spi0.0: found w25q32, expected m25p80
[    0.609229] m25p80 spi0.0: w25q32 (4096 Kbytes)
[    0.614279] 5 tp-link partitions found on MTD device spi0.0
[    0.619876] Creating 5 MTD partitions on "spi0.0":
[    0.624661] 0x000000000000-0x000000020000 : "u-boot"
[    0.632019] 0x000000020000-0x00000016fbc8 : "kernel"
[    0.639582] 0x00000016fbc8-0x0000003f0000 : "rootfs"
[    0.646613] mtd: device 2 (rootfs) set to be root filesystem
[    0.652313] 1 squashfs-split partitions found on MTD device rootfs
[    0.658552] 0x0000003a0000-0x0000003f0000 : "rootfs_data"
[    0.666722] 0x0000003f0000-0x000000400000 : "art"
[    0.673959] 0x000000020000-0x0000003f0000 : "firmware"

...
```
Listando as partições do roteador

```console
root@OpenWrt:/# cat /proc/mtd
dev:    size   erasesize  name
mtd0: 00020000 00010000 "u-boot"
mtd1: 0014fbc8 00010000 "kernel"
mtd2: 00280438 00010000 "rootfs"
mtd3: 00050000 00010000 "rootfs_data"
mtd4: 00010000 00010000 "art"
mtd5: 003d0000 00010000 "firmware"
```
Após localizar as partição identificada com **u-boot, art e firmware**, fazer um cópia para a pasta /tmp

```console
dd if=/dev/mtd0 of=/tmp/uboot.bin
```
```console
dd if=/dev/mtd4 of=/tmp/art.bin
```
```console
dd if=/dev/mtd5 of=/tmp/firmware.bin
```

Para descobrir o ip do roteador
```console
sudo netdiscover -S -f -i enp9s0
```

Em seguida fazer o backup usando scp, executar no PC

```console
ssh -oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedAlgorithms=+ssh-rsa root@192.168.1.1
```

Para copiar o arquivo no PC

```console
scp -O -oHostKeyAlgorithms=+ssh-rsa root@192.168.1.1:/tmp/art.bin ./
```



### https://openwrt.org/docs/guide-user/installation/restore_art_partition
### https://github.com/pepe2k/u-boot_mod?tab=readme-ov-file#building-on-linux
