---
title: youtube-dl
description: Programa de linha de comando para baixar vídeos do YouTube.com
date: 2021-11-09T13:00:00-00:00
featured_image: "/images/Pope-Edouard-de-Beaumont-1844.jpg"
draft: false
tags:
  - youtube.com
  - youtube-dl
  - mp4
  - mp3
  - ffmpeg
---
## Sobre o programa
O `youtube-dl` é um programa de linha de comando para baixar vídeos do YouTube.com e de alguns outros sites, como Metacafe, Dailymotion, Instagram, Vine, Vimeo, Tumblr, Trilulilu, Syfy, Slashdot, RottenTomatoes, NBC, NBA, NBCNews, MySpace, MTV, Metacritic, KickStarter, GameSpot, Flickr, Dropbox, Discovery, CollegeHumor, ComedyCentral, CNN, CBS, Bloomberg e 9gag.
Além do acima, o 4tube, AddAnime, AppleTrailers, ARD, Bandcamp, BlipTV, Brightcove, Chilloutzone, Cinemassacre, Clipsyndicate, DepositFiles e FranceInter também estão entre os sites suportados.
Também poderá baixar vídeos de sites apenas para adultos, como YouPorn, XTube, XNXX, Pornjam, Pornotube, XHamster, PornHub, PornHd, RedTube e Mofosex.
No entanto, se você deseja converter os vídeos .webm para .mp3, você precisará do FFMpeg instalado em seu sistema.
## Instalação do youtube-dl
Descubra qual versão está disponível no repositório:
```
$ apt-cache policy youtube-dl
```
No Linux, você pode instalá-lo diretamente do terminal usando este comando:
```
$ sudo apt install youtube-dl
```
## Uso da ferramenta
Agora vamos aprender como usá-lo, por meio de exemplos:
![tabela-youtube-dl.png](/img/posts/tabela-youtube-dl.png)
O comando básico às vezes é a melhor opção:
```
$ youtube-dl "URL"
```
Para FULL HD 1080p:
```
$ youtube-dl -o file.mp4 -f 37 "URL"
```
Para 720p:
```
$ youtube-dl -o file.mp4 -f 22 "URL"
```
Outras opções:
```
-b - Melhor qualidade.
-m - Versão móvel.
-d - Alta Definição.
-g - Não faça download, apenas mostre o url.
-c - Retomar o download de um vídeo que foi interrompido anteriormente.
-w - Não sobrescrever o arquivo existente.
```
## youtube-dl para mp3
Para baixar e converter mp4, webm ou qualquer outro formato que o vídeo do YouTube possa ter, este comando fará o download e o converterá em um arquivo .mp3:
```
$ youtube-dl --extract-audio --audio-format mp3 "URL"
```
Para baixar uma lista de reprodução:
```
$ youtube-dl -itcv --yes-playlist https://www.youtube.com/playlist?list=
```
Agora, se você quiser que essa lista se transforme em .mp3, faça assim:
```
$ youtube-dl -itcv --yes-playlist --extract-audio --audio-format mp3 https://www.youtube.com/playlist?list=PLUDOMtEpSH_5kkA0iGd3AyEG7_7W1OVrV
```
## Atualização
Como atualizar o software YouTube-DL:
```
$ youtube-dl --version
```
```
$ sudo youtube-dl -U
```
## Em caso de ERRO
Se por algum motivo o youtube-dl não funcionar, faça o seguinte:
```
$ sudo apt install python3-pip
```
Então, para corrigir o erro:
```
$ sudo pip install youtube-dl --upgrade
```
## Fonte
https://www.linuxexperten.com/content/youtube-dl-youtube-mp3-downloader
* * *