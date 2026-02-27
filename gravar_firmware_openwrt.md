# Tutorial para gravar firmware por TFTP
Será usado o rotreador TL-WR720N CPU Atheros AR9331-AL3A

Foi adicionado 32MB de RAM (K4D551638-TC500) e 4MB de flash. A placa original usar 16MB e 2MB.

---
The Qualcomm Atheros AR9331 SoC typically maps its memory in the MIPS
kseg0 address space, with the following standard memory mapping: 

    DDR SDRAM (RAM): Starts at 0x80000000 (physical 0x00000000).
    SPI Flash Memory: Typically mapped to 0x9F000000 (physical 0x1F000000). 

Memory and Address Details

    Address Space: The AR9331 uses a 32-bit architecture where the physical a
    ddress 0x00000000 is mapped to 0x80000000 in the kernel virtual space (kseg0).
    Bootloader: U-Boot usually relocates itself to the top of the RAM area.
    Typical Configuration: The AR9331 is often paired with 64 MB of DDR2 RAM and 
    16 MB of Flash memory, though some boards use 32 MB RAM or 8 MB Flash.
    Flash Mapping: The SPI flash, which holds the bootloader and firmware, 
    is commonly found at 0x9F000000. 

Common Memory Map (Standard 16MB Flash / 64MB RAM)

    Flash (Start): 0x9F000000
    Flash (End): 0x9FFFFFFF (for 16MB)
    DDR RAM (Start): 0x80000000
    DDR RAM (End): 0x83FFFFFF (for 64MB)
---

## Comandos
```console
sudo netdiscover -S -f -i enp9s0
```

```console
sudo apt install tftp-hpa
sudo systemctl restart tftpd-hpa
sudo ufw allow tftp
sudo ufw allow 69/udp
```

```console
sudo apt install dhex
```



## Create a working image

In order to replace the 4mb flash chip with a 16mb one you may at first dump two important partitions:

64k u-boot + 64k data section: at the beginning of the chip. The data section is important as it contains 
MAC (at 0x1FC00) and PIN (at 0x1FE00) as well as Model information.
64k ART partition: which contains wireless voodoo configuration. Without it your wifi won't come up.

After dumping the memory, use dd to extract the second and last block.

```console
#!/bin/sh
# new image size
# block size -> 64k
bs=65536
ls -l flash_dump
# -rw-rw-r-- 1 makefu makefu 4194304 Mar 21 10:28 flash_dump
flash_size=$(ls -l flash_dump | cut -d\  -f 5)
#             4194304 / 65536
num_blocks=$(($flash_size/$bs))
# 64 blocks, 64kilobyte each
dd if=flash_dump of=data.bin bs=$bs count=1 skip=1
dd if=flash_dump of=art.bin bs=$bs count=1 skip=$(($num_blocks-1))
```

After that you can cat together your new image:

```console
new_image_size=16777216
truncate --size $((new_image_size-3*$bs)) whitespace.bin
 
# build pepe2k bootloader at first: see https://github.com/pepe2k/u-boot_mod
cat uboot_for_tp-link_tl-wr703n.bin \
    data.bin \
    whitespace.bin \
    art.bin > wr703_bootloader_data_whitespace_art.bin
```

Flash this image with your SPI-programmer on your new chip and solder it in. You can now hold the button for 3 seconds (will blink each second) and release to make the bootloader start a httpd at 192.168.1.1.




## Referência
### https://openwrt.org/toh/tp-link/tl-wr720n
### https://openwrt.org/toh/arduino.cc/yun
### https://docs.arduino.cc/tutorials/yun-rev2/yun-sys-upgrade/
### https://docs.arduino.cc/tutorials/yun-rev2/yun-u-boot-reflash/
### https://openwrt.org/toh/tp-link/tl-wr1043nd
### https://openwrt.org/toh/tp-link/tl-wr941nd
### https://github.com/Intika-Linux-Router/U-Boot-R-MoD/tree/master
### https://github.com/pepe2k/u-boot_mod/tree/master/original_u-boot_images
### https://openwrt.org/toh/mercury/mw150r
### https://openwrt.org/toh/tp-link/tl-wr740n
### https://cavefxa.com/posts/router-hacking0/
### https://cavefxa.com/posts/router-hacking1/
### https://cavefxa.com/posts/router-hacking2/
### https://github.com/jyy5206/TP-link-WR720N-16M-Flush-Firmware
### http://ftp.ufanet.ru/pub/firmware/Tp-Link/TL-WR720N/V2/
### https://www.dragino.com/products/mother-board/item/115-ms14n-s.html

sobre TFTP

### https://openwrt.org/docs/guide-user/installation/generic.flashing.tftp.easy-ubuntu

falado do uboot e ART

### https://openwrt.org/toh/tp-link/tl-wr710n
### https://openwrt.org/toh/tp-link/tl-wr703n#mb_flash_mod
### https://stackoverflow.com/questions/47025038/the-beginning-and-end-address-of-the-flash-memory
### https://github.com/bkil/calibrated-art-collection/tree/master
### https://openwrt.org/toh/gl.inet/64xx
### https://github.com/Edragon/openwrt/tree/master/JS9331

