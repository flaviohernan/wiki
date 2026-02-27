# Guia rápido de uso do software flashrom

## Intalação do flashrom
### Linux

```console
sudo apt-get install flashrom
```

## Uso do flashrom

### Linux

```console
sudo flashrom -p ch341a_spi
```

```console
sudo flashrom -p ch341a_spi -r filename.bin
```

```console
sudo flashrom -p ch341a_spi -w filename.bin
``` 
#### Gravar região de memória

criar um arquivo de texto, contendo o mapa da memória
```console
sudo flashrom -p <programmer> -l layout.txt -i region_name:filename.bin --fast-verify -w
```

#### Gravar uma imagem menor em uma memória maior

primeiramente criar um arquivo cheio de 0xFF com o tamanho da memória que se deseja preencher
pode ser feito através dos comandos **dd** ou **truncate**

Usando dd

```console
# First, get the size of the flash chip (e.g., 256KB = 262144 bytes)
# Pad the image file to the full size of the chip
dd if=/dev/zero bs=1 count=0 seek=262144 iflag=fullblock of=full_image.bin
dd if=smaller_image.bin of=full_image.bin conv=notrunc bs=1
```
Usando truncate

```console
# Create a new, empty file of the target size (e.g., 16 MB)
truncate -s 16M full_image.bin

# Copy your smaller image to the beginning of the new file
dd if=smaller_image.bin of=full_image.bin conv=notrunc bs=1
```

```console
flashrom -p <programmer> -w full_image.bin
```

 As far as I know there is no way to tell dd to pad using 0xFF. But there is a workaround.
First create a file with the required length filled with 0xFF:

$ dd if=/dev/zero ibs=1k count=100 | tr "\000" "\377" >paddedFile.bin
100+0 records in
200+0 records out
102400 bytes (102 kB) copied, 0,0114595 s, 8,9 MB/s

tr is used to replace zeroes with 0xFF. tr expects arguments in octal. 0xFF in octal is \377.
Result:

$ hexdump -C paddedFile.bin 
00000000  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff ff ff  |................|
*
00019000

Then insert the input file at the beginning of the "padded" file:

$ dd if=inputFile.bin of=paddedFile.bin conv=notrunc
0+1 records in
0+1 records out
8 bytes (8 B) copied, 7,4311e-05 s, 108 kB/s

Note the conv=notrunc which tells dd to not truncate the output file.
Example input file:

$ hexdump -C inputFile.bin 
00000000  66 6f 6f 0a 62 61 72 0a                           |foo.bar.|
00000008

Result:

$ hexdump -C paddedFile.bin 
00000000  66 6f 6f 0a 62 61 72 0a  ff ff ff ff ff ff ff ff  |foo.bar.........|
00000010  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff ff ff  |................|
*
00019000

## Referencias
### https://flashrom.org/supported_hw/supported_prog/ch341ab.html
### https://simple-is-beauty.blogspot.com/2019/11/generating-0xff.html
