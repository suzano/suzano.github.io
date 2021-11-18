---
title: Configurar VPN USP no Linux
description: Configurar VPN USP no Linux
date: 2021-11-09T17:00:00-00:00
featured_image: "/images/Pope-Edouard-de-Beaumont-1844.jpg"
draft: false
tags:
  - linux
  - vpn
  - usp
  - uspdigital
  - semfio
---
## Etapa 1:
Abra o terminal e digite os comandos de instação:
```
$ sudo apt-get install network-manager-openconnect
```
```
$ sudo apt-get install network-manager-openconnect-gnome
```
## Etapa 2:
Após a instalação abra as configurações de Rede.
## Etapa 3:
Clique no botão + e em seguida deixe selecionado VPN e clique em Criar...
## Etapa 4:
Selecione a opção VPN Compatível com Cisco Any Connect (openconnect) e clique em Criar..
## Etapa 5:
Preencha o campo Nome da conexão com VPN USPNet e o campo Gateway com **vpn.semfio.usp.br**. Não é necessário alterar os outros campos. Clique em Salvar.
## Etapa 6:
Mude a chave de conexão para ON. Na janela que abrir clique sobre o ícone de rede.
## Etapa 7:
Os dados para acesso são o seu Número USP e sua senha única  do portal **uspdigital.usp.br**. Depois de preencher os dados, clique em Login.
Depois disso, a conexão deve ser estabelecida.
## Fonte

* * *