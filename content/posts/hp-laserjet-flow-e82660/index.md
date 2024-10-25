---
title:  "HP LaserJet Flow E82660"
date:   2024-10-17 09:00:00 +0530
img: "impressora.png"
categories: [Impressora, Instalação, Driver, PCS]
author: "Suzano Bitencourt"
profile:
  attrs:
    - key: 
      val: 
    - key: 
      val: 
---

Procedimento para instalação da impressora multifuncional laser HP LaserJet Flow E82660.

<!--more-->

## Parte 1: Download do driver

1 - Para fazer o download do driver da impressora, entre no site da HP (<https://support.hp.com/br-pt/product/details/hp-laserjet-managed-mfp-e826dn-printer-series/model/38350966>)

![Site HP](/posts/hp-laserjet-flow-e82660/figura01.png "HP LaserJet Multifuncional Managed E82660dn")

Clique em `Software e drivers`.

![Site HP](/posts/hp-laserjet-flow-e82660/figura02.png "HP LaserJet Multifuncional Managed E82660dn")

2 - Escolha `Driver de impressão universal / HP Universal Print Driver for Windows` e clique em `Baixar` para fazer o download do executável.

3 - Link direto para o download do executável (https://ftp.hp.com/pub/softlib/software13/printers/UPD/upd-pcl6-x64-7.2.0.25780.exe).


## Parte 2: Instalação

1 - Execute o arquivo `upd-pcl6-x64-7.2.0.25780.exe`.

2 - Clique em `Browse...` e escolha um diretório de sua preferência para guardar os drivers e clique em `Unzip` para descompactar os drivers da impressora.

![Unzip](/posts/hp-laserjet-flow-e82660/figura03.png "Unzip")

3 - Um assistente de instalação da HP será aberto. Leia o `Contrato de licença do usuário final` e clique `Sim` para continuar.

![Instalador](/posts/hp-laserjet-flow-e82660/figura04.png "Instalador")

4 - Escolha `Modo Tradicional` e clique em `Avançar`.

![Instalador](/posts/hp-laserjet-flow-e82660/figura05.png "Instalador")

5 - Escolha `Adiocionar uma impressora local ou de rede usando configurações manuais`.

![Instalador](/posts/hp-laserjet-flow-e82660/figura06.png "Instalador")

6 - Escolha `Criar nova porta:` e para o `Tipo de porta:` marque `Standard TCP/IP Port` depois clique em `Avançar`.

![Instalador](/posts/hp-laserjet-flow-e82660/figura07.png "Instalador")

7 - Em `Nome do host ou endereço IP:`, digite o endereço IP da impressora `192.168.X.XX`. **Recomendação:** Desmarque a opção `Consultar a impressora e selecionar automaticamente o driver a ser usado`.

![Instalador](/posts/hp-laserjet-flow-e82660/figura08.png "Instalador")

8 - Para selecionar o driver da impressora, clique em `Com Disco...`.

![Instalador](/posts/hp-laserjet-flow-e82660/figura09.png "Instalador")

9 - Clique em `Procuara...` para selecione o diretório onde foi descompactado o driver da impressora e depois em `OK`.

![Instalador](/posts/hp-laserjet-flow-e82660/figura10.png "Instalador")

10 - Será exibido uma lista dos drivers encontrados no diretório. Selecione o arquivo `HP Universal Printing PCL 6 (v7.2.0)` e clique em `Avançar`.

![Instalador](/posts/hp-laserjet-flow-e82660/figura11.png "Instalador")

11 - No local indicado abaixo, escreva um nome para a sua impressora, por exemplo: `Impressora da Secretaria` e depois em `Avançar`.

![Instalador](/posts/hp-laserjet-flow-e82660/figura12.png "Instalador")

11 - Clique em `Concluir` para instalar.

![Instalador](/posts/hp-laserjet-flow-e82660/figura13.png "Instalador")

12 - Clique em `Concluir` para fechar o assistente de instalação.

![Instalador](/posts/hp-laserjet-flow-e82660/figura14.png "Instalador")

## Parte 3: PS (PostScript) ou PCL (Printer Command Language)

Os drivers **PS (PostScript)** e **PCL (Printer Command Language)** são padrões de linguagem de impressão utilizados para enviar dados de impressão para impressoras, mas eles possuem diferenças significativas que impactam no desempenho e na qualidade de impressão.

---

**Driver PCL (Printer Command Language)** foi criado pela **HP**, e é um padrão amplamente suportado por várias marcas de impressoras e é frequentemente usado em ambientes empresariais.
- **Desempenho:** PCL é rápido e eficiente, pois processa os dados diretamente na impressora, o que reduz o tempo de envio e a carga de trabalho no computador.
- **Qualidade:** Oferece boa qualidade para textos e gráficos simples, mas pode ter limitações em gráficos mais complexos, como aqueles com muitos detalhes ou camadas.
- **Compatibilidade:** É altamente compatível com documentos de escritório e ambientes que exigem velocidade de impressão.

---

**Driver PS (PostScript)** foi desenvolvido pela **Adobe**, e é uma linguagem voltada para gráficos, ideal para documentos complexos ou que requerem alta precisão gráfica, como publicações e designs.
- **Desempenho:** O processamento é feito primeiro no computador (RIP – Raster Image Processing) e depois enviado para a impressora. Isso pode aumentar o tempo de envio, especialmente em documentos gráficos.
- **Qualidade:** Fornece uma qualidade superior para documentos com muitos gráficos, imagens em alta resolução e cores complexas, pois oferece um controle mais preciso.
- **Compatibilidade:** O PS é mais comum em ambientes que exigem qualidade gráfica, como editoras e agências de design.

---

**Qual escolher?**

Se o objetivo é imprimir documentos comuns e rápidos, o **PCL** é mais recomendado. Para trabalhos gráficos ou documentos que exigem alta precisão na impressão, o **PS** será a melhor escolha devido à sua fidelidade e qualidade.

## Parte 4 - Modos de Comunição

Existem 3 modos de comunicação que ajustes a forma como a impressora se comunica com o computador e como ela se integra à rede.

**Modo Tradicional**
- **Uso:** Indicado para instalações em redes de maior porte ou em configurações de rede estáticas e controladas, como em escritórios empresariais.
- **Configuração:** Conecta a impressora diretamente ao computador ou à rede usando um IP estático (fixo), o que facilita o gerenciamento e o suporte técnico em redes maiores.
- **Vantagem:** Como o IP da impressora é fixo, o modo tradicional evita problemas de conexão devido a alterações de endereço IP, proporcionando maior estabilidade em redes corporativas.
- **Contras:** Pode exigir mais configuração inicial, especialmente ao definir IPs e outras configurações de rede.

---

**Modo Dinâmico**
- **Uso:** Ideal para redes domésticas ou ambientes onde os endereços IP são atribuídos automaticamente por DHCP (Dynamic Host Configuration Protocol).
- **Configuração:** A impressora obtém automaticamente um endereço IP na rede, o que facilita a configuração em redes onde dispositivos entram e saem com frequência.
- **Vantagem:** Menos configuração manual e mais adaptabilidade para redes que mudam frequentemente, como redes domésticas.
- **Contras:** O endereço IP da impressora pode mudar periodicamente, o que pode exigir uma reconfiguração em alguns casos.

---

**Modo USB**
- **Uso:** Quando a impressora será conectada diretamente ao computador via cabo USB, sem necessidade de conexão em rede.
- **Configuração:** Não requer uma rede, pois o driver é instalado para uso direto pelo USB.
- **Vantagem:** Instalação rápida e simples, ideal para usuários que não precisam de uma conexão de rede, como em instalações individuais ou para usuários que precisam imprimir diretamente.
- **Contras:** Limita a conectividade apenas ao computador ao qual está conectada, sem opção de compartilhamento direto para outros dispositivos na rede.

---

**Qual modo escolher?**
- Modo tradicional: Ambientes empresariais ou redes grandes.
- Modo dinâmico: Redes domésticas ou redes menores.
- Modo USB: Computadores individuais.

## Ilustrações

**CAPTURA DE TELA - Próprio editor**  
Disponível em: <https://suzano.github.io/posts/hp-laserjet-flow-e82660/>  
Acesso em: 17 out. 2024.

**PIXABAY**  
Disponível em: <https://pixabay.com/pt/vectors/computador-dados-base-de-dados-1294359/>  
Acesso em: 17 out. 2024.

## Referências

**HP - Bem-vindo ao Software e Drivers HP**  
Disponível em: <https://support.hp.com/br-pt/drivers/printers>  
Acesso em: 17 out. 2024.