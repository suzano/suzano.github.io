# Real VNC


Ventoy é uma ferramenta de código aberto para criar uma unidade USB inicializável para arquivos ISO/WIM/IMG/VHD(x)/EFI.

<!--more-->

## Conceitos


realvnc-vnc-server

Software de servidor de desktop remoto VNC da RealVNC

Você pode ir para:

https://www.realvnc.com/en/connect/home

e crie uma conta no site, se você não tiver uma, e solicite a "Assinatura doméstica".

Você pode conectar até 5 PCs remotos gratuitamente.



## Parte 1: VNC

O aplicativo pode ser baixado pelo link <https://www.ventoy.net/en/download.html>.

## Parte 2: Instalação

Arch Linux
```shell
$ paru -Sy realvnc-vnc-server
```

Conflitos:	tigervnc, tightvnc, pregadovnc
Esses pacotes "gtk2" e "gnome-themes-extra" também são necessários para mostrar e funcionar corretamente o ícone da bandeja em alguns ambientes da área de trabalho

## Parte 3: Como funciona...

Após a conclusão da instalação, abre o programa.

![Ventoy](./ventoy.png "Ventoy")

Escolha a unidade USB que deseja tornar inicializável e clique em instalar.

A unidade USB será dividida em 2 partições. Uma partição será formatada com o sistema de arquivos FAT16 e será usada SOMENTE para o `Ventoy` e a outra partição será formatada com o sistema de arquivos exFAT (você também pode reformatá-la manualmente com NTFS/FAT32/UDF/XFS/Ext2/3/4).

Agora o que você precisa fazer é copiar os arquivos `.ISO` para esta partição. Você pode colocar os arquivos iso/wim/img/vhd(x) em qualquer lugar. O Ventoy pesquisará todos os diretórios e subdiretórios recursivamente para encontrar todos os arquivos de imagem e listá-los no menu de inicialização em ordem alfabética.Além disso, você usar a configuração do plug-in para informar ao Ventoy apenas para procurar arquivos de imagem em um diretório fixo (e seus subdiretórios).

Você também pode usá-lo como uma unidade USB simples para armazenar arquivos e isso não afetará a função do Ventoy.

## Ilustrações

**MESTRE DA INFORMÁTICA**  
Disponível em: <https://mestresdainformatica.com.br/ventoy-criar-pendrive-multiboot-gratis/>  
Acesso em: 24 mar. 2023.

## Referências

https://www.realvnc.com/

https://aur.archlinux.org/packages/realvnc-vnc-server
https://aur.archlinux.org/packages/realvnc-vnc-viewer


