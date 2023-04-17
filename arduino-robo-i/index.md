# Construindo um Robô Arduino - Parte I


Construindo um veículo robô controlado remotamente.

Usando Arduino para a plataforma de hardware, por ser amplamente utilizada por criadores de hardware em todo o mundo, o que significa que há muitas informações e recursos disponíveis.

Sendo fácil o suficiente para concluir em um período de tempo relativamente curto, mas difícil o suficiente para ser interessante e desafiador.

<!--more-->

{{< admonition >}}
Este artigo é uma tradução vergonhosa da página do [miguelgrinberg.com](https://blog.miguelgrinberg.com/post/building-an-arduino-robot-part-i-hardware-components).
{{< /admonition >}}

## Recursos e Funções do Robô

Recursos e funções:
- Deve ser um veículo que pode se mover para frente, para trás e virar.
- Deve ser fácil de montar e desmontar.
- Deve ter um modo em que seja capaz de se mover por conta própria, detectando os obstáculos à frente e evitando-os.
- Deve ter um modo em que possa ser totalmente controlado a partir do meu smartphone Android.
- Deve ser fácil de hackear, mudar e melhorar.

## Lista de Dispositivos

Lista de dispositivos usados para projeto:
- Placa Arduino
- Controle de motor
- Sensor de distância
- Escravo Bluetooth
- Placa de prototipagem e cabos
- Cabo USB
- Kit de veículo

### Placa Arduino

Arduino é uma plataforma eletrônica de código aberto baseada em hardware e software fáceis de usar. As placas Arduino são capazes de ler entradas de um sensor, transformá-las em uma saída, ativando um motor, ligando um LED ou até publicando algo online. Você pode dizer à sua placa o que fazer enviando um conjunto de instruções para o microcontrolador na placa. Para isso utiliza-se a linguagem de programação Arduino (baseada em Wiring), e o Software Arduino (IDE), baseado em Processamento.

### Controle de Motor

A placa Arduino não pode controlar diretamente um motor. Para essa função existe um circuito especializado chamado `H-Bridge`, e existem várias implementações deste circuito prontamente disponíveis para a plataforma Arduino, ou você também pode construir um a partir de peças básicas por quase nada.

### Sensor de Distância

Os sensores de distância enviam um sinal ultrassônico para a frente e, em seguida, aguardam para receber um sinal rebatido. Dependendo de quanto tempo o sinal leva para retornar, a distância aproximada de um obstáculo pode ser calculada. Vamos usar este pequeno dispositivo para evitar que o robô bata em paredes ou outros obstáculos em seu caminho.

### Escravo Bluetooth

A maneira mais fácil de controlar o robô a partir de um smartphone é através da interface serial bluetooth que todos os smartphones modernos possuem. O telefone funcionará como um mestre, então eu precisava de um escravo bluetooth para o robô.

### Placa de prototipagem (protoboard) e cabos

Para poder montar e desmontar o robô à vontade sem estragar nenhuma peça, usaremos uma  placa de prototipagem (protoboard) e diversos cabos não havendo necessidade de nenhuma solda.

### Cabo USB

A placa Arduino é conectada a um computador através de uma porta USB. A conexão USB é usada para carregar software e também pode ser usada como fonte de energia durante o teste.

### Kit de veículo

Existem muitas opções de kit para veículos com Arduino. Os únicos requisitos é um com o tamanho suficiente para suportar a plataforma e todas as peças, incluindo as rodas e motores.

## Ilustrações

**PIXABAY**  
Disponível em: <https://pixabay.com/pt/photos/circuito-integrado-computador-441294/>  
Acesso em: 17 abr. 2023.

## Fontes

**MIGUELGRINBERG.COM**  
Disponível em: <https://blog.miguelgrinberg.com/post/building-an-arduino-robot-part-i-hardware-components>  
Acesso em: 17 abr. 2023.

**ARDUINO.CC**  
Disponível em: <https://www.arduino.cc>  
Acesso em: 17 abr. 2023. 
