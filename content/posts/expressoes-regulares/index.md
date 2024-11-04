---
title:  "Expressões Regulares"
date:   2024-09-25 09:00:00 +0530
img: "regex.png"
categories: [Linguagem]
author: "Suzano Bitencourt"
profile:
  attrs:
    - key: 
      val: 
    - key: 
      val: 
---

Expressões Regulares (ou "Regex") são uma ferramenta poderosa para buscar e manipular padrões em textos, muito úteis para tarefas de programação e análise de dados.

<!--more-->

## Conceito


## Parte 1: Guia básico

1 - Sintaxe básica:
```
. : qualquer caractere, exceto nova linha.
* : zero ou mais repetições do caractere anterior.
+ : uma ou mais repetições do caractere anterior.
? : zero ou uma ocorrência do caractere anterior (torna-o opcional).
\d : qualquer dígito.
\w : qualquer letra, dígito ou sublinhado.
\s : espaço em branco.
^ : início da linha.
$ : fim da linha.
```

2 - Agrupamento e alternância:
```
(abc) : corresponde exatamente ao padrão abc.
[a-z] : corresponde a qualquer caractere entre a e z.
(abc|def) : corresponde a abc ou def.
```

3 - Exemplos práticos:
```
Encontrar números de telefone: \(\d{2}\)\s\d{4,5}-\d{4}.
Validar e-mails: \b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,7}\b.
```

## Parte 2: Testar suas Expressões Regulares


Alguns sites onde você pode praticar e testar suas expressões regulares de forma interativa:
- **Regex101** (<https://regex101.com/>): Este site oferece uma interface intuitiva e explica cada parte da expressão regular. É compatível com diversas linguagens, como Python, JavaScript, e PHP.
- **RegExr** (<https://regexr.com/>): Com uma interface visual e prática, este site permite testar e construir expressões regulares, além de fornecer tutoriais e exemplos comuns.
- **RegexPlanet** (<https://www.regexplanet.com/>) : Permite testar regex em diferentes linguagens, sendo útil para ver como a mesma expressão regular se comporta em diferentes ambientes.
- **Regexper** (<https://regexper.com/>): Gera uma visualização gráfica das expressões regulares, ajudando a entender a estrutura de regex mais complexas.
- **Debuggex** (<https://www.debuggex.com/>): Outra ferramenta que oferece uma representação visual, excelente para ver o comportamento de expressões complexas e otimizar seu uso.

## Parte 3: Aplicação em formulários

### Validação de Nomes

Entendendo os requisitos:
- Máximo de 150 caracteres: Precisamos limitar o comprimento da string.
- Sem ponto ou espaço após uma letra: Queremos evitar nomes como "J. da Silva" ou "J da Silva".

Expressão regular que atende a esses requisitos é:
```
^[a-zA-ZÀ-ÿ']{2,150}(?: [a-zA-ZÀ-ÿ']{2,150})*$
```

Explicando cada parte:
```
1. ^: Indica o início da string.
2. [a-zA-ZÀ-ÿ']{2,150}: Permite de 2 a 150 letras (maiúsculas ou minúsculas).
3. (?: [a-zA-ZÀ-ÿ']{1,150})*: Permite zero ou mais ocorrências de um espaço seguido de 2 a 150 letras.
    - O ?: indica um grupo não capturante.
4. $: Indica o final da string.
```

### Validação de Número com Máximo de 12 Caracteres

Entendendo os requisitos:
- Somente números com no máximo 12 caracteres.

Expressão regular que atende a esses requisitos é:
```
^\d{1,12}$
```

Explicando cada parte:
```
1. ^: Indica o início da string.
2. \d: Representa qualquer dígito numérico (0-9).
3. {1,12}: Quantificador que indica que o dígito anterior (\d) pode ocorrer de 1 a 12 vezes.
4. $: Indica o final da string.
```

### Validação de URLs

Entendendo os requisitos:
- Início: A URL deve começar com https://, http:// ou www..

Expressão regular que atende a esses requisitos é:
```
^(https?:\/\/)([a-zA-Z0-9-]+\.)+[a-zA-Z]{2,}(\/[^\s]*)?$
```

Explicando cada parte:
```
1. ^: Início da string.
2. (https?:\/\/): Verifica se o endereço começa com http:// ou https://.
    - https?: s é opcional, permitindo http ou https.
    - :\/\/: Literalmente corresponde aos caracteres ://.
3. ([a-zA-Z0-9-]+\.)+: Garante que o endereço contenha um domínio válido, permitindo letras (a-zA-Z), números (0-9), e hífens (-), seguido por pelo menos um ponto ..
    - O + permite que subdomínios adicionais, como www. ou sub.dominio., sejam incluídos.
4. [a-zA-Z]{2,}: Exige uma extensão de domínio com pelo menos duas letras (como .com, .org, etc.).
5. (\/[^\s]*)?: Opcionalmente permite um caminho após o domínio, começando com / e seguido de qualquer caractere que não seja um espaço.
    - O ? indica que o caminho após o domínio é opcional.
6. $: Indica o fim da linha, garantindo que todo o texto corresponda ao padrão.
```

### Validação de Texto com até 300 Carateres

Entendendo os requisitos:
- Limitar um campo a no máximo de 300 caracteres.

Expressão regular que atende a esses requisitos é:
```
^.{1,300}$
```

Explicando cada parte:
```
1. ^: Indica o início da linha.
2. .{1,300}:
    - . representa qualquer caractere (exceto quebras de linha).
    - {1,300} limita o título a entre 1 e 300 caracteres.
3. $: Indica o fim da linha.
```

### Validação de Texto Com Formato Específico

Entendendo os requisitos:
- Limitar um campo do tipo texto com o seguinte formato. SIGLA - Nome da Instituição - Departamento

Expressão regular que atende a esses requisitos é:
```
^[A-Z]{2,10} - [A-Za-zÀ-ÿ0-9\s]+ - [A-Za-zÀ-ÿ0-9\s]+$
```

Explicando cada parte:
```
1. ^: Indica o início da linha.
2. [A-Z]{2,10}:
    - [A-Z]: Exige letras maiúsculas de A a Z.
    - {2,10}: Limita a sigla a entre 2 e 10 letras.
3. -: Espaços e hífens literais que separam a sigla de "Nome da Instituição" e o "Departamento".
4. - [A-Za-zÀ-ÿ0-9\s]+:
    - [A-Za-zÀ-ÿ0-9\s]: Permite letras (maiúsculas e minúsculas), acentos, números, e espaços.
    - +: Exige pelo menos um caractere para o nome e o departamento.
5. -: Outro espaço e hífen literal para separar o nome da instituição do departamento.
6. [A-Za-zÀ-ÿ0-9\s]+: Repete a estrutura para o "Departamento".
7. $: Indica o fim da linha.
```

## Ilustrações

**ICONDUCK**  
Disponível em: <https://iconduck.com/icons/20674/regex>  
Acesso em: 25 set. 2024.

## Referências

**DEVMEDIA - Iniciando Expressões Regulares**  
Disponível em: <https://www.devmedia.com.br/iniciando-expressoes-regulares/6557>  
Acesso em: 25 set. 2024.

**DEVELOPER MOZILLA ORG - Expressões Regulares**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Regular_expressions>  
Acesso em: 25 set. 2024.

**MEDIUM - Regex: O Guia Essencial das Expressões Regulares**  
Disponível em: <https://blog.dp6.com.br/regex-o-guia-essencial-das-express%C3%B5es-regulares-2fc1df38a481>  
Acesso em: 25 set. 2024.

**GIOVANNI REIS NUNES - Expressões Regulares**  
Disponível em: <https://giovannireisnunes.wordpress.com/?s=regulares>  
Acesso em: 25 set. 2024.