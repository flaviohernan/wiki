
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
root@OpenWrt:/# cat /proc/mtd
dev:    size   erasesize  name
mtd0: 00020000 00010000 "u-boot"
mtd1: 0014fbc8 00010000 "kernel"
mtd2: 00280438 00010000 "rootfs"
mtd3: 00050000 00010000 "rootfs_data"
mtd4: 00010000 00010000 "art"
mtd5: 003d0000 00010000 "firmware"
```

### https://openwrt.org/docs/guide-user/installation/restore_art_partition
