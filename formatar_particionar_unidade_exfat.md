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
Para particionar pode usar **fdisk** ou **gdisk**

```console
sudo gdisk /dev/sdX
```

```console
Command (? for help): n
```
Nesse passo pode pressionar **ENTER**

```console
Partition number (1-128, default 1): 1
```

Nesse passo pode pressionar **ENTER**

```console
First sector (34-6291455966, default = 2048) or {+-}size{KMGTP}: 
Last sector (2048-6291455966, default = 6291455966) or {+-}size{KMGTP}:
```

Nesse passo pode pressionar **ENTER**

```console
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300):
Changed type of partition to 'Linux filesystem'
```
Para salvar as modficações
```console
Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdb.
The operation has completed successfully.
```


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
sudo mkfs.vfat -F 32 /dev/sdx1
```

```console
sudo mkfs.ext4 /dev/sdx1
```


# Referências
### https://linuxconfig.org/how-to-format-usb-with-exfat-on-linux
