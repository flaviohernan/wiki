## Alterar o arquivo Device Tree (DTS)
   Você deve expandir o tamanho da partição firmware e mover a partição art (essencial para o Wi-Fi) para o final dos 16MB

   O OpenWrt define o layout da memória flash (onde começa e termina o firmware) via arquivos Device Tree (DTS).

   Você precisará editar o arquivo de definição do hardware antes de compilar. Geralmente ele está em:target/linux/ath79/dts/ar9331_tplink_tl-wr710n-v1.dts (o caminho exato pode variar conforme a versão do OpenWrt).Lá, você deve procurar pela seção de partições e garantir que a partição firmware tenha o novo tamanho (ex: <0x000000 0xfe0000> para quase 16MB).

No OpenWrt moderno (como o 24.10), para o TP-Link WR710N v1, o arquivo geralmente está em:
   ```console
   target/linux/ath79/dts/ar9331_tplink_tl-wr710n-v1.dts
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
