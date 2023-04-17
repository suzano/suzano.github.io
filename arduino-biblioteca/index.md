# Criando uma biblioteca para Arduino


Criando uma biblioteca que tem a função de facilitar o código PISCA LED, com a biblioteca pronta e inserida no código, o led irá piscar com apenas 01 linha de programação!

<!--more-->

## Conceito

O que é uma Biblioteca?

Uma biblioteca ou pacote é um conjunto de instruções desenvolvidas para executar algumas tarefas específicas relacionadas a um determinado, sensor, processo ou atuador.

Por exemplo, uma biblioteca para a Ponte H L298N, a biblioteca dele seria L298N.h e ela possuiria funções desenvolvidas especificamente para rodar tarefas como, configurar os pinos de comando para os motores DC, aceleração dos motores, sentido da rotação dos motores e etc. Facilitando o desenvolvimento de um código o tornando mais simples e organizado.

## Parte 1: Estrutura da biblioteca

```
Nome da pasta deve ser igual ao nome do arquivo .h e .cpp

 -----------          ----------
| exemples/ |  --->  | exemplo1 |
 -----------          ----------

                      --------
               --->  | Nome.h |
 ------       |       --------
| src/ |   ---
 ------       |       ----------
               --->  | Nome.cpp |
                      ----------
 
 --------------------
| library.properties |
 -------------------- 
```

## Parte 1: Criando uma função simples

Abra a IDE do Arduino e carregue o exemplo `Blink`:

Menu Arquivo > Exemplos > 01.Basics > Blink

```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);                    
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}
```

Altere o código para criar uma função `acende_led()`:

```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}
void loop() {
  acende_led();
}

void acende_led(){
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);                    
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);

}
```

## Parte 2: Criando estrutura de diretórios

Abre o Explorer e crie a seguinte estrutura de pastas dentro de `Este Computador\Documentos\Arduino\libraries\`.

```
Arduino
  └ libraries
      └ PiscaLed
        ├ examples
        |   └ PiscaLed.ino
        ├ src
        |   ├ PiscaLed.h
        |   └ PiscaLed.cpp
        └ libraries.properties
```


## Parte 3: Código do arquivo PiscaLed.h

Para começar a criar a biblioteca, abra o nome `PiscaLed.h`.

Digite o seguinte código e salve:

```cpp
#ifndef _PISCALED_H
#define _PISCALED_H

#include <Arduino.h>

class PiscaLed {
  private:
    
  public:
    PiscaLed(int pino, long tempo); // Construtor
    void acende_led();     
};
#endif
```

No código da extensão `.h` tem algumas instruções como o `class`, `public`, `private` e `#endif`, alguns desses conceitos são derivados da programação orientada a objetos (POO):

- `class`: é com essa palavra chave/reservada que criamos uma classe, que em nosso caso definimos ser pisca.
- `public`: é quando queremos definir que a variável/função dentro dessa estrutura é pública, o que em orientação objetos quer dizer que podemos acessar a variável/função dentro e fora da classe originária.
- `private`: é quando quero definir que a variável/função dentro dessa estrutura é privada, isso quer dizer que só é possível acessar dentro da própria classe que contém a variável/função.
- `#ifndef`: Esta diretiva verifica se o identificador não está definido no momento.
- `#endif`: Esta diretiva acaba com o escopo da diretiva.


## Parte 4: Código do arquivo PiscaLed.cpp

Para começar a criar a biblioteca, abra o nome `PiscaLed.cpp`.

Digite o seguinte código e salve:

```cpp
#include <PiscaLed.h>

// Globais
int _pino;
long _tempo;

PiscaLed::PiscaLed(int pino, long tempo){
  // pino e tempo só podem ser acessados de dentro dessa função
  pinMode(pino, OUTPUT);
  _pino = pino;
  _tempo = tempo;
}

void PiscaLed::acende_led(){
  digitalWrite(_pino, HIGH);
  delay(_tempo);                    
  digitalWrite(_pino, LOW);
  delay(_tempo);
}
```

## Parte 5: Código do arquivo PiscaLed.ino

Para começar a criar a biblioteca, abra o nome `PiscaLed.ino`.

Digite o seguinte código e salve:

```cpp
#include "PiscaLed.h"

PiscaLed p(13, 1000);

void setup() {
  
}
void loop() {
  p.acende_led();
}
```

## Ilustrações

**PIXABAY**  
Disponível em: https://pixabay.com/pt/photos/circuito-integrado-computador-441291/  
Acesso em: 14 abr. 2023.

## Fontes

**ARDUINO ÔMEGA - Criando uma biblioteca para Arduino**  
Disponível em: <https://blog.arduinoomega.com/criando-uma-biblioteca-para-arduino/>  
Acesso em: 14 mar. 2023.

**Lobo da Robótica - Como criar bibliotecas para Arduino? (O GUIA DEFINITIVO)**  
Disponível em: <https://www.youtube.com/watch?v=-tT0ZYQVRe4>
Acesso em: 14 abr. 2023.
