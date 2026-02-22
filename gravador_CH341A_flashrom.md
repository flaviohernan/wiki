# Guia rápido de uso do software flashrom

## Intalação do flashrom
### Linux

```console
sudo apt-get install flashrom
```

## Uso do flashrom

### Linux

```console
flashrom -p ch341a_spi
```

```console
flashrom -p ch341a_spi -r filename.bin
```

```console
flashrom -p ch341a_spi -w filename.bin
``` 


## Referencias
### https://flashrom.org/supported_hw/supported_prog/ch341ab.html
