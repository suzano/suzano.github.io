# Construindo um Robô Arduino - Parte III


Um Firmware de Robô Básico (Não Tão)

Esboço do Arduino que faz o robô correr para frente.

A idéia é escrever o esboço de forma que me permita adicionar funcionalidades mais complexas posteriormente sem ter que começar do zero. Estabelecendo uma base sólida sobre a qual empilharemos as peças mais complexas posteriormente.

<!--more-->

{{< admonition >}}
Este artigo é uma tradução vergonhosa da página do [miguelgrinberg.com](https://blog.miguelgrinberg.com/post/building-an-arduino-robot-part-iv-a-not-so-basic-robot-firmware).
{{< /admonition >}}

## Metas

Objetivos do projeto do ponto de vista da engenharia de software.

### Estrutura Escalável

Para esboços simples, a estrutura de esboço padrão baseada nas funções `setup()` e `loop()` é suficiente. Os esboços anteriores foram para testar todos os componentes do robô e aprender a programar esses componentes.

O problema é que essa estrutura não `escala` bem. Para o projeto do robô, precisaremos controlar dois motores, o sensor de distância e reagir a comandos remotos vindos do bluetooth, tudo ao mesmo tempo. No futuro, podemos querer estendê-lo com ainda mais dispositivos controlados. Talvez sensores de distância adicionais nas laterais e atrás, ou um olhando para baixo para detectar quando o veículo chega ao final de uma mesa. Talvez até montar uma câmera sem fio ou adicionar recursos de som. As possibilidades são infinitas e cada novo dispositivo adicionado aumentará a complexidade do esboço.

A função `loop()` precisaria ficar muito longa e complexa para fazer tudo e, em seguida, fazer alterações nela se tornaria um pesadelo, com qualquer alteração que se  fizesse, correria o risco de quebrar inadvertidamente a funcionalidade existente. O esboço acabaria sendo um [`código espaguete`](https://pt.wikipedia.org/wiki/C%C3%B3digo_espaguete) (spaghetti code).

Para este projeto usaremos técnicas de orientação a objetos para organizar o código do esboço e torná-lo mais fácil de escrever, testar, manter e modificar.

### Abstrações de dispositivo

Este esboço esta disponível como código aberto. É seguro presumir que outras pessoas construirão seus próprios veículos robóticos usando peças diferentes das que estamos usando nesta montagem. Por exemplo, alguém pode usar uma placa de driver de motor diferente ou usar wi-fi para o controle remoto em vez de bluetooth. Se construirmos um esboço com a suposição de que os componentes do robô são apenas aqueles para os que estamos usando nesta montagem, apenas alguns poucos poderão se beneficiar imediatamente e a maioria terá que hackear para fazê-lo funcionar para eles.

Em vez disso, pensaremos sobre a funcionalidade que desejamos implementar em termos gerais e, depois, escrever drivers de dispositivo para os módulos de que precisamos.

Dando à outros a liberdade de substituir peças no robô sem precisar modificar o esboço principal. Mudar de bluetooth para wi-fi exigirá apenas escrever um novo driver de comunicação remota. O esboço principal falará com os drivers bluetooth ou wi-fi e não saberá a diferença!

### Configuração

A ideia é que deva ser fácil configurar o software do robô para o hardware real. O melhor exemplo é o uso de pinos na placa Arduino. Não vamos codificar nenhum número de pino. Em vez disso, adicionarei constantes `#define` na parte superior do esboço com todos os pinos, para que alterar as atribuições dos pinos se torne uma tarefa trivial.

Mas a configuração não se limita a números de pinos. Existem também alguns padrões operacionais (como a distância até uma parede ou obstáculo quando o robô para e gira) que também podem ser considerados parte da configuração e serão representados por constantes na parte superior do esboço para os usuários modificarem facilmente.

### Timing mais inteligente

Em esboços simples, tende-se a abusar da função `delay()` como uma maneira fácil de fazer com que as ações durem um certo tempo. 

Mas para um projeto real que precisa fazer muitas coisas ao mesmo tempo isso é `impraticável`. Mas na plataforma Arduino há um único `thread` de execução, então chamar `delay()` faz todo o programa entrar em hibernação, e isso não é bom para funcionamento do robô.

Um ambiente `multithreading`, é a forma ideal de fazer um programa fazer muitas coisas ao mesmo tempo. Uma chamada de thread `delay()` não impediria a execução de outras threads. 

Portanto, não usaremos `delay()`para nada, exceto para testes de descarte.

Parte do segredo está em fazer a função `loop()` fazer apenas uma pequena quantidade de trabalho e retornar. A função `loop()` será chamada em um ritmo muito rápido (lembre-se de que ela é chamada repetidamente até que a placa seja desligada). Cada vez que `loop()` é chamado, podemos descobrir qual é o tempo de atividade. Saber a hora atual permitirá implementar um equivalente bloqueio ou espera, sem usar o `delay()`.

## Escrevendo um driver de dispositivo!

Vamos começar escrevendo um driver de dispositivo que saiba como controlar motores.

Um driver de dispositivo é simplesmente uma abstração para o dispositivo pretendido. Agora estamos escrevendo um para um motor, então a operação básica que esse driver deve saber fazer é definir a velocidade do motor.

Vamos armazenar os drivers de dispositivo em arquivos de cabeçalho, que são arquivos com extensão `.h`. Para módulos pequenos, usar um arquivo de cabeçalho é uma boa escolha. Para módulos maiores, a norma é armazenar o código em um arquivo fonte com extensão `.cpp` e depois escrever um pequeno arquivo de cabeçalho que contenha apenas a declaração das funções públicas do arquivo fonte. Os arquivos de cabeçalho funcionam para neste momento, se no futuro um módulo crescer para um tamanho decente, podemos mover o código para um arquivo `.cpp`.

A intenção é que o driver do dispositivo do motor permita que o esboço principal funcione com diferentes controladores de motor usando as mesmas chamadas de função, portanto, a primeira tarefa ao definir um driver é decidir quais serão as funções comuns do driver.

Aqui está o código do driver de dispositivo motor, que vamos armazenar em um arquivo chamado `motor_driver.h`:

```cpp
namespace Michelino
{
    class MotorDriver
    {
    public:
        /**
         *  Use positive values to run the motor forward, 
         *  negative values to run it backward and zero to stop the motor.
         */
        virtual void setSpeed(int speed) = 0;

        /**
         * Return the current speed of the motor.
         * The current speed of the motor with range -255 to 255.
         */
        virtual int getSpeed() const = 0;            
    };
};
```

Se você não estiver familiarizado com C++, há várias coisas aqui que precisam de uma explicação.

Qualquer texto que apareça entre `/*` e `*/` é considerado um comentário, portanto será ignorado pelo compilador C++. Existe um formato alternativo para comentários que você já deve ter visto, esses usam um prefixo `//` e vão até o final da linha. Ambos os formatos são válidos, mas neste caso, como estou escrevendo comentários de várias linhas, estou usando o formato `/* ... */`.

A palavra-chave `namespace` agrupa todas as definições dentro `{` e `}` sob um nome definido pelo usuário. Isso é útil para evitar colisões de nomes com outros módulos, por isso é sempre uma boa ideia incluir seu próprio código em um `namespace`. Colocamos todo o código sob o namespace `Michelino`.

A palavra-chave `class` define uma estrutura que agrupa dados e funções em uma entidade chamada `objeto`. Minha classe de driver de motor é chamada `MotorDriver` e contém apenas duas funções, que no contexto de uma `classe` são chamadas de `métodos`. Os métodos `setSpeed` e `getSpeed` controlarão um motor, mas observe que, ao contrário da biblioteca `AF_Motor` que usamos antes, não estamos definindo que tipo de controlador de motor é usado para a tarefa. O esboço principal apenas chamará esses métodos sem saber como eles são implementados, portanto, para alternar de um controlador para outro, basta reimplementar essas duas funções para o controlador selecionado.

A apalavra-chave `public:` que aparece antes dos métodos indica que as declarações a seguir são acessíveis a qualquer pessoa. Você verá mais tarde que algumas classes têm conteúdos que estão escondidos do mundo exterior.

A palavra-chave `virtual` que inicia cada declaração de método indica que esses métodos podem ser sobrescritos por uma subclasse, e no final `= 0` das declarações indica que os métodos não possuem uma implementação. Esses dois atributos combinados são usados ​​para garantir que a única maneira de fornecer uma implementação para esses métodos seja em uma `subclasse`.

Por fim, a palavra-chave `const` que aparece no método `getSpeed` indica que esse método é constante, ou seja, que esse método não altera o estado interno do objeto.

Deixando de lado os detalhes técnicos de escrever uma classe C++, o ponto importante é que os drivers de dispositivo que adotam a interface acima devem ser capazes de controlar um motor DC com duas operações, `setSpeed()` e `getSpeed()`. Os valores de velocidade são dados na faixa de `-255` a `255`, com velocidades positivas movendo-se para `frente`, velocidades negativas movendo-se para `trás` e `zero` fazendo o motor `parar`.

## O driver de motor Adafruit

Escrevendo uma implementação específica para a shield de motor Adafruit.

Vou armazenar o driver da shield do motor Adafruit em um arquivo chamado `adafruit_motor_driver.h`. Aqui está o código:

```cpp
#include "motor_driver.h"

namespace Michelino
{
    class Motor : public MotorDriver
    {
    public:
        /*
         * Class constructor.
         * number the DC motor number to control, from 1 to 4.
         */
        Motor(int number)
            : MotorDriver(), motor(number), currentSpeed(0)
        {
        }

        void setSpeed(int speed)
        {
            currentSpeed = speed;
            if (speed >= 0) {
                motor.setSpeed(speed);
                motor.run(FORWARD);
            }
            else {
                motor.setSpeed(-speed);
                motor.run(BACKWARD);
            }
        }

        int getSpeed() const
        {
            return currentSpeed;
        }

    private:
        AF_DCMotor motor;
        int currentSpeed;
    };
};
```

Iniciamos incluindo o arquivo de cabeçalho do driver do motor. O driver Adafruit deriva da definição de driver genérico que escrevemos acima, de modo que a definição precisa ser acessível.

A definição `class` neste arquivo parece um pouco diferente:

```cpp
class Motor : public MotorDriver
```

Isso diz que estamos criando uma classe chamada `Motor` que deriva da classe `MotorDriver`. Isso significa que a classe `Motor` seguirá o protocolo estabelecido pela classe `MotorDriver`.

A classe tem uma seção `public` que começa com constructor:

```cpp
Motor(int number)
```

Este é um método com o mesmo nome da classe (Motor neste caso). Os métodos construtores são chamados quando um objeto é criado e destinam-se a definir o estado inicial do objeto. Este construtor usa o número do motor como um argumento.

O construtor `Motor` tem uma lista de inicializadores:

```cpp
: MotorDriver(), motor(number), currentSpeed(0)
```

Esta é uma lista de itens que serão inicializados quando um objeto desta classe for criado. O primeiro item apenas invoca o construtor da classe pai, o driver genérico `MotorDriver`. Eu não incluí um construtor nesta classe, mas o compilador irá gerar um vazio. É uma boa prática sempre inicializar a `classe pai` mesmo quando não houver um construtor, porque no futuro um construtor pode ser adicionado.

Os dois itens restantes na lista de inicializadores são `variáveis` ​​de membro dessa classe. Se você olhar na parte inferior da classe, há um bloco `private` que define duas variáveis ​​chamadas `motor` e `currentSpeed`. A variável `motor` é do tipo `AF_DCMotor`, a classe definida pela biblioteca da shield do motor Adafruit. Para inicializar esta variável, tenho que invocar seu construtor, que, se você se lembra de um artigo anterior, usa o número do motor como argumento. Recebi o número do motor como um argumento para meu próprio construtor, então apenas o transmito aqui. A variável `currentSpeed` é do tipo int, então apenas a inicializo com `0` para que ela tenha um valor inicial conhecido.

O corpo do construtor `Motor` está vazio, pois a única coisa que preciso é inicializar as variáveis ​​de membro.

O que se segue é a implementação dos métodos setSpeede getSpeedpara este controlador de motor específico, usando a biblioteca AF_Motor de código aberto da Adafruit, que deve ser instalada separadamente (consulte meu artigo anterior para obter instruções). Esta biblioteca requer duas funções a serem chamadas para configurar um motor, uma para definir a velocidade e outra para definir o modo. Eu defini meu driver de motor para usar uma forma mais simples de configurar o motor, apenas com uma velocidade que pode ser positiva, negativa ou zero. A implementação de setSpeedtraduz meu formato para aquele exigido pela biblioteca de escudos do motor Adafruit. Eu também armazeno a velocidade atual em uma variável de membro, para que eu possa retorná-la em getSpeed.

Na parte inferior estão as duas variáveis ​​de membro privadas que esta classe usa. Essas variáveis ​​são declaradas como privadas porque não quero que sejam acessíveis de fora do objeto que as possui. Quero que qualquer alteração no motor ou em sua velocidade seja realizada por meio das funções públicas do driver (seguindo o princípio do encapsulamento ), portanto, uma boa maneira de evitar que eu use acidentalmente as variáveis ​​de membro diretamente é torná-las privadas. Uma variável de membro privado só pode ser modificada de métodos que pertencem ao objeto, mas não é acessível de nenhum outro lugar no código. Um bom motivo para ocultar essas variáveis ​​de membro é que outros drivers de motor precisarão de variáveis ​​diferentes, desde que o código fora dessa classe apenas chame setSpeed()egetSpeed()trocar este driver por outro não deve ser um problema.

Se você estiver usando um controlador de motor diferente do meu em seu robô, tudo o que você precisa fazer é copiar o adafruit_motor_driver.harquivo <your_controller>_motor_driver.he implementar a classe conforme apropriado para seu controlador. O único requisito é que a nova classe também seja chamada Motore tenha as mesmas duas funções públicas. As duas classes serão então conceitualmente equivalentes, então o esboço principal pode usar qualquer uma delas.

## Usando o driver de dispositivo

Agora eu tenho um driver de dispositivo completo para minha bplindagem de motor Adafruit. Mas como faço para usá-lo em um esboço?

Isso é realmente mais simples do que você pode pensar. Aqui está um esboço de exemplo que inicia um motor em velocidade máxima usando o driver Adafruit que acabei de construir:

```cpp
#include <AFMotor.h>
#include "adafruit_motor_driver.h"
#define MOTOR_INIT 1

Michelino::Motor motor(MOTOR_INIT);

void setup()
{
    motor.setSpeed(255);
}

void loop()
{
}
```

O `#include` no topo traz a biblioteca de motores `Adafruit` e do `driver` para ela.

Observe como o `objeto` motor é criado:

```cpp
Michelino::Motor motor(MOTOR_INIT);
```

A notação `Michelino::Motor` diz ao compilador para localizar a classe `Motor` dentro do namespace `Michelino`.

Uma vez que o objeto do motor é criado, ele pode ser controlado usando as funções do driver `setSpeed` e `getSpeed`.

Agora vamos supor que mais tarde você queira fazer o esboço acima funcionar com outra shield de motor, digamos uma chamada `"x"`, para a qual você escreveu um driver de dispositivo. Então você pode apenas adicionar algumas linhas de código ao sketch, como segue:

```cpp
// enable one of the motor shields below
//#define ENABLE_ADAFRUIT_MOTOR_DRIVER
#define ENABLE_X_MOTOR_DRIVER

#ifdef ENABLE_ADAFRUIT_MOTOR_DRIVER
#include <AFMotor.h>
#include "adafruit_motor_driver.h"
#define MOTOR_INIT 1
#endif

#ifdef ENABLE_X_MOTOR_DRIVER
#include <XMotor.h>
#include "x_motor_driver.h"
#define MOTOR_INIT 2
#endif

Michelino::Motor motor(MOTOR_INIT);

void setup()
{
    motor.setSpeed(255);
}

void loop()
{
}
```

No topo, estamos definindo duas constantes `#define`, mas uma delas está comentada. Esta é uma maneira muito fácil de fornecer configuração, basta descomentar a única constante que corresponde à parte que você possui.

Um bloco `#ifdef ... #endif` só será visto pelo compilador se a constante que segue `#ifdef` estiver definida. Como apenas uma das constantes de blindagem do motor será definida, estou carregando efetivamente apenas um dos drivers de dispositivo no esboço.

No exemplo acima, o esboço pode ser alternado entre a blindagem Adafruit usando o motor nº 1 e a blindagem do motor X usando o motor nº 2, apenas alterando qual das #defineinstruções na parte superior é usada!

O esboço principal
Agora que tenho uma solução realmente boa para controlar minhas peças de hardware, preciso pensar em como o esboço principal será estruturado.

Como mencionei antes, ter um grande pedaço de código na loop()função não é ideal porque funções grandes e complexas são difíceis de manter. Se eu criei uma classe para representar um motor, por que não criar também uma classe para representar o robô inteiro?

Aqui está um esboço que define uma classe de ponto inicial para o robô. Este arquivo será nomeado michelino.ino(os esboços do Arduino usam a .inoextensão):

```cpp
/**
 * @file michelino.ino
 * @brief Arduino robot vehicle firmware.
 * @author Miguel Grinberg
 */

#define ENABLE_ADAFRUIT_MOTOR_DRIVER

#ifdef ENABLE_ADAFRUIT_MOTOR_DRIVER
#include <AFMotor.h>
#include "adafruit_motor_driver.h"
#define LEFT_MOTOR_INIT 1
#define RIGHT_MOTOR_INIT 3
#endif

namespace Michelino
{
    class Robot
    {
    public:
        /*
         * @brief Class constructor.
         */
        Robot()
            : leftMotor(LEFT_MOTOR_INIT), rightMotor(RIGHT_MOTOR_INIT)
        {
            initialize();
        }

        /*
         * @brief Initialize the robot state.
         */
        void initialize()
        {
            leftMotor.setSpeed(255);
            rightMotor.setSpeed(255);
        }

        /*
         * @brief Update the state of the robot based on input from sensor and remote control.
         *  Must be called repeatedly while the robot is in operation.
         */
        void run()
        {
        }

    private:
        Motor leftMotor;
        Motor rightMotor;
    };
};

Michelino::Robot robot;

void setup()
{
    robot.initialize();
}

void loop()
{
    robot.run();
}
```

O esboço não deve apresentar surpresas. Começo carregando meu driver de blindagem do motor, usando a #ifdeftécnica que mostrei antes. Quando e se eu escrever novos drivers de motor, adicionarei novas constantes e #ifdefblocos para carregá-los.

Minha classe de robô será nomeada apropriadamente Robote estará dentro do Michelinonamespace. Ele terá inicialmente dois membros de dados privados que representam os dois motores nomeados leftMotore rightMotor. Eles serão inicializados na Robotlista de inicializadores do construtor de classe. A classe tem dois métodos públicos, initialize()que run()serão as contrapartes da classe para setup()e loop(). Nesta versão inicial da classe, o initialize()método inicia os dois motores em velocidade máxima e run()não faz nada.

Depois que a classe é definida, uma instância é criada no escopo global e os métodos setup()e loop()simplesmente chamam os métodos initialize()e run()desse objeto.

O que você acha que acontecerá quando executar esse esboço? O robô vai avançar! Dei algumas voltas e reviravoltas, mas finalmente cumpri minha promessa.

## Como implementar atrasos

Antes de terminar este artigo, vou mostrar como os atrasos podem ser implementados sem realmente usar a delay()função, para que o robô possa fazer outras coisas enquanto espera, como receber e executar comandos remotos.

Para mostrar como isso é feito, vou modificar o esboço acima para fazer o robô começar esperando por cinco segundos, depois avançando por oito segundos e repetindo o ciclo.

Primeiro, adicionarei o conceito de estado ao robô. Para este exemplo, terei dois estados possíveis, parado e em execução . Para definir esses estados no sketch vou usar uma enumeração C++ :

```cpp
    private:
    enum state_t { stateStopped, stateRunning };
    state_t state;
```

A enuminstrução cria um tipo enumerado definido pelo usuário chamado state_t. A segunda instrução define uma nova variável de membro nomeada statedesse tipo. A statevariável de membro terá um dos dois valores possíveis, stateStoppedou stateRunning. Eu poderia facilmente ter usado uma intvariável e chamar o estado 0 de estado parado e o estado 1 de estado em execução, mas depois que você me ver usando essa variável, tenho certeza de que concordará comigo que usar tipos enumerados torna o código muito mais legível e mais fácil de entender.

Vou adicionar outra variável de membro à Robotclasse que me ajudará a contar o tempo:

```cpp
private:
    unsigned long startTime;
```

O tipo da startTimevariável é unsigned long. Este é o tipo em que as unidades de tempo são retornadas pela função millis()fornecida pelas bibliotecas do software Arduino.

Em seguida, no initialize()método em vez de ligar os motores, agora vou inicializar o estado do robô e registrar a hora atual:

```cpp
  void initialize()
    {
        state = stateStopped;
        startTime = millis();
    }
```

E por fim, no run()método é onde toda a mágica acontece:

```cpp
void run()
    {
        unsigned long currentTime = millis();
        unsigned long elapsedTime = currentTime - startTime;
        switch (state) {
        case stateStopped:
            if (elapsedTime >= 5000) {
                leftMotor.setSpeed(255);
                rightMotor.setSpeed(255);
                state = stateRunning;
                startTime = currentTime;
            }
            break;
        case stateRunning:
            if (elapsedTime >= 8000) {
                leftMotor.setSpeed(0);
                rightMotor.setSpeed(0);
                state = stateStopped;
                startTime = currentTime;
            }
            break;
        }
    }
```

O run()método é chamado repetidamente por meio da loop()função, portanto, aqui posso verificar facilmente quanto tempo se passou subtraindo o startTimeque inicializei initialize()do tempo atual fornecido pela millis()função. Estou armazenando o tempo atual e decorrido em duas variáveis ​​locais que nomeei currentTimee elapsedTime.

O que resta é verificar se terminei de esperar e, se sim, altere o estado do robô. Como o período de espera é diferente dependendo do estado em que o robô está, decidi usar uma switchinstrução, que analisa o valor de uma expressão e executa o bloco de código que começa na caseinstrução correspondente e termina com a breakinstrução .

Então, quando o robô estiver no estado parado, o seguinte código será executado:

```cpp
if (elapsedTime >= 5000) {
                leftMotor.setSpeed(255);
                rightMotor.setSpeed(255);
                state = stateRunning;
                startTime = currentTime;
            }
```

Espera-se que este código seja auto-explicativo. Se o tempo decorrido não chegar a cinco segundos nada acontecerá, a run()função retornará sem nenhuma alteração e um pouco depois será chamada novamente. Eventualmente, o se elapsedTimetornará 5000 milissegundos ou mais, então o código dentro da ifinstrução será executado. E essas instruções iniciam os motores, alteram o estado para stateRunninge redefinem o startTimepara o currentTime, de modo que o tempo decorrido seja redefinido para zero.

A próxima vez run()que executa o estado será stateRunning, então o outro bloco na switchinstrução será executado:

```cpp
  if (elapsedTime >= 8000) {
                leftMotor.setSpeed(0);
                rightMotor.setSpeed(0);
                state = stateStopped;
                startTime = currentTime;
            }
```

E isso funciona exatamente como acima, mas espera oito segundos em vez de cinco.

Fazer coisas neste certamente mais complicado do que usar delay():

```cpp
void run()
        {
            leftMotor.setSpeed(0);
            rightMotor.setSpeed(0);
            delay(5000);
            leftMotor.setSpeed(255);
            rightMotor.setSpeed(255);
            delay(8000);
         }
```

Mas a delay()solução mostrada acima é limitada, pois nada acontece durante essas esperas de cinco e oito segundos. Com a solução de tempo decorrido, será fácil para mim fazer o robô fazer outras coisas enquanto espera, como parar quando chegar muito perto de uma parede ou responder a comandos remotos enviados por bluetooth.

## Ilustrações

**PIXABAY**  
Disponível em: <https://pixabay.com/pt/photos/circuito-integrado-computador-441294/>  
Acesso em: 18 abr. 2023.

## Fontes

**MIGUELGRINBERG.COM**  
Disponível em: <https://blog.miguelgrinberg.com/post/building-an-arduino-robot-part-iv-a-not-so-basic-robot-firmware>  
Acesso em: 18 abr. 2023.

**ARDUINO.CC**  
Disponível em: <https://www.arduino.cc>  
Acesso em: 18 abr. 2023. 
