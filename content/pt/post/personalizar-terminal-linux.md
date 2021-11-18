---
title: Personalizar terminal Linux
description: Personalizar a tela inicial do terminal Linux
date: 2021-11-09T16:00:00-00:00
featured_image: "/images/Pope-Edouard-de-Beaumont-1844.jpg"
draft: false
tags:
  - linux
  - terminal
  - alias
  - personalizacao
  - comandos
---
## Etapa 1: Encontrar o arquivo de configuração do Shell
O emulador de terminal instalado em sua máquina Linux funciona como um frontend para o shell subjacente. Na maioria das distros Linux, o Bash é o shell padrão que vem pré-instalado com o sistema.
Cada shell possui um arquivo de configuração armazenado no diretório inicial do usuário. Para o Bash, o arquivo é denominado `.bashrc` . E se você estiver usando Zsh, será `.zshrc`.
No diretório inicial, localize o arquivo de configuração correspondente ao shell que você está usando no momento. Para o propósito deste guia, demonstraremos como personalizar a tela inicial no Bash. No entanto, observe que as etapas também são semelhantes para outros shells.
Para personalizar a tela inicial do seu terminal, primeiro abra o arquivo de configuração do shell usando seu editor de texto favorito . Neste caso, Vim:
```
$ vim ~/.bashrc
```
## Etapa 2: adicionar o conteúdo da tela inicial
Antes de começar a adicionar scripts sofisticados ao arquivo, tente imprimir uma string simples primeiro para verificar se o arquivo de configuração foi lido corretamente pelo shell. Para fazer isso, anexe a seguinte linha ao final do arquivo de configuração:
```
echo "Welcome to the Terminal!"
```
Agora, salve e saia do Vim e reinicie o terminal para ver as alterações.
```
$ $Shell
```
## Etapa 3: outros comandos (opcional)
```
# Exibir informações do sistema na tela inicial
neofetch
screenfetch
```
```
# Exibir uma mensagem aleatória
fortune
# ou
fortune | cowsay
```
```
# Mostre uma arte ASCII no lançamento
figlet -cl "Arch Linux"
```
```
# Adicionar informações de tempo e data
curl wttr.in/paris?0
```
* * *
## Fonte
https://www.makeuseof.com/customize-linux-terminal-splash-screen/