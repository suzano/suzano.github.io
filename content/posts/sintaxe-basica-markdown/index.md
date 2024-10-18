---
title:  "Sintaxe Básica do Markdown"
date:   2024-10-18 09:00:00 +0530
img: "markdown.png"
categories: [Linguagem]
author: "Suzano Bitencourt"
profile:
  attrs:
    - key: Name
      val: Stuart
    - key: Likes
      val: Playing guitar
---

Este artigo oferece uma amostra da sintaxe básica do Markdown que pode ser usada em arquivos de conteúdo do Hugo.

<!--more-->

Este artigo é uma tradução vergonhosa da página do [Grav](https://learn.getgrav.org/17/content/markdown).

## Conceito

**Markdown** é a melhor maneira de escrever **HTML**, sem todas as complexidades e fealdades que geralmente o acompanham.

Alguns dos principais benefícios são:

1. Markdown é simples de aprender, com o mínimo de caracteres extras, por isso também é mais rápido escrever conteúdo.
2. Menor chance de erros ao escrever no Markdown.
3. Produz uma saída XHTML válida.
4. Mantém o conteúdo e a exibição visual separados, para que você não estrague a aparência do seu site.
5. Escreva em qualquer editor de texto ou aplicativo Markdown de sua preferência.
6. Markdown é uma alegria de usar!

John Gruber, o autor de Markdown, coloca assim:

> O objetivo primordial do design para a sintaxe de formatação do Markdown é torná-lo o mais legível possível.
> A ideia é que um documento no formato Markdown seja publicável como está, como texto simples,
> sem parecer que foi marcado com tags ou instruções de formatação.
> Embora a sintaxe do Markdown tenha sido influenciada por vários filtros text-to-HTML existentes,
> a maior fonte de inspiração para a sintaxe do Markdown é o formato de e-mail de texto simples.
>
> _John Gruber_

## Parte 1: Cabeçalhos (Headings)

Títulos de `h2` a `h6` são construídos com um `#` para cada nível:

```markdown
## h2 Heading
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading
```

O HTML fica assim:

```html
<h2>Cabeçalho h2</h2>
<h3>Cabeçalho h3</h3>
<h4>Cabeçalho h4</h4>
<h5>Cabeçalho h5</h5>
<h6>Cabeçalho h6</h6>
```

"IDs de Cabeçalho"
Para adicionar um ID de cabeçalho personalizado, coloque o ID personalizado entre chaves na mesma linha do título:

```markdown
### Um ótimo título {#custom-id}
```

The HTML looks like this:

```html
<h3 id="custom-id">Um ótimo título</h3>
```

## Parte 2: Comentários

Os comentários devem ser compatíveis com HTML.

```html
<!--
Este é um comentário
-->
```

O comentário abaixo **NÃO** deve ser visto:

<!--
Este é um comentário
-->

## Parte 3: Réguas Horizontais

O elemento HTML `<hr>` serve para criar uma "quebra temática" entre os elementos em nível de parágrafo.
No Markdown, você pode criar um `<hr>` com qualquer um dos seguintes:

* `___`: três sublinhados consecutivos
* `---`: três traços consecutivos
* `***`: três asteriscos consecutivos

A saída renderizada fica assim:

___
---
***

## Parte 4: Cópia do Corpo

A cópia do corpo escrita normalmente, o texto simples será agrupado com tags `<p></p>` no HTML renderizado.

Portanto, esta cópia do corpo:

```markdown
Lorem ipsum dolor sit amet, graecis denique ei vel, at duo primis mandamus. Et legere ocurreret pri,
animal tacimates complectitur ad cum. Cu eum inermis inimicus efficiendi. Labore officiis his ex,
soluta officiis concludaturque ei qui, vide sensibus vim ad.
```

O HTML fica assim:

```html
<p>Lorem ipsum dolor sit amet, graecis denique ei vel, at duo primis mandamus. Et legere ocurreret pri, animal tacimates complectitur ad cum. Cu eum inermis inimicus efficiendi. Labore officiis his ex, soluta officiis concludaturque ei qui, vide sensibus vim ad.</p>
```

Uma **quebra de linha** pode ser feita com uma linha em branco.

## Parte 5: HTML Embutido

Se você precisa de uma determinada tag HTML (com uma classe), pode simplesmente usar HTML:

```html
Parágrafo em Markdown.

<div class="class">
    Isto é <b>HTML</b>
</div>

Parágrafo em Markdown.
```

## Parte 6: Ênfase

### Negrito (Bold)

Para enfatizar um trecho de texto com um peso de fonte mais pesado.

O trecho de texto a seguir é **renderizado como texto em negrito**.

```markdown
**renderizado como texto em negrito**
__renderizado como texto em negrito__
```

O HTML fica assim:

```html
<strong>renderizado como texto em negrito</strong>
```

### Itálico (Italics)

Para enfatizar um trecho de texto com itálico.

O fragmento de texto a seguir é _renderizado como texto em itálico_.

```markdown
*renderizado como texto em itálico*
_renderizado como texto em itálico_
```

O HTML fica assim:

```html
<em>renderizado como texto em itálico</em>
```

### Tachado (Strikethrough)

Em [[GFM]^(GitHub flavored Markdown)](https://github.github.com/gfm/) você pode fazer tachados.

```markdown
~~Risque este texto.~~
```

A saída renderizada fica assim:

~~Risque este texto.~~

O HTML fica assim:

```html
<del>Risque este texto.</del>
```

### Combinação

Negrito, itálico e tachado podem ser usados em combinação.

```markdown
***negrito e itálico***
~~**riscado e em negrito**~~
~~*riscado e itálico*~~
~~***negrito, itálico e tachado***~~
```

A saída renderizada fica assim:

***negrito e itálico***

~~**riscado e em negrito**~~

~~*riscado e itálico*~~

~~***negrito, itálico e tachado***~~

O HTML fica assim:

```html
<em><strong>negrito e itálico</strong></em>
<del><strong>tachado e negrito</strong></del>
<del><em>tachado e itálico</em></del>
<del><em><strong>negrito, itálico e tachado</strong></em></del>
```

## Parte 7: Citações em bloco

Para citar blocos de conteúdo de outra fonte em seu documento.

Adicione `>` antes de qualquer texto que você deseja citar:

```markdown
> **Fusion Drive** combina um disco rígido com um armazenamento flash (unidade de estado sólido) e o apresenta como um único volume lógico com o espaço de ambas as unidades combinadas.
```

A saída renderizada fica assim:

> **Fusion Drive** combina um disco rígido com um armazenamento flash (unidade de estado sólido) e o apresenta como um único volume lógico com o espaço de ambas as unidades combinadas.

O HTML fica assim:

```html
<blockquote>
   <p>
     <strong>Fusion Drive</strong> combina um disco rígido com um armazenamento flash (unidade de estado sólido) e o apresenta como um único volume lógico com o espaço de ambas as unidades combinadas.
   </p>
</blockquote>
```

Blockquotes também podem ser aninhados:

```markdown
> Donec massa lacus, ultricies a ullamcorper in, fermentum sed augue.
Nunc augue augue, aliquam non hendrerit ac, comodo vel nisi.
>> Sed adipiscing elit vitae augue consectetur a gravida nunc vehicula. Donec autor
odio non est accumsan facilisis. Aliquam id turpis in dolor tincidunt mollis ac eu diam.
```

A saída renderizada fica assim:

> Donec massa lacus, ultricies a ullamcorper in, fermentum sed augue.
Nunc augue augue, aliquam non hendrerit ac, comodo vel nisi.
>> Sed adipiscing elit vitae augue consectetur a gravida nunc vehicula. Donec autor
odio non est accumsan facilisis. Aliquam id turpis in dolor tincidunt mollis ac eu diam.

## Parte 8: Listas

### Não ordenada

Uma lista de itens em que a ordem dos itens não importa explicitamente.

Você pode usar qualquer um dos seguintes símbolos para denotar marcadores para cada item da lista:

```markdown
* marcador válido
- ponto válido
+ marcador válido
```

Por exemplo:

```markdown
* Lorem ipsum dolor sit amet
* Consectetur adipiscing elit
* Integer molestie lorem at massa
* Facilisis em pretium nisl aliquet
* Nulla volutpat aliquam velit
   * Phasellus iaculis neque
   * Purus sodales ultricies
   * Vestibulum laoreet porttitor sem
   * Ac tristique libero volutpat at
* Faucibus porta lacus fringilla vel
* Eneia sit amet erat nunc
* Eget porttitor lorem
```

A saída renderizada fica assim:

* Lorem ipsum dolor sit amet
* Consectetur adipiscing elit
* Integer molestie lorem at massa
* Facilisis em pretium nisl aliquet
* Nulla volutpat aliquam velit
   * Phasellus iaculis neque
   * Purus sodales ultricies
   * Vestibulum laoreet porttitor sem
   * Ac tristique libero volutpat at
* Faucibus porta lacus fringilla vel
* Eneia sit amet erat nunc
* Eget porttitor lorem

O HTML fica assim:

```html
<ul>
   <li>Lorem ipsum dolor sit amet</li>
   <li>Consectetur adipiscing elit</li>
   <li>Integer molestie lorem at massa</li>
   <li>Facilisis em pretium nisl aliquet</li>
   <li>Nulla volutpat aliquam velit
     <ul>
       <li>Phasellus iaculis neque</li>
       <li>Purus sodales ultricies</li>
       <li>Vestibulum laoreet porttitor sem</li>
       <li>Ac tristique libero volutpat at</li>
     </ul>
   </li>
   <li>Faucibus porta lacus fringilla vel</li>
   <li>Eneico sit amet erat nunc</li>
   <li>Eget porttitor lorem</li>
</ul>
```

### Ordenada

Uma lista de itens em que a ordem dos itens importa explicitamente.

```markdown
1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa
4. Facilisis em pretium nisl aliquet
5. Nulla volutpat aliquam velit
6. Faucibus porta lacus fringilla vel
7. Eneia sit amet erat nunc
8. Eget porttitor lorem
```

A saída renderizada fica assim:

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa
4. Facilisis em pretium nisl aliquet
5. Nulla volutpat aliquam velit
6. Faucibus porta lacus fringilla vel
7. Eneia sit amet erat nunc
8. Eget porttitor lorem

O HTML fica assim:

```html
<ol>
   <li>Lorem ipsum dolor sit amet</li>
   <li>Consectetur adipiscing elit</li>
   <li>Integer molestie lorem at massa</li>
   <li>Facilisis em pretium nisl aliquet</li>
   <li>Nulla volutpat aliquam velit</li>
   <li>Faucibus porta lacus fringilla vel</li>
   <li>Eneico sit amet erat nunc</li>
   <li>Eget porttitor lorem</li>
</ol>
```

Se você apenas usar `1.` para cada número, o Markdown numerará automaticamente cada item. Por exemplo:

```markdown
1. Lorem ipsum dolor sit amet
1. Consectetur adipiscing elit
1. Integer molestie lorem at massa
1. Facilisis in pretium nisl aliquet
1. Nulla volutpat aliquam velit
1. Faucibus porta lacus fringilla vel
1. Aenean sit amet erat nunc
1. Eget porttitor lorem
```

A saída renderizada fica assim:

1. Lorem ipsum dolor sit amet
1. Consectetur adipiscing elit
1. Integer molestie lorem at massa
1. Facilisis in pretium nisl aliquet
1. Nulla volutpat aliquam velit
1. Faucibus porta lacus fringilla vel
1. Aenean sit amet erat nunc
1. Eget porttitor lorem

### Listas de Tarefas

As listas de tarefas permitem que você crie uma lista de itens com caixas de seleção. Para criar uma lista de tarefas, adicione hífens (`-`) e colchetes com um espaço (`[ ]`) antes dos itens da lista de tarefas. Para marcar uma caixa de seleção, adicione um x entre os colchetes (`[x]`).

```markdown
- [x] Escreva o comunicado de imprensa
- [ ] Atualizar o site
- [ ] Entre em contato com a mídia
```

A saída renderizada fica assim:

- [x] Escreva o comunicado de imprensa
- [ ] Atualizar o site
- [ ] Entre em contato com a mídia

## Parte 9: Código

### Código embutido

Envolva trechos de código embutidos com <code>`</code>.

```markdown
Neste exemplo, `<section></section>` deve ser agrupado como **código**.
```

A saída renderizada fica assim:

Neste exemplo, `<section></section>` deve ser agrupado como **código**.

O HTML fica assim:

```html
<p>
  Neste exemplo, <code>&lt;section&gt;&lt;/section&gt;</code> deve ser agrupado com <strong>code</strong>.
</p>
```

### Código Indentado

Ou recue várias linhas de código em pelo menos quatro espaços, como em:

```markdown
    // Alguns comentários
    linha 1 do código
    linha 2 do código
    linha 3 do codigo
```

A saída renderizada fica assim:

    // Alguns comentários
    linha 1 do código
    linha 2 do código
    linha 3 do codigo

O HTML fica assim:

```html
<pré>
   <código>
     // Alguns comentários
     linha 1 do código
     linha 2 do código
     linha 3 do codigo
   </código>
</pre>
```

### Bloquear Código Protegido

Use "cercas" <code>```</code> para bloquear em várias linhas de código com um atributo de idioma.

{{< highlight markdown >}}
```markdown
Exemplo de texto aqui...
```
{{< / highlight >}}

O HTML fica assim:

```html
<pre language-html>
   <code>Exemplo de texto aqui...</code>
</pre>
```

### Realce de Sintaxe

[GFM]^(GitHub Flavored Markdown) também suporta realce de sintaxe.

Para ativá-lo, basta adicionar a extensão do arquivo do idioma que deseja usar logo após o primeiro código "cerca",
<code>```js</code> e realce de sintaxe serão aplicados automaticamente no HTML renderizado.

Por exemplo, para aplicar realce de sintaxe ao código JavaScript:

{{< highlight markdown >}}
```js
grunt.initConfig({
  assemble: {
    options: {
      assets: 'docs/assets',
      data: 'src/data/*.{json,yml}',
      helpers: 'src/custom-helpers.js',
      partials: ['src/partials/**/*.{hbs,md}']
    },
    pages: {
      options: {
        layout: 'default.hbs'
      },
      files: {
        './': ['src/templates/pages/index.hbs']
      }
    }
  }
};
```
{{< / highlight >}}

A saída renderizada fica assim:

```js
grunt.initConfig({
  assemble: {
    options: {
      assets: 'docs/assets',
      data: 'src/data/*.{json,yml}',
      helpers: 'src/custom-helpers.js',
      partials: ['src/partials/**/*.{hbs,md}']
    },
    pages: {
      options: {
        layout: 'default.hbs'
      },
      files: {
        './': ['src/templates/pages/index.hbs']
      }
    }
  }
};
```

[Syntax highlighting page](https://gohugo.io/content-management/syntax-highlighting/) em **Hugo** Docs apresenta mais sobre realce de sintaxe, incluindo shortcode de realce.

## Parte 10: Tabelas

As tabelas são criadas adicionando tubos como divisores entre cada célula e adicionando uma linha de traços (também separados por barras) abaixo do cabeçalho. Observe que os tubos não precisam ser alinhados verticalmente.

```markdown
| Opção | Descrição |
| ------ | ----------- |
| data | caminho para arquivos de dados para fornecer os dados que serão passados para os modelos. |
| engine | motor a ser usado para processar modelos. O guidão é o padrão. |
| ext | extensão a ser usada para arquivos dest. |
```

A saída renderizada fica assim:

| Opção | Descrição |
| ------ | ----------- |
| data | caminho para arquivos de dados para fornecer os dados que serão passados para os modelos. |
| engine | motor a ser usado para processar modelos. O guidão é o padrão. |
| ext | extensão a ser usada para arquivos dest. |

O HTML fica assim:

```html
<table>
  <thead>
    <tr>
      <th>Opção</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>data</td>
      <td>caminho para arquivos de dados para fornecer os dados que serão passados para os modelos.</td>
    </tr>
    <tr>
      <td>engine</td>
      <td>motor a ser usado para processar modelos. O guidão é o padrão.</td>
    </tr>
    <tr>
      <td>ext</td>
      <td>extensão a ser usada para arquivos dest.</td>
    </tr>
  </tbody>
</table>
```

"Texto alinhado à direita ou ao centro"
Adicionar dois pontos no lado direito dos traços abaixo de qualquer título alinhará à direita o texto dessa coluna.

Adicionar dois-pontos em ambos os lados dos traços abaixo de qualquer cabeçalho centralizará o texto dessa coluna.

```markdown
| Opção | Descrição |
|:------:| -----------:|
| data   | caminho para arquivos de dados para fornecer os dados que serão passados para os modelos. |
| engine | motor a ser usado para processar modelos. O guidão é o padrão. |
| ext    | extensão a ser usada para arquivos dest. |
```

A saída renderizada fica assim:

| Opção | Descrição |
|:------:| -----------:|
| data   | caminho para arquivos de dados para fornecer os dados que serão passados para os modelos. |
| engine | motor a ser usado para processar modelos. O guidão é o padrão. |
| ext    | extensão a ser usada para arquivos dest. |

## Parte 11: Links {#links}

### Link Básico

```markdown
<https://assemble.io>
<contact@revolunet.com>
[Assemble](https://assemble.io)
```

A saída renderizada se parece com isso (passe o mouse sobre o link, não há dica de ferramenta):

<https://assemble.io>

<contact@revolunet.com>

[Assemble](https://assemble.io)

O HTML fica assim:

```html
<a href="https://assemble.io">https://assemble.io</a>
<a href="mailto:contact@revolunet.com">contact@revolunet.com</a>
<a href="https://assemble.io">Assemble</a>
```

### Adicione um Título

```markdown
[Upstage](https://github.com/upstage/ "Visite o Upstage!")
```

A saída renderizada se parece com isso (passe o mouse sobre o link, deve haver uma dica de ferramenta):

[Upstage](https://github.com/upstage/ "Visite o Upstage!")

O HTML fica assim:

```html
<a href="https://github.com/upstage/" title="Visite o Upstage!">Upstage</a>
```

### Âncoras Nomeadas

As âncoras nomeadas permitem pular para o ponto de ancoragem especificado na mesma página. Por exemplo, cada um destes capítulos:

```markdown
## Índice
   * [Capítulo 1](#capítulo-1)
   * [Capítulo 2](#capítulo-2)
   * [Capítulo 3](#capítulo-3)
```

saltará para estas seções:

```markdown
## Capítulo 1 <a id="chapter-1"></a>
Conteúdo do capítulo um.

## Capítulo 2 <a id="chapter-2"></a>
Conteúdo do capítulo um.

## Capítulo 3 <a id="chapter-3"></a>
Conteúdo do capítulo um.
```

A colocação específica da tag âncora parece ser arbitrária. Eles são colocados em linha aqui, pois parece ser discreto e funciona.

## Parte 12: Notas de Rodapé

As notas de rodapé permitem adicionar notas e referências sem sobrecarregar o corpo do documento. Quando você cria uma nota de rodapé, um número sobrescrito com um link aparece onde você adicionou a referência da nota de rodapé. Os leitores podem clicar no link para pular para o conteúdo da nota de rodapé na parte inferior da página.

Para criar uma referência de nota de rodapé, adicione um cursor e um identificador entre colchetes (`[^1]`). Os identificadores podem ser números ou palavras, mas não podem conter espaços ou tabulações. Os identificadores apenas correlacionam a referência da nota de rodapé com a própria nota de rodapé — na saída, as notas de rodapé são numeradas sequencialmente.

Adicione a nota de rodapé usando outro cursor e número entre colchetes com dois pontos e texto (`[^1]: Minha nota de rodapé.`). Você não precisa colocar notas de rodapé no final do documento. Você pode colocá-los em qualquer lugar, exceto dentro de outros elementos, como listas, citações de bloco e tabelas.

```markdown
Esta é uma nota de rodapé digital[^1].
Esta é uma nota de rodapé com rotulo[^rotulo]

[^1]: Esta é uma nota de rodapé digital
[^label]: Esta é uma nota de rodapé com "label"
```

Esta é uma nota de rodapé digital[^1].

Esta é uma nota de rodapé com rótulo[^rótulo]

[^1]: Esta é uma nota de rodapé digital
[^rótulo]: Esta é uma nota de rodapé com "rótulo"

## Parte 13: Imagens

As imagens têm uma sintaxe semelhante aos links, mas incluem um ponto de exclamação precedente.

```markdown
![Minion](https://octodex.github.com/images/minion.png)
```

![Minion](https://octodex.github.com/images/minion.png)

ou:

```markdown
![Texto alternativo](https://octodex.github.com/images/stormtroopocat.jpg "The Stormtroopocat")
```

![Texto alternativo](https://octodex.github.com/images/stormtroopocat.jpg "The Stormtroopocat")

Assim como os links, as imagens também têm uma sintaxe de estilo de nota de rodapé:

```markdown
![Texto alternativo][id]
```

![Texto alternativo][id]

Com uma referência mais adiante no documento que define o local da URL:

```markdown
[id]: https://octodex.github.com/images/dojocat.jpg  "The Dojocat"
```

[id]: https://octodex.github.com/images/dojocat.jpg  "The Dojocat"


## Ilustrações

**WIKIPEDIA**  
Disponível em: <https://pt.m.wikipedia.org/wiki/Ficheiro:Markdown-mark.svg>  
Acesso em: 23 mar. 2023.

**GITHUB OCTODEX**  
Disponível em: <https://octodex.github.com/images/minion.png>  
Disponível em: <https://octodex.github.com/images/stormtroopocat.jpg>  
Disponível em: <https://octodex.github.com/images/dojocat.jpg>  
Acesso em: 23 mar. 2023.

## Referências

**GRAV - Markdown Syntax**  
Disponível em: <https://learn.getgrav.org/17/content/markdown>  
Acesso em: 23 mar. 2023.