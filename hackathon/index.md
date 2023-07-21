# Hackathon


**Escola de Verão** é um evento que reúne programadores e designers, cujo objetivo é desenvolver um software ou solução tecnológica que atenda a um fim específico.

<!--more-->

## Lista de Softwares (Linux Ubuntu)

### Git - Instalação
/
Use as ferramentas de gerenciamento de pacotes apt.
```shell
$ sudo apt update
$ sudo apt install git
$ git --version
```

### Gradle - Instalação

O Gradle requer apenas a instalação de uma versão Java JDK 8 ou superior.
```shell
$ sudo apt update
$ sudo apt install openjdk-17-jdk openjdk-17-jre
$ java --version
$ sudo mkdir /opt/gradle
$ cd /opt/gradle
$ sudo wget https://services.gradle.org/distributions/gradle-8.2.1-all.zip
$ sudo unzip -d /opt/gradle gradle-8.2.1-bin.zip
$ ls /opt/gradle/gradle-8.2.1
$ export PATH=$PATH:/opt/gradle/gradle-8.2.1/bin
$ gradle -v
```

### cURL - Instalação

Use as ferramentas de gerenciamento de pacotes apt.
```shell
$ sudo apt update
$ sudo apt install curl
$ curl --version
```

### Node.js 18.x - Instalação

Use as ferramentas de gerenciamento de pacotes apt.
```shell
$ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
$ sudo apt install -y nodejs
$ node -v
```

### Node.RED - Instalação

De acordo com o site (https://nodered.org/docs/getting-started/local).

Use as ferramentas de gerenciamento de pacotes apt e download.
```shell
$ sudo apt update
$ sudo apt install build-essential git curl
$ bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
$ sudo systemctl enable nodered.service
$ node-red
```

Para instalar o Node-RED, você pode usar o comando `npm` que vem com o `node.js`:
```shell
$ sudo npm install -g --unsafe-perm node-red
$ node-red
```

Pelo navegar, você deve usar o nome do host ou endereço IP: 
```browser
http:// <hostname>:1880
```

### GNU Nano

Use as ferramentas de gerenciamento de pacotes apt.
```shell
$ sudo apt update
$ sudo apt install nano
$ nano --version
```

### rasqal-utils

Use as ferramentas de gerenciamento de pacotes apt.
```shell
$ sudo apt update
$ sudo apt rasqal-utils
$ rasqal-utils --version
```

### raptor2-utils

Use as ferramentas de gerenciamento de pacotes apt.
```shell
$ sudo apt update
$ sudo apt raptor2-utils
$ raptor2-utils --version
```

### VS Code com as extensões

Faça o download do arquivo de `.deb`.
```shell
$ cd ~/Download
$ wget https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64
$ sudo apt install ./code_*.deb
```

  * Extension Pack for Java (https://open-vsx.org/vscode/item?itemName=vscjava.vscode-java-pack)
  * JaCaMo4Code (https://open-vsx.org/vscode/item?itemName=tabajara-krausburg.jacamo4code)
  * RedHat XML (https://open-vsx.org/vscode/item?itemName=redhat.vscode-xml)
  * Node-RED (https://open-vsx.org/vscode/item?itemName=formulahendry.vscode-node-red)
  * Stardog RDF Grammars (https://open-vsx.org/vscode/item?itemName=vemonet.stardog-rdf-grammars)

## Ilustrações

**PIXABAY**  
Disponível em: <https://pixabay.com/illustrations/iot-internet-of-things-network-3337536/>  
Acesso em: 17 jul. 2023.

## Referências

**H4CK4THON - Brasil**  
Disponível em: <https://hackathonbrasil.com.br>  
Acesso em: 17 jul. 2023.

**GIT --everythings-is-local**  
Disponível em: <https://git-scm.com>  
Acesso em: 17 jul. 2023.

**OpenJDK - Oficial**  
Disponível em: <https://openjdk.org>  
Acesso em: 17 jul. 2023.

**GRADLE - Build Tool**  
Disponível em: <https://gradle.org/install/>  
Acesso em: 17 jul. 2023.

**CURL - command line tool and library for transferring data with URLs**  
Disponível em: <https://curl.se>  
Acesso em: 17 jul. 2023.

**NODE.JS - Oficial**  
Disponível em: <https://nodejs.org/>  
Acesso em: 17 jul. 2023.

**NODE.RED - Oficial**  
Disponível em: <https://nodered.org>  
Acesso em: 17 jul. 2023.

**GNU NANO - Text Editor Homepage**  
Disponível em: <https://www.nano-editor.org>  
Acesso em: 17 jul. 2023.

**VS CODE - Oficial**  
Disponível em: <https://code.visualstudio.com>  
Acesso em: 17 jul. 2023.
