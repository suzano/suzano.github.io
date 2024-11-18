---
title:  "Comandos para ChatGPT"
date:   2024-11-13 09:00:00 +0530
img: "markdown.png"
categories: [ChatGPT, IA, Comandos]
draft: "True"
author: "Suzano Bitencourt"
profile:
  attrs:
    - key: 
      val: 
    - key: 
      val: 
---

Usando a Inteligência Artificial para otimizar o aprendizado e assimilição de informações.

<!--more-->

## Parte 1: Aprender qualquer coisa

Comandos para aprender qualquer coisa em qualquer área.

1 - Explorar e revisar conteúdos complexos:

```prompt
"Explique [tema] de maneira simples e sugira um plano de estudo para entender melhor."
```

2 - Simular situações de aprendizado prático:

```prompt
"Simule uma conversa ou prática sobre [tema], e me corrija se eu cometer algum erro."
```

3 - Revisar e reforçar conteúdos:

```prompt
"Crie um resumo sobre [tema] para revisão rápida."
```

## Parte 2: Mudança de carreira

Comandos para planejar uma mudança de carreira.

1 - Explorar o mercado de trabalho:

```prompt
"Quais são as oportunidades e desafios na área de [nova carreira]?"
```

2 - Criar um plano de transição de carreira:

```prompt
"Crie um plano de transição de carreira para migrar de [carreira atual] para [nova carreira]."
```

3 - Identificar habilidades a serem desenvolvidas:

```prompt
"Quais são as habilidades essenciais para se destacar em [nova carreira]?"
```

## Parte 3: Mudança de carreira

Comandos para desenvolver novas habilidades em tecnologia.

1 - Criar um plano de estudo personalizado:

```prompt
"Crie um plano de estudo para aprender [habilidade tecnológica]."
```

2 - Obter explicações sobre temas complexos:

```prompt
"Explique [tema de tecnologia] de maneira simples e detalhada."
```

3 - Simular desafios práticos:

```prompt
"Simule um problema prático em [habilidade tecnológica] e me guie na resolução."
```

## Parte 4: Produtividade no trabalho

Comandos para turbinar sua produtividade no trabalho.

1 - Organizar sua agenda e priorizar tarefas:

```prompt
"Ajude-me a organizar meu dia de trabalho priorizando as tarefas mais importantes."
```

2 - Automatizar pequenas tarefas diárias:

```prompt
"Sugira maneiras de automatizar tarefas recorrentes na minha rotina de trabalho."
```

3 - Aprimorar a tomada de decisão:

```prompt
"Analise essas opções e sugira a melhor decisão com base em critérios X, Y e Z."
```

Parte 5: Outros sites de IA

[perplexity.ai](https://www.perplexity.ai/)

1 - Pesquisas na Web:

```prompt
"As principais noticias sobre inteligencia artificial no Brasil nos ultimos 7 dias."
```

2 - Pesquisar vídeos:

```prompt
"Quais são os temas mais polêmicos sobre demartologia hoje?"
```

Continue no chat para refinar a pesquisa:

```prompt
"A minha paciente é jornalista, e ela tem uma pele ótima, qual dessas polêmicas é mais indicado para eu conversar com ele?"
```

Magic ToDo (https://goblin.tools/)

1 - Pesquisar tarefas e  microtarefas para desenvolver uma campanha de marketing (Break down item):

```prompt
"Criar uma caompanha de marketing de guerrilha."
```

Make HQ (https://www.make.com/)

Permite fazer uma automação de pesquisas em chats de inteligência artificial.

Automatizar uma criação de um Post para Blog de Notícias:

1. Crie uma planilha no Google Sheets com o link do conteúdo ou descrição do conteúdo.
2. Pegar os fatos referentes ao conteúdo da planilha:
  1. Connection: My Perplexity connection
  2. Model: Ilma-3.1-7b-instruct
  3. Messages.Content: Pesquisa sobre `Conteúdo (B)`. Traga ponto de crítica, pontos de elogios, diferentes pontos de vista sobre os impactos da notícia. Traga também um resumo que me ajude a entender essa notícia, seja detalhista ao extremo, traga todos os fatos recentes sobre a notícia, detalhadamente, minuciosamente, cite nomes de pessoas, empresas, estatísticas, dados relevantes, traga também um contexto histórico mais amplo, notícias relacionadas do passado que ajudem a contar a história completa. Faça toda a pesquisa necessária para um jornalista produzir um artigo sobre o assunto.
3. Escrever o artigo:
  1. Connection: My Anthropic Claude connection
  2. Model: claude-3-5-sonnet
  3. Max Tokens: 3000
  4. Messages.Role: User
  5. Messages.Content.Type: Text
  6. Messages.Content.Text: Você é o diretor de inteligência artificial de uma importante empresa de educação e mídia no Brasil, liderando a adoção de IA pelas empresas brasileiras. Você está escrevendo suas percepções sobre uma noticia relevante. Sua tarefa é escrever um post de blog em português sobre um artigo de notícias recente. Siga estas instruções cuidadosamente: Primeiro, considere a seguinte notícia:<noticia>`Conteúdo (B)`</noticia> abaixo está o contexto de toda a notícia <contexto>`2.Choices[]:Message.Content`</contexto> no primeiro paragrafo do seu texto você faz um resumo sobre a notícia, despertando curiosidade, implicitamente, no leitor, nada de falar coisas como "descubra como", "leia abaixo", etc.
4. Gerar um resumo do artigo criado.
5. Gerar com o ChatGPT para classificar o artigo em diferentes categorias.
6. Ler a notícia e gerar uma imagem em pixelart
  1. Connection: conexao oficial
  2. Model: DallE 3
  3. Prompt: Gera uma pixelart criativa e bem humorada, e colorida, cores que chamem atenção que ilustr a noticia a seguir: `Conteúdo (B)` escreve "invetormiguel" na imagem e palavras da manchete também em português.
7. Atualiza a planilha do Google.
8. Publica no blog (Webflow/Tactiq)

## Ilustrações

**WIKIPEDIA**  
Disponível em: <https://pt.m.wikipedia.org/wiki/Ficheiro:Markdown-mark.svg>  
Acesso em: 01 jan. 2024.

**GITHUB OCTODEX**  
Disponível em: <https://octodex.github.com/images/minion.png>  
Disponível em: <https://octodex.github.com/images/stormtroopocat.jpg>  
Disponível em: <https://octodex.github.com/images/dojocat.jpg>  
Acesso em: 01 jan. 2024.

## Referências

**EXAME.COM - 3 comandos do ChatGPT para aprender qualquer coisa em qualquer área**  
Disponível em: <https://exame.com/carreira/3-comandos-do-chatgpt-para-aprender-qualquer-coisa-em-qualquer-area/>  
Acesso em: 13 nov. 2024.

**EXAME.COM - 3 comandos do ChatGPT para aprender qualquer coisa em qualquer área**  
Disponível em: <https://exame.com/carreira/3-comandos-do-chatgpt-para-planejar-uma-mudanca-de-carreira-com-seguranca/>  
Acesso em: 13 nov. 2024.

**EXAME.COM - 3 comandos do ChatGPT para desenvolver novas habilidades em tecnologia**  
Disponível em: <https://exame.com/carreira/3-comandos-do-chatgpt-para-desenvolver-novas-habilidades-em-tecnologia/>  
Acesso em: 13 nov. 2024.

**EXAME.COM - 3 comandos do ChatGPT para turbinar sua produtividade no trabalho**  
Disponível em: <https://exame.com/carreira/3-comandos-do-chatgpt-para-turbinar-sua-produtividade-no-trabalho/>  
Acesso em: 13 nov. 2024.


https://lps.exame.com/vdl-pre-mba-ai-aula-ferramentas-202411


