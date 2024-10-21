---
title:  "Flatpak no Debian"
date:   2024-10-20 08:00:00 +0530
img: "flatpak.png"
categories: [Debian, Ferramentas, Flatpak]
author: "Suzano Bitencourt"
profile:
  attrs:
    - key: 
      val: 
    - key: 
      val: 
---

Este artigo é uma tradução (vergonhosa) da página do [Flathub](https://flathub.org/setup/Debian).

<!--more-->

## Conceito

**Flatpak** é um sistema de distribuição de aplicativos que oferece uma forma padronizada e isolada de instalar e executar software em diferentes distribuições Linux. Ele foi projetado para resolver o problema de fragmentação no ecossistema Linux, onde diferentes distribuições têm gerenciadores de pacotes e sistemas de arquivos distintos, tornando difícil a compatibilidade universal de aplicativos.

## Parte 1: Instalação do Flatpak

1 - Para instalá-lo, execute o seguinte como root:
```bash
sudo apt install flatpak
```

## Parte 2: Instalação dos plugins para Flatpak

1 - Se você estiver executando o GNOME, também é uma boa ideia instalar o plugin Flatpak para o software GNOME.
```bash
sudo apt install gnome-software-plugin-flatpak
```

## Parte 3: Adição do repositório Flathub

1 - Flathub é o melhor lugar para obter aplicativos Flatpak. Para ativá-lo, execute o seguinte em um terminal:
```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Parte 4: Reiniciar

1 - Para concluir a configuração, reinicie o sistema.
```bash
sudo reboot
```

## Parte 5: Instalação de aplicativos

1 - Vamos instalar o `ytDownloader` (Anteriormente conhecido como Youtube Downloader Plus) permite baixar vídeos e áudios de diferentes qualidades de centenas de sites, incluindo os populares, mas não limitados a Youtube, Facebook, Instagram, Tiktok, etc Twitter, Twitch e assim por diante:
```bash
flatpak install flathub io.github.aandrew_me.ytdn
```

2 - Execute o aplicativo:
```bash
flatpak run io.github.aandrew_me.ytdn
```

## Ilustrações

**WIKIPEDIA**  
Disponível em: <https://upload.wikimedia.org/wikipedia/commons/thumb/8/8a/Flatpak_Logo.svg/400px-Flatpak_Logo.svg.png>  
Acesso em: 20 out. 2024.

## Referências

**FLATHUB - Debian**  
Disponível em: <https://flathub.org/setup/Debian>  
Acesso em: 20 out. 2024.