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

Este é um tutorial Django "Biblioteca Local" do MDN (<https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/Tutorial_local_library_website>), vamos desenvolver um site para gerenciar o catálogo de uma biblioteca local, cobrindo desde a criação do projeto até a implementação de funcionalidades para o gerenciamento de livros e empréstimos.

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

Este tutorial guiará a criação de um site chamado LocalLibrary. O objetivo do site é oferecer um catálogo online para gerenciar o acervo de uma pequena biblioteca local, permitindo a consulta e administração de livros e empréstimos.

## Parte 1: Esqueleto do Projeto

Para o website `Biblioteca Local`, tanto a pasta principal do site quanto a pasta do projeto terão o nome `locallibrary`, e haverá apenas um aplicativo chamado `catalog`. A estrutura de diretórios no nível hierárquico mais alto ficará assim:

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

4 - O comando `django-admin startproject <nome_do_projeto>` criará uma estrutura com pastas e arquivos:
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
1. **manage.py** - É usado para criar aplicações, trabalhar com bancos de dados, e iniciar o webserver de desenvolvimento.
    - Arquivo de comando que facilita a interação com o projeto Django.
    - Você o usa para comandos como iniciar o servidor (runserver), realizar migrações (migrate), criar usuários (createsuperuser), entre outros.
    - Ele é uma espécie de atalho para o comando django-admin.
2. **locallibrary/** - Diretório interno.
    - Diretório que contém os arquivos principais de configuração do projeto.
    - Tem o mesmo nome do projeto e abriga as configurações, rotas e outros arquivos necessários para que o projeto funcione.
3. **__ __init__ __.py**  - É um arquivo em branco que instrui o Python a tratar esse diretório como um pacote Python.
    - Isso permite que o projeto seja importado como um módulo Python.
4. **settings.py** - Contém todas as definições do website.
    - O arquivo de configurações do projeto.
    - Nele estão as definições de configurações, como banco de dados, middleware, templates, aplicativos instalados, entre outros.
    - É aqui que você ajusta os parâmetros de comportamento do Django, como a configuração de segurança e a conexão com o banco de dados.
5. **urls.py** -Pode conter todo o código para mapeamento de URL, é mais comum delegar apenas o mapeamento para aplicativos específicos.
    - Arquivo responsável por definir as rotas/URLs do projeto.
    - Nele, você mapeia URLs para as respectivas views (funcionalidades).
    - Funciona como uma "tabela de roteamento", que direciona requisições para as funções apropriadas.
6. **asgi.py** - Arquivo de configuração para a interface de servidor ASGI (Asynchronous Server Gateway Interface).
    - ASGI é o padrão para aplicativos Django assíncronos e em tempo real, usado em conjunto com servidores compatíveis com essa interface.
    - Ele é útil quando você precisa de funcionalidades assíncronas, como WebSockets.
7. **wsgi.py** - É usado para ajudar na comunicação entre seu aplicativo Django e o web server. Você pode tratar isso como um boilerplate.
    - Arquivo de configuração para a interface de servidor WSGI (Web Server Gateway Interface).
    - WSGI é a interface padrão usada para servir aplicativos Django de forma síncrona.
    - É o ponto de entrada para servidores web como o Gunicorn ou o Apache servirem o seu aplicativo Django.

### Criando o aplicativo de catálogo

1 - Criando o aplicativo de catálogo:
```bash
python3 manage.py startapp catalog
```
A ferramenta cria uma nova pasta `catalog` e adiciona alguns arquivos para diferentes partes da aplicação.

### Registrando o aplicativo de catálogo

1 - Abra o arquivo de configurações do projeto `locallibrary/locallibrary/settings.py` e encontre a definição para a lista `INSTALLED_APPS`.

É em `INSTALLED_APPS` que definimos uma lista de aplicativos (apps) que estão habilitados para o seu projeto. Esses aplicativos podem ser tanto os nativos do Django quanto aplicativos criados por você ou pacotes de terceiros.
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'catalog.apps.CatalogConfig', # Especifica o objeto de configuração do aplicativo
]
```

A nova linha especifica o objeto de configuração do aplicativo (CatalogConfig) que foi gerado em `/locallibrary/catalog/apps.py` onde a aplicação foi criada.

### Especificando o Banco de Dados

Neste ponto, você também define o banco de dados que será utilizado no projeto. É recomendável usar o mesmo banco de dados tanto no desenvolvimento quanto na produção (sempre que possível), para evitar diferenças sutis de comportamento.

Para mais detalhes sobre outras opções de banco de dados, consulte a documentação do Django em Databases (<https://docs.djangoproject.com/en/2.0/ref/settings/#databases>).

Neste exemplo, usaremos o banco de dados SQLite, já que não esperamos um grande número de acessos simultâneos. Além disso, o SQLite não exige configurações adicionais, o que o torna ideal para uma demonstração. A configuração do banco de dados é feita no arquivo settings.py (mais detalhes estão descritos abaixo).

O arquivo de configurações mais simples possível é para uma configuração de banco de dados único usando SQLite. Isso pode ser configurado usando o seguinte:

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': 'mydatabase',
    }
}
```

Ao se conectar a outros backends de banco de dados, como MySQL, Oracle ou PostgreSQL, parâmetros de conexão adicionais serão necessários. Ver o ENGINE definição abaixo sobre como especificar outros tipos de banco de dados. Este exemplo é para PostgreSQL:

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```

### Outras configurações do projeto

O arquivo `settings.py` também é utilizado para configurar diversas outras definições, como o `TIME_ZONE`.

Configurar o `TIME_ZONE` é importante para manter a consistência de dados. Garantindo que todos os registros de data e hora no banco de dados sejam armazenados de maneira consistente, evitando confusões em aplicações que operam em diferentes fusos horários.

Mais detalhes podem ser encontrados na documentação do Django (<https://docs.djangoproject.com/en/2.0/ref/settings/#std:setting-TIME_ZONE>).

Altere o valor de `TIME_ZONE` para uma string correspondente ao seu fuso horário, como, por exemplo:
```
TIME_ZONE = 'America/Sao_Paulo'
```

### Conectando o mapeador de URL

O website foi criado com um arquivo mapeador de URL `urls.py` na pasta do projeto. Ele desempenha um papel crucial na definição de como os URLs solicitados pelos usuários são correspondidos às respectivas visualizações (views) da aplicação.
Embora você possa usar esse arquivo para gerenciar todos seus mapeamentos de URL, é mais comum fazer os mapeamentos diretamente no aplicativo associado.

Abra `locallibrary/locallibrary/urls.py` e leia o texto que explica alguma formas de usar o mapeador de URL.

```
"""
URL configuration for locallibrary project.

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/5.1/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

Ouma lista Python de funções `path()`. Cada função `path()` associa um padrão s mapeamentos de URL são gerenciados através da variável `urlpatterns` que é de URL para uma view específica, que será exibida quando o padrão for correspondido, ou com outra lista de testes de padrões de URL (no segundo caso, o padrão vem da "URL base" para padrões definidos no módulo target). A lista urlpatterns define inicialmente uma função única que mapeia todas URLs com o padrão admin para o módulo admin.site.urls, que contém as próprias definições de mapeamento de URL da área de administração do aplicativo.

Nota: A rota em path() é uma string que define um padrão de URL para correspondência. Essa string pode incluir um nome de variável (entre tags), e.g. 'catalog/<id>/'. Esse padrão corresponderá a uma URL como /catalog/any_chars/ e passa any_chars para a view como uma string com paramêtros nome id). Nós discutiremos métodos de caminho e padrões de rota ainda mais em tópicos posteriores

Adicione as linhas abaixo no fim do arquivo a fim de adicionar um novo item à lista urlpatterns. Esse novo item inclui um path() que encaminha solicitações com o padrão catalog/ para o módulo catalog.urls (o arquivo com a URL relativa /catalog/urls.py).

```
# Use include() to add paths from the catalog application
from django.conf.urls import include
from django.urls import path

urlpatterns += [
    path('catalog/', include('catalog.urls')),
]
```


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