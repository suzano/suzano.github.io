# Fatsort


O Fatsort é uma aplicação para organizar por ordem alfabética os mp3 em um pendrive ou aparelho de MP3 player.

<!--more-->

## Conceitos

Após copiar uma série músicas para um pendrive ou aparelho de MP3 player portátil, mesmo as músicas sendo renomeadas ou colocadas em ordem alfabética, elas acabam não sendo tocadas nesse mesma ordem.

Para aqueles que gostam de ouvir as faixas aleatoriamente isso não é um incômodo, mas para mim, isso é muito chato!

## Parte 1: Fatsort

O aplicativo pode ser baixado pelo link <http://fatsort.berlios.de>.

## Parte 2: Instalação

Arch Linux
```shell
$ paru -Sy fatsort
```

Debian/Ubuntu
```shell
$ sudo apt install fatsort
```

## Parte 3: Uso do aplicativo

1. Monte seu pendrive ou aparelho de MP3.
2. Copie as músicas (ou as pastas que contém as músicas) para o dispositivo.
3. Desmonte a conexão com o dispositivo.
4. Como super usuário, digite no terminal:
```shell
$ sudo fatsort /dev/sda
```
5. Você já pode desconectar o dispositivo da sua máquina.

{{< admonition note "Info:" >}}
O caminho `/dev/sdb1` é a localização do meu aparelho. Certifique-se qual é a localização do seu antes desta operação.
{{< /admonition >}}

## Ilustrações

**PIXABAY**  
Disponível em: <https://pixabay.com/pt/photos/multid%C3%A3o-show-festival-de-m%C3%BAsica-1056764/>  
Acesso em: 22 mar. 2023.

## Referências

**VIVA O LINUX - Como deixar seus arquivos mp3 em ordem no mp3 player**  
Disponível em: <https://www.vivaolinux.com.br/dica/Como-deixar-seus-arquivos-mp3-em-ordem-no-mp3-player>  
Acesso em: 22 mar. 2023.

https://pixabay.com/pt/photos/fones-de-ouvido-m%C3%BAsica-ouvindo-1230987/

