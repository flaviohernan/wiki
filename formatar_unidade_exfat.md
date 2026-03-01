Comandos para formatar a unidade em exfat, mas pode ser usada outros métodos de formatação, ext4, fat32, ntfs ...

# Instruções

## Instalação

```console
sudo apt update
sudo apt install exfat-fuse
```

## Identificar a unidade
```console
sudo fdisk -l
```
ou 

```console
lsblk
```

## Particionar a unidade

## Formatar a unidade
Desmontar a unidade, se necessário

```console
sudo umount /dev/sdx1
```
EXFAT

```console
sudo mkfs -t exfat /dev/sdx1
```
FAT32
```console
sudo mkfs.vfat -F 32 /dev/sdb1
```

```console

```

```console

```

```console

```

```console

```

```console

```

# Referências
### https://linuxconfig.org/how-to-format-usb-with-exfat-on-linux
