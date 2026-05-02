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
Abrir o arquivo .dts e procurar a seção **partitions@0**, abaixo é um exemplo
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
### Modificar para 16MB

Como deve ficar para 16MB:
* u-boot: Mantém o mesmo (0x000000 a 0x020000).
* firmware: Vai começar em 0x020000 e terá o tamanho de 0xfd0000 (isso cobre até quase o fim dos 16MB).
* art: Deve ser movida para o endereço 0xff0000 (os últimos 64KB do chip).

O arquivo deve ficar com as seguintes alterações:
```console
partition@0 {
    label = "u-boot";
    reg = <0x000000 0x020000>;
    read-only;
};

partition@20000 {
    label = "firmware";
    reg = <0x020000 0xfd0000>; // Expandido para 16MB (quase 15.8MB)
};

partition@ff0000 {
    label = "art";
    reg = <0xff0000 0x010000>; // Movido para o final real do chip de 16MB
    read-only;
};

```

```console
```

```console
```

```console
```



## Alterar o Makefile do Target

O OpenWrt limita o tamanho da imagem final para evitar erros. 
Para o WR710N, precisamos avisar ao compilador que agora ele tem 16MB.
Edite o arquivo de definições de imagem:

```console
vi target/linux/ath79/image/generic-tp-link.mk
```
* De: $(Device/tplink-8mlzma) Para: $(Device/tplink-16mlzma)
* E garanta que a linha IMAGE_SIZE := 15872k esteja logo abaixo.

```console
define Device/tplink_tl-wr710n-v1
  $(Device/tplink-16mlzma)
  SOC := ar9331
  DEVICE_MODEL := TL-WR710N
  DEVICE_VARIANT := v1
  DEVICE_PACKAGES := kmod-usb-chipidea2 kmod-usb-ledtrig-usbport
  TPLINK_HWID := 0x07100001
  IMAGE_SIZE := 15872k
  SUPPORTED_DEVICES += tl-wr710n
  DEFAULT := n
endef
TARGET_DEVICES += tplink_tl-wr710n-v1
```

Recomendação é de limmpar os arquivos temporários caso ocorra erro de tamanho do binario final.
```console
rm -rf bin/targets/ath79/generic/
```

```console
make target/linux/compile
```

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

## Resumo dos passos
1. Preparação do Ambiente
   * Executar ./scripts/feeds update -a && ./scripts/feeds install -a
   * Ter o backup da sua partição ART de 64KB salvo.
2. Modificação dos Arquivos de Imagem (Ajuste de Limite)
   * Editar o arquivo target/linux/ath79/image/tiny.mk (ou generic.mk).
   * Localizar Device/tplink_tl-wr710n-v1 e alterar:IMAGE_SIZE := 15872k
3. Modificação do Layout de Memória (DTS)
   * Editar o arquivo target/linux/ath79/dts/ar9331_tplink_tl-wr710n-v1.dts
   * Ajustar a partição firmware: reg = <0x020000 0xfd0000>;
   * Ajustar a partição art: reg = <0xff0000 0x010000>;
4. Configuração do Firmware (Menuconfig)
   * Rodar make menuconfig.
   * Selecionar Target System (Atheros AR7xxx/AR9xxx) e Target Profile (TP-Link TL-WR710N v1).
   * Ir em Target Images -> Root filesystem partition size (in MB) -> Definir como 14.
   * Selecionar o LuCI (Interface Web) se desejar: LuCI -> Collections -> luci.
   * Salvar e Sair.
5. Validação e Compilação
   * Executar make defconfig (para validar as dependências e o novo tamanho).
   * Executar make -j$(nproc) V=s.

## Resumo2
1. Modificação do Perfil de Hardware (.mk)
   * No arquivo target/linux/ath79/image/generic-tp-link.mk:
   * Alterar o pai do dispositivo para $(Device/tplink-16mlzma).
   * Garantir a linha IMAGE_SIZE := 15872k.
   * Isso permite gerar o arquivo de 16.252.928 bytes.
2. Modificação do Layout de Memória (.dts)
   * No arquivo target/linux/ath79/dts/ar9331_tplink_tl-wr710n-v1.dts:
   * Redefinir a partição firmware para reg = <0x020000 0xfd0000>;
   * Mover a partição art para o final do chip: reg = <0xff0000 0x010000>;
   * Isso garante que o kernel encontre o Wi-Fi e o espaço extra do overlay.
3. Compilação
   * make menuconfig -> Target Images -> Root partition size: 14 (ou deixar o padrão, já que o DTS agora manda).
   * make defconfig -> Para validar as mudanças.
   * make -j$(nproc) V=s -> Gerou o arquivo correto de ~16MB.
4. Instalação 
   * Entrar no U-Boot/Breed: Ligue o roteador segurando o botão reset.
   * Backup/ART: Certifique-se de que seus dados de ART (64KB) foram gravados no final do chip físico (endereço 0xFF0000).
   * Flash: Envie o arquivo openwrt-ath79-...-factory.bin de 16MB via interface web do U-Boot/Breed.
   * Verificação:
   *    df -h: Verifique se o overlay tem ~12MB livres.
   *    wifi up: Teste se o rádio liga (confirmação do ART)


## Referencia
### https://hackinggate.com/blog/build-openwrt-22-03-for-tl-wr703n-with-16m-flash
