# Raspberry Pi - Softwares


Este artigo oferece sugestões de softwares para o Raspberry Pi.

<!--more-->

{{< admonition >}}
Este artigo é uma anotação com recortes e traduções (vergonhosas) da página do [Raspberry Pi](https://www.raspberrypi.com).
{{< /admonition >}}

## Conceito

O `Raspberry Pi` precisa de um sistema operacional para funcionar. Usaremos o `Raspberry Pi Imager` é a maneira rápida e fácil de instalar o `Raspberry Pi OS` e outros sistemas operacionais em um cartão microSD que será inserido no `Raspberry Pi`.

## Parte 1: Conectar-se na internet

A conexão do Raspberry Pi pode ser feito por meio do cabo Ethernet ou usando um dongle Wi-Fi. Nesse uma caso é necessário uma série de instruções para configurar o Wi-Fi.

Scan de redes wifi locais, onde so valores "ESSID" são os nomes das redes encontradas:
```shell
$ ip addr
$ sudo iwlist wlan0 scan | grep ESSID
```

Editar o `wpa_supplicant` para adicionar uma entrada para o Wi-Fi:
```shell
$ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

Adicionar as linhas para registrar a entrada de novas Wi-Fis conhecidas pelo Raspberry Pi:
```
network={
ssid="WIFI_SSID"
scan_ssid=1
psk="WIFI_PASSWORD"
key_mgmt=WPA-PSK
}
```

O roteador fornece Wi-Fi/LAN sem fio. O `IP` é um protocolo de comunicação que constitui a base da inter-rede de computadores que estabelece a Internet. Para encontrar o endereço IP atribuida para o Raspberry, use o comando:
```shell
$ ip addr
```

A interface `lo` é o `loopback`, o computador a utiliza para se comunicar consigo mesmo. A interface `eth0` é a interface `Ethernet` e interface `wlan0` corresponde a interface `Wi-Fi`. O `endereço IP` da LAN tem o título `inet` e se parece com `192.168.0.10`.

Para testar a conexão, é possível executar o `ping` em alguns sites para procurar uma resposta:
```shell
$ ping www.google.com
$ ping www.stackoverflow.com
$ ping www.facebook.com
```

## Parte 2: Softwares para Raspberry Pi

Para atualizar ou instalar novos softwares no `Raspberry Pi OS`, podemos usar a ferramenta `APT (Advanced Packaging Tool)` em uma janela do Terminal. O `APT` mantém uma lista de fontes de software no seu `Raspberry Pi` em um arquivo localizado em `/etc/apt/sources.list`.

Para atualizar a lista de pacotes abra uma janela do Terminal e digite:
```shell
$ sudo apt update
```

Atualizar todos os pacotes instalados para as versões mais recentes com o seguinte comando:
```shell
$ sudo apt full-upgrade
```

Instalar de outros pacotes com APT:
```shell
$ sudo apt install <nome_do_pacote>
```

Desinstalar um pacote com APT:
```shell
$ sudo apt remove <nome_do_pacote>
```

Remover completamente o pacote e seus arquivos de configuração associados:
```shell
$ sudo apt apt purge <nome_do_pacote>
```

Atualizar o kernel do Raspberry Pi OS e o firmware VideoCore para as versões:
```shell
$ sudo rpi-update
$ sudo reboot
```

## Parte 3: WebCam USB 

Verificar se a webcam foi identificada corretamente, execute esse comando:
```shell
$ lsusb
```
Será exibida uma lista como todos os periféricos usb.

Instalar os pacotes para uso de webcam USB:
```shell
# Permite usar uma webcam USB padrão para tirar fotos e gravar vídeos em seu Raspberry Pi.
$ sudo apt install fswebcam
# Adicionar nome de usuário ao videogrupo, caso contrário, você verá erros de “permissão negada”.
$ sudo usermod -a -G video guaracy
# Para verificar se o usuário foi adicionado ao grupo corretamente.
$ groups
```

Tirar uma foto usando a webcam e salvando com um nome de arquivo especificado:
```shell
$ fswebcam image.jpg
```

{{< admonition >}}
A foto utiliza a resolução padrão e a apresenta um banner mostrando o carimbo de data/hora.
{{< /admonition >}}

Especificar a resolução deseja para a foto, use o parâmetro `-r`:
```shell
fswebcam -r 1280x720 image2.jpg
```

Remover o banner da foto, utilize o parâmetro `--no-banner`:
```shell
$ fswebcam -r 1280x720 --no-banner image3.jpg
```

Para automatizar a captura de imagens é necessário criar um `script Bash` que tire uma foto com a webcam e salve as imagens no diretório `/home/guaracy/webcam`:
```shell
$ cd ~
$ mkdir webcam
$ cd webcam
$ touch webcam.sh
$ nano webcam.sh
```

Código do script Bash para tirar uma foto e nomea-la com a correspondente data e hora:
```shell
#!/bin/bash
DATE=$(date +"%Y-%m-%d_%H%M%S")
fswebcam -r 1280x720 --no-banner /home/guaracy/webcam/$DATE.jpg
```

Para que o script funcione, precisamos torná-lo um arquivo executável:
```shell
$ chmod +x webcam.sh
```

Para executar o script:
```shell
$ ./webcam.sh
```

Também é possível usar o `cron` para agendar a captura de uma foto em um determinado intervalo:
```shell
$ crontab -e
```

Adicionando a seguinte linha, será agendada a captura de uma foto a cada minuto (referindo-se ao script Bash acima):
```
* * * * * /home/pi/webcam.sh 2>&1
```

## Parte 4: WebServer

O `lighttpd` que é um servidor web seguro, rápido e muito flexível, otimizado para ambientes de alto desempenho (pode ser usado em vez do Apache por exemplo). Possue baixo consumo de memória e CPU em comparação com outros servidores web.

Instalação do Lighttpd e seus componentes:
```shell
$ sudo apt install lighttpd -y
$ sudo lighttpd-enable-mod cgi
$ sudo lighttpd-enable-mod fastcgi
```
Por padrão, o `Lighttpd` procurará uma página `index.html` no diretório `/var/www/html`. É possível alterar esse diretório editando o arquivo de configuração do `Lighttpd`:
```shell
$ sudo nano /etc/lighttpd/lighttpd.conf
```

alterar a linha:
```
server.document-root =“/var/www/html”
```

para:
```
server.document-root =“/var/www”
```

Qualquer alteração no arquivo de configuração só terá efeito após, o servidor web ser parado e reiniciado:
```shell
$ sudo /etc/init.d/lighttpd stop
$ sudo /etc/init.d/lighttpd start
```

Criando uma página `HTML` simples para efeito de testes:
```shell
$ cd /var/www/
$ sudo nano index.html
```

Exemplo de conteúdo HTML:
```html
<!DOCTYPE HTML>
<html lang="pt-BR">
<head>
	<meta charset="UTF-8">
	<title>Uma Página HTML Básica</title>
</head>
<body>

<p>
	Esta é uma página básica, contendo os principais elementos:
</p>
<ul>
	<li>Doctype do HTML5</li>
	<li>Elemento <code>html</code> com o atributo <code>lang</code>, o elemento "raiz" que contém todos os outros</li>
	<li>Elemento <code>head</code> com o conteúdo de cabeçalho da página não visível</li>
	<li>Elemento <code>meta</code> com o atributo <code>charset</code>, especificando a codificação da página como sendo UTF-8 (para evitar problemas com caracteres acentuados e outras línguas)</li>
	<li>Elemento <code>title</code> com o texto que aparece justamente no título da janela do navegador (ou da respectiva aba no navegador)</li>
	<li>Elemento <code>body</code>, que contém todo o conteúdo vísivel do site e que será também estruturado com HTML</li>
</ul>
<p>
	Acima e neste parágrafo, você vê a utilização das tags <code>p</code> (parágrafo), <code>ul</code> (<em>unordered list</em>, ou lista não ordenada)
	e <code>li</code> (<em>list item</em>, ou item de lista), que iremos ver mais a fundo na lição sobre Texto e Listas.
	Também utilizada nesta página é a tag <code>code</code>, que serve para identificar código utilizado em computadores (neste caso as próprias tags HTML).
</p>
<!-- Este é um comentário HTML. O texto aqui não irá aparecer na tela do navegador. Comentários são úteis para anotar partes do documento ou então esconder partes do código intencionalmente, para fins de diagnóstico de problemas (chamado "commenting out"), entre outros. -->

</body>
</html>
```

Depois de editar a página e salvá-la, é necessário alterar as permissões:
```shell
$ sudo chmod 755 index.html
```
 
No navegador web, digite o endereço IP correspondente ao Raspberry Pi:
```
http://192.168.0.10
```

## Parte 5: Motion

O `Motion` é um software de vigilância escrito para Linux e derivados. É estritamente uma ferramenta de linha de comando que também pode ser executada como um daemon (serviço que roda no background do sistema operacional), tornando-a perfeita para um sistema embarcado.

Normalmente, os softwares no Linux e derivados são instalados usando `APT (Advanced Packaging Tool)`, porém, o repositório correspondente ao `Motion` fornecerá uma versão do desatualizada do software. Em vez disso, podemos fazer o download do código-fonte do programa disponível no site do GitHub (rede social de desenvolvedores), compilar o código e adicionar manualmente aos registros do sistema operacional.

```shell
$ cd ~
$ mkdir Downloads
$ cd Downloads
$ sudo apt update
$ sudo apt install autoconf automake autopoint build-essential pkgconf libtool libzip-dev libjpeg-dev git libavformat-dev libavcodec-dev libavutil-dev libswscale-dev libavdevice-dev libwebp-dev gettext libmicrohttpd-dev
$ git clone https://github.com/Motion-Project/motion.git
$ cd motion
$ autoreconf -fiv
$ ./configure
$ make
$ sudo make install
$ sudo mv /usr/local/etc/motion/motion-dist.conf /usr/local/etc/motion/motion.conf
$ sudo reboot
```

Editar o arquivo de configuração do `Motion`, alterar a qualidade da câmera, habilitar web streaming, habilitar autenticação web, etc.

```shell
$ sudo nano /usr/local/etc/motion/motion.conf
$ sudo motion
```

Algumas das opções úteis:
- daemon on
- height 320
- width 240
- framerate 100
- text_left CAMERA
- movie_quality
- webcontrol_localhost off
- stream_locahost off
- webcam_quality (compressão jpeg) 
- stream_maxrate ()
- stream_authentication
- stream_auth_method (habilitar autenticação)
- webcam_localhost
- control_localhost

A saída do Motion pode ser vista abrindo o navegador web e digitando:
```
http://192.168.0.10:8081
```

Para incorporar o vídeo no site, use um iframe na sua página `motion.html`. Um iframe é apenas uma janela para outra página, neste caso o streaming de vídeo do Motion.
```shell
$ cd /var/www/
$ sudo touch motion.html
$ sudo chmod 755 index.html
$ sudo touch motion.html
```

Exemplo de conteúdo HTML:
```html
<!DOCTYPE HTML>
<html lang="pt-BR">
<head>
	<meta charset="UTF-8">
	<title>Motion</title>
</head>
<body>

<iframe src="http://192.168.0.10:8081" height="750" width="1300"></iframe>

</body>
</html>
```

## Parte 6: htop

O `htop` é uma ferramenta de monitoramento de processos do Linux interativa e em tempo real muito avançada, muito semelhante ao comando `top` do Linux, mas possui alguns recursos avançados, interface amigável e teclas de atalho.

```shell
$ sudo apt install htop
$ sudo htop
```

## Parte 7: nload

O `nload` é uma ferramenta de linha de comando simples e fácil de usar para monitorar o tráfego de rede e o uso da largura de banda em tempo real.

```shell
$ sudo apt install nload
$ nload
```

## Ilustrações

**PIXABAY**  
Disponível em: <https://pixabay.com/pt/photos/raspberry-pi-computador-eletr%C3%B4nicos-572481/>  
Acesso em: 25 ago. 2023.

## Referências

**RASPBERRY PI - Getting started**  
Disponível em: <https://www.raspberrypi.com/documentation/computers/getting-started.html>  
Acesso em: 25 ago. 2023.

**MJROBOT.ORG - Controlando um Raspberry Pi robô pela Internet**  
Disponível em: <https://mjrobot.org/2016/06/01/controlando-um-raspberry-pi-robo-pela-internet/>  
Acesso em: 25 ago. 2023.

**JRL - Using Motion with a Raspberry Pi**  
Disponível em: <https://jarlowrey.com/blog/rpi-with-motion.html>  
Acesso em: 25 ago. 2023.
