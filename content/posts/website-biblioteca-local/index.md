---
title:  "Website da Biblioteca Local"
date:   2024-10-21 09:00:00 +0530
img: "django.png"
categories: [Programação, Linguagem, Django]
author: "Suzano Bitencourt"
profile:
  attrs:
    - key: 
      val: 
    - key: 
      val: 
---

Este artigo faz parte dos meus estudos de programação de site do lado do servidor e como usar os frameworks web Django.

<!--more-->

A programação do lado do servidor é essencial para sites que precisam exibir dados dinamicamente, como Amazon e Facebook, pois permite atualizar informações em modelos estáticos de HTML, CSS e JavaScript sem criar inúmeras páginas estáticas.

## Visão geral

Este é um tutorial Django "Biblioteca Local" do MDN (<https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Tutorial_local_library_website>), no qual desenvolveremos um website que pode ser usado para gerenciar um catálogo para uma biblioteca local.

Será estudado nesse tutorial:
- Usar as ferramentas do Django para criar a estrutura de um website e aplicação.
- Começar e parar o servidor de desenvolvimento.
- Criar models para representar os dados da aplicação.
- Usar o admin do Django para popular os dados do seu site.
- Criar views para recuperar dados específicos em resposta a diferentes requisições, e templates para renderizar os dados como HTML para serem exibidos no navegador.
- Criar mappers para associar diferentes padrões de URL com asviews específicas.
- Adicionar autorização de usuário e sessões para controlar o comportamento e acesso do site.
- Trabalhar com formulários.
- Criar teste de código para a sua aplicação.
- Usar a segurança do Django de forma eficaz.
- Implantar sua aplicação para produção.

## Website da Biblioteca Local - LocalLibrary

Esse tutoria, guiará a criação de um site chamado **LocalLibrary**. A proposta do site é fornecer um catálogo online para uma pequena biblioteca local.

## Parte 1: Esqueleto do Projeto

Para o website `Biblioteca Local` a pasta do website e a pasta do projeto terão, ambas, o nome `locallibrary`, e terá apenas um aplicativo chamado `catalog`. O nível hierárquico mais alto da estrutura de pastas ficará assim:

```
┬ locallibrary/ # Pasta do website
├ manage.py     # Script para executara as ferramentas do Django
├ locallibrary/ # Pasta do projeto
└ catalog/      # Pasta do aplicativo
```

### Criando o projeto

1 - Crie um diretório que deseja colocar seus aplicativos Django.
```bash
mkdir website-biblioteca-local
cd website-biblioteca-local
```

2 - Tenha certeza que está em seu ambiente virtual e navegue até o diretório que deseja colocar seus aplicativos Django.
```bash
mkvirtualenv django_projects
pip3 install django
python3 -m django --version
```

3 - Crie um novo projeto usando o comando `django-admin startproject`:
```bash
django-admin startproject locallibrary
cd locallibrary
```

4 - O comando `django-admin` criará uma estrutura com pastas e arquivos:
```
┬ locallibrary/
├ manage.py
└ locallibrary/
  ├ __init__.py
  ├ settings.py
  ├ urls.py
  └ wsgi.py
```

A sub-pasta do projeto:
- **__ __init__ __.py**  - É um arquivo em branco que instrui o Python a tratar esse diretório como um pacote Python.
- **settings.py** - Contém todas as definições do website. É onde nós registramos qualquer aplicação que criarmos, a localização de nossos arquivos estáticos, configurações de banco de dados etc.
- **urls.py** - Define os mapeamentos de URL para visualização do site. Mesmo que esse arquivo possa conter todo o código para mapeamento de URL, é mais comum delegar apenas o mapeamento para aplicativos específicos, como será visto mais adiante.
- **wsgi.py** - É usado para ajudar na comunicação entre seu aplicativo Django e o web server. Você pode tratar isso como um boilerplate.
- **manage.py** - É usado para criar aplicações, trabalhar com bancos de dados, e iniciar o webserver de desenvolvimento.

### Criando o aplicativo de catálogo

1 - Criando o aplicativo de catálogo:
```bash
python3 manage.py startapp catalog
```
A ferramenta cria uma nova pasta `catalog` e adiciona alguns arquivos para diferentes partes da aplicação.

### Registrando o aplicativo de catálogo

1 - Abra o arquivo de configurações do projeto `locallibrary/locallibrary/settings.py` e encontre a definição para a lista `INSTALLED_APPS`. 
```

```

### Especificando o Banco de Dados

### Outras configurações do projeto

### Conectando o mapeador de URL


### Testando o framework do site


## Parte 9: Testando o website
## Parte 6: Outras configurações do projeto
## Parte 6: Outras configurações do projeto



## Ilustrações

**DJANGO PROJECT**  
Disponível em: <https://www.djangoproject.com/community/logos/>  
Acesso em: 20 out. 2024.

## Referências

**MDN WEB DOCS - Tutorial Django: Website da Biblioteca Local**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Tutorial_local_library_website>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Django Tutorial Parte 2: Criando o "esqueleto" de um site**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/skeleton_website>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Tutorial Django Parte 3: Usando models**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Models>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Tutorial Django Parte 4: Django admin site**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Admin_site>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Django Tutorial Parte 5: Criando nossa home page**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Home_page>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Tutorial Django Parte 6: Lista genérica e detail views**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Generic_views>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Tutorial Django Parte 7: Sessões**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Sessions>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Tutorial Django Parte 8: Autenticação de usuário e permissões**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Authentication>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Tutorial Django Parte 9: Trabalhando com formulários**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Forms>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Tutorial Django Parte 10: Testando uma aplicação web Django**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Testing>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Tutorial Django Parte 11: Hospedando Django para produção**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Deployment>  
Acesso em: 21 out. 2024.

**MDN WEB DOCS - Segurança de aplicações web Django**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/web_application_security>  
Acesso em: 21 out. 2024.

**MATEMÁTICA.PT - Tabela ASCII**  
Disponível em: <https://www.matematica.pt/util/resumos/tabela-ascii.php>  
Acesso em: 21 out. 2024.