## Alterar o arquivo Device Tree (DTS)
   Você deve expandir o tamanho da partição firmware e mover a partição art (essencial para o Wi-Fi) para o final dos 16MB

   O OpenWrt define o layout da memória flash (onde começa e termina o firmware) via arquivos Device Tree (DTS).

   Você precisará editar o arquivo de definição do hardware antes de compilar. Geralmente ele está em:target/linux/ath79/dts/ar9331_tplink_tl-wr710n-v1.dts (o caminho exato pode variar conforme a versão do OpenWrt).Lá, você deve procurar pela seção de partições e garantir que a partição firmware tenha o novo tamanho (ex: <0x000000 0xfe0000> para quase 16MB).

O kernel Linux usa o DTS para saber onde a memória Flash termina.

No OpenWrt moderno (como o 24.10), para o TP-Link WR710N v1, o arquivo geralmente está em:
```console
target/linux/ath79/dts/ar9331_tplink_tl-wr710n-v1.dts
```
Para localizar o arquivo **DTS**
```console
find target/linux/ath79/dts/ -name "*wr710n-v1*"
```
Abrir o arquivo .dts e procurar a seção **partitions@0**
```console
partition@0 {
    label = "u-boot";
    reg = <0x000000 0x020000>;
    read-only;
};

partition@20000 {
    label = "firmware";
    reg = <0x020000 0x7d0000>; // Aqui está o limite de 8MB (0x7d0000 + 0x20000 = 0x7f0000)
};

partition@7f0000 {
    label = "art";
    reg = <0x7f0000 0x010000>;
    read-only;
};

```

```console
```

```console
```

```console
```

```console
```



## Alterar o Makefile do Target
## Sincronizar o U-Boot
## Como compilar corretamente (Comando)
  
   ```console
   ./scripts/feeds update -a && ./scripts/feeds install -a
   make defconfig
   make -j$(nproc) V=s
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


## Referencia
### https://hackinggate.com/blog/build-openwrt-22-03-for-tl-wr703n-with-16m-flash
