Método para criar partição e formatar um disco com particionamento MBR.

# Comandos

```console
root # fdisk -l /dev/sdx

Disk /dev/sdx: 640.1 GB, 640135028736 bytes, 1250263728 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: gpt

#         Start          End    Size  Type            Name
 1         2048   1250263694  596.2G  Linux filesyste Linux filesystem
```

```console
root # fdisk /dev/sdx
```

```console
Command (m for help): o ↵
```
Create Partition 1 (boot): 
```console
Command (m for help): n ↵
Partition type (default p): ↵
Partition number (1-4, default 1): ↵
First sector: ↵
Last sector: +128M ↵
```
Create Partition 2 (swap): 
```console
Command (m for help): n ↵
Partition type (default p): ↵
Partition number (2-4, default 2): ↵
First sector: ↵
Last sector: +2G ↵
Command (m for help): t ↵ 
Partition number (1,2, default 2):  ↵
Hex code (type L to list all codes): 82 ↵
```
Create the root partition:
```console
Command (m for help): n ↵
Partition type (default p): ↵
Partition number (3,4, default 3): ↵
First sector: ↵
Last sector: ↵
```
Verify the partition table: 
```console
Command (m for help): p

Disk /dev/sdx: 298.1 GiB, 320072933376 bytes, 625142448 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x82abc9a6

Device    Boot     Start       End    Blocks  Id System
/dev/sdx1           2048    264191    131072  83 Linux
/dev/sdx2         264192   4458495   2097152  82 Linux swap / Solaris
/dev/sdx3        4458496 625142447 310341976  83 Linux
```
Write the partition table to disk:
```console
Command (m for help): w
```

```console

```

# Referencias
### https://www.funtoo.org/Install/MBR_Partitioning
### https://linuxconfig.org/how-to-format-usb-with-exfat-on-linux
