# Tutorial para gravar firmware por TFTP
Será usado o rotreador TL-WR720N CPU Atheros AR9331-AL3A

Foi adicionado 32MB de RAM (K4D551638-TC500) e 4MB de flash. A placa original usar 16MB e 2MB.

## Comandos
 ```console
sudo netdiscover -S -f -i enp9s0

  sudo apt install tftp-hpa
  sudo systemctl restart tftpd-hpa
  sudo ufw allow tftp
  sudo ufw allow 69/udp

sudo apt install dhex

```

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
