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

```console
# First, get the size of the flash chip (e.g., 256KB = 262144 bytes)
# Pad the image file to the full size of the chip
dd if=/dev/zero bs=1 count=0 seek=262144 iflag=fullblock of=full_image.bin
dd if=smaller_image.bin of=full_image.bin conv=notrunc bs=1
```

```console
flashrom -p <programmer> -w full_image.bin
```

## Referencias
### https://flashrom.org/supported_hw/supported_prog/ch341ab.html
