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

## Referencias
### https://flashrom.org/supported_hw/supported_prog/ch341ab.html
