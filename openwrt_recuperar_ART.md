
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
## Output WR841N V9.1
```console
 CPU0 revision is: 00019374 (MIPS 24Kc)
 SoC: Qualcomm Atheros QCA9533 ver 1 rev 1
 m25p80 spi0.0: found w25q32, expected m25p80
 m25p80 spi0.0: w25q32 (4096 Kbytes)
 5 tp-link partitions found on MTD device spi0.0
 Creating 5 MTD partitions on "spi0.0":
 0x000000000000-0x000000020000 : "u-boot"
 0x000000020000-0x00000016dde0 : "kernel"
 0x00000016dde0-0x0000003f0000 : "rootfs"
 mtd: device 2 (rootfs) set to be root filesystem
 1 squashfs-split partitions found on MTD device rootfs
 0x0000003a0000-0x0000003f0000 : "rootfs_data"
 0x0000003f0000-0x000000400000 : "art"
 0x000000020000-0x0000003f0000 : "firmware"
 libphy: Fixed MDIO Bus: probed
 libphy: ag71xx_mdio: probed
 ag71xx-mdio.1: Found an AR934X built-in switch

```

## Output HLK-RM65
```console
    spi-nand spi0.0: Macronix SPI NAND was found.
    spi-nand spi0.0: 128 MiB, block size: 128 KiB, page size: 2048, OOB size: 64
    5 fixed-partitions partitions found on MTD device nmbm_spim_nand
    Creating 5 MTD partitions on "nmbm_spim_nand":
    0x000000000000-0x000000100000 : "BL2"
    0x000000100000-0x000000180000 : "u-boot-env"
    0x000000180000-0x000000380000 : "Factory"
    0x000000380000-0x000000580000 : "FIP"
    0x000000580000-0x000004580000 : "ubi"
```

```console
root@HiLink:/# cat /proc/mtd
dev:    size   erasesize  name
mtd0: 08000000 00020000 "spi0.0"
mtd1: 00100000 00020000 "BL2"
mtd2: 00080000 00020000 "u-boot-env"
mtd3: 00200000 00020000 "Factory"
mtd4: 00200000 00020000 "FIP"
mtd5: 04000000 00020000 "ubi"
```

## Output TL-WR1043ND
```console
    m25p80 spi0.0: s25sl064a (8192 Kbytes)
    Searching for RedBoot partition table in spi0.0 at offset 0x7e0000
    Searching for RedBoot partition table in spi0.0 at offset 0x7f0000
    No RedBoot partition table detected in spi0.0
    spi0.0: no WRT160NL signature found
    Creating 5 MTD partitions on "spi0.0":
    0x000000000000-0x000000020000 : "u-boot"
    0x000000020000-0x000000160000 : "kernel"
    0x000000160000-0x0000007f0000 : "rootfs"
    mtd: partition "rootfs" set to be root filesystem
    mtd: partition "rootfs_data" created automatically, ofs=2A0000, len=550000
    0x0000002a0000-0x0000007f0000 : "rootfs_data"
    0x0000007f0000-0x000000800000 : "art"
    0x000000020000-0x0000007f0000 : "firmware"
```
## Output TL-WR710N V1

```console
spi-nor spi0.0: w25q128 (16384 Kbytes)
3 fixed-partitions partitions found on MTD device spi0.0
OF: Bad cell count for /ahb/spi@1f000000/flash@0/partitions
OF: Bad cell count for /ahb/spi@1f000000/flash@0/partitions
Creating 3 MTD partitions on "spi0.0":
0x000000000000-0x000000020000 : "u-boot"
OF: Bad cell count for /ahb/spi@1f000000/flash@0/partitions
0x000000020000-0x0000007f0000 : "firmware"
2 tplink-fw partitions found on MTD device firmware
Creating 2 MTD partitions on "firmware":
0x000000000000-0x000000287fff : "kernel"
mtd: partition "kernel" doesn't end on an erase/write block -- force read-only
0x000000288000-0x0000007d0000 : "rootfs"
mtd: setting mtd3 (rootfs) as root device
1 squashfs-split partitions found on MTD device rootfs
0x000000660000-0x0000007d0000 : "rootfs_data"
0x0000007f0000-0x000000800000 : "art"

```



## Output TL-WR941ND V3.6
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

Para descobrir o ip do roteador
```console
sudo netdiscover -S -f -i enp9s0
```

Para acessar o roteador é necessário usar o **ssh**, executar no PC.

```console
ssh -oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedAlgorithms=+ssh-rsa root@192.168.1.1
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



Para copiar o arquivo no PC

```console
scp -O -oHostKeyAlgorithms=+ssh-rsa root@192.168.1.1:/tmp/*.bin ./
```

Para ignorar a chave privada

```console
scp -O -oHostKeyAlgorithms=+ssh-rsa -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null root@192.168.1.1:/tmp/*.bin ./
```

## update uboot

### serial

```console
loady 0x81000000
```

no PC usar o **minicom**, com a opção de envio de arquivo usando o **ymodem**

```console
Welcome to minicom 2.9

OPTIONS: I18n 
Port /dev/ttyUSB0, 19:58:41

Press CTRL-A Z for help on sp+-[Upload]--+
                             | zmodem    |
                             | ymodem    |
                             | xmodem    |
                             | kermit    |
                             | ascii     |
                             +-----------+















CTRL-A Z for help | 115200 8N1 | NOR | Minicom 2.9 | VT102 | Offline | ttyUSB0                                          
```
Na tela seguinte, colocar o caminho completo do arquivo que se deseja enviar.

:warning: Esse método de envio é bastante lento, logo só é recomendável para arquivos pequenos, tais como **uboot** e **art**.

```console
Welcome to minicom 2.9+-------------------[Select one or more files for upload]-------------------+
                      |Directory: /root                                                           |
OPTIONS: I18n         | [..]                                                                      |
Port /dev/ttyUSB0, 19:| [.cache]                                                                  |
                      | [.dbus]                                                                   |
Press CTRL-A Z for hel| [.launchpadlib]                                                           |
                      | [.putty]                                                                  |
                      | [.ssh]                                                                    |
                      | [snap]                                                                    |
                      | .bashrc        +-----------------------------------------+                |
                      | .lesshst       |No file selected - enter filename:       |                |
                      | .linssid.prefs |>                                        |                |
                      | .profile       +-----------------------------------------+                |
                      | .viminfo                                                                  |
                      | minicom.log                                                               |
                      |                                                                           |
                      |                                                                           |
                      |                                                                           |
                      |                                                                           |
                      |                                                                           |
                      |                                                                           |
                      |                                                                           |
                      |              ( Escape to exit, Space to tag )                             |
                      +---------------------------------------------------------------------------+

                                     [Goto]  [Prev]  [Show]   [Tag]  [Untag] [Okay]                

CTRL-A Z for help | 115200 8N1 | NOR | Minicom 2.9 | VT102 | Offline | ttyUSB0                                          
```

### tftp


```console
tftpboot 0x81000000 u-boot_mod.20151021.tl-wr1043nd.bin

```
### gravando na memória flash

```console
cp.b 0xbf01fc00 0x8101fc00 0x400
erase 0xbf000000 +0x20000
cp.b 0x81000000 0xbf000000 0x20000
```
Note that the first "cp.b" copies the 0x400 bytes of mac address, board type and WPS pin so it is not lost.
Once this is done, you should see this on reboot:

## update system
```console
setenv serverip 192.168.1.100; setenv ipaddr 192.168.1.1
tftpboot 0x81000000 openwrt-18.06.9-ar71xx-tiny-tl-wr941nd-v3-squashfs-factory.bin
erase.b 0xbf020000 +0x3c0000
cp.b 0x81000000 0xbf020000 0x3c0000
reset
```

### https://openwrt.org/pt-br/toh/tp-link/tl-wr941nd
### https://openwrt.org/toh/tp-link/tl-wr941nd

### https://openwrt.org/docs/guide-user/installation/restore_art_partition
### https://github.com/pepe2k/u-boot_mod?tab=readme-ov-file#building-on-linux

### https://openwrt.org/toh/tp-link/tl-wa901nd

### https://openwrt.org/toh/tp-link/tl-mr3040
### https://openwrt.org/toh/gl.inet/gl-ar150


Uboot 

### https://forum.archive.openwrt.org/viewtopic.php?id=43237&p=19
### https://github.com/ranma/u-boot_mod/tree/tl-wr1043nd
### https://grenville.wordpress.com/2011/11/24/serial-console-tplink-wr1043nd/

hack
### https://hackaday.io/project/202585-wi-fi-router-autopsy/log/239101-chapter-1-recovering-the-passwords
### https://hackaday.io/project/202585-wi-fi-router-autopsy/log/239228-chapter-2-firmware-tour
### https://hackaday.io/project/202585-wi-fi-router-autopsy/log/239494-chapter-3-jtag

### https://forum.archive.openwrt.org/viewtopic.php?id=50765

### https://github.com/gwlim/Openwrt_Firmware
### https://github.com/gwlim/openwrt-sfe-flowoffload-ath79
### https://openwrt.org/toh/linksys/wrt160nl
### https://openwrt.org/toh/linksys/e2100l
### https://openwrt.org/toh/netgear/wnr2000
### https://openwrt.org/toh/tp-link/tl-wr841nd
### https://openwrt.org/toh/tp-link/tl-wr1043nd
### https://forum.archive.openwrt.org/viewtopic.php?id=32512

# MODS
### https://openwrt.org/toh/tp-link/tl-wr703n
### https://forum.archive.openwrt.org/viewtopic.php?id=28343
### https://forum.archive.openwrt.org/viewtopic.php?id=32512
### https://forum.archive.openwrt.org/viewtopic.php?id=18279
