---
title:  "Ambiente de Desenvolvimento Django"
date:   2024-10-20 09:00:00 +0530
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

## Conceito

O ambiente de desenvolvimento é uma instalação e configuração do Django localmente para permitir o desenvolvimento e teste de aplicativos Django antes de serem implementados em produção. A principal ferramenta fornecida pelo Django é um conjunto de scripts Python que facilita a criação e manipulação de projetos, além de incluir um servidor web de desenvolvimento simples para testar as aplicações localmente no navegador. Isso possibilita aos desenvolvedores realizar ajustes e verificar o funcionamento do app sem precisar de um servidor externo.

Aplicações web Django podem rodar em quase todas as maquinas que suportam a linguagem de programação Python 3. Windows, macOS, Linux/Unix e Solaris são alguns desses SO's.

Existem várias formas de baixar o Django, porém, a melhor forma de conseguir a última versão estável do Django é usando Python Package Repository (PyPi), pelo comando pip.

Django suporta (principalmente) quatro bancos de dados (PostgreSQL, MySQL, Oracle, e SQLite ), contudo, existem bibliotecas community que fornecem níveis variados de suporte para outros populares bancos de dados SQL e NoSQL.

### Instalar em todo o sistema VS Instalar em ambiente virtual Python

Quando Django é instalado no ambiente global do sistema, apenas uma versão do framework pode ser usada, o que pode ser problemático ao trabalhar com projetos que exigem diferentes versões. Para contornar isso, desenvolvedores experientes utilizam ambientes virtuais Python, que são ambientes isolados, permitindo a instalação de versões específicas do Django para diferentes projetos em um único computador. A equipe de desenvolvimento do Django também recomenda essa prática para facilitar a manutenção e o desenvolvimento simultâneo.

## Parte 1: Instalando Python 3

Você deve ter Python instalado em seu sistema operacional para usar Django.

1 - No Linux, você pode confirmar isso executando o seguinte comando no Terminal:
```bash
python3 -V
```

2 - Contudo, o Python Package Index, que você precisará para instalar pacotes para Python 3 (incluindo Django), não está disponível por padrão.
```bash
sudo apt install python3-pip
```

## Parte 2: Ambiente virtual Python

As bibliotecas que nós iremos usar para criar nossos ambientes virtuais são `virtualenv` (permite criar e gerenciar ambientes virtuais isolados no Python) e `virtualenvwrapper` (uma extensão para o virtualenv, que fornece comandos simplificados e utilitários para facilitar o gerenciamento dos ambientes virtuais).

1 - Instalar a ferramenta usando pip3:
```bash
sudo pip3 install virtualenvwrapper
ou
sudo pip3 install virtualenvwrapper --break-system-packages
```

2 - Em seguida, vamos configurar o arquivo de inicialização do shell (normalmente chamado de .bashrc e localizado no diretório home) para definir os caminhos necessários para o desenvolvimento com ambientes virtuais.

```bash
nano ~/.bashrc
```

As linhas a serem adicionadas especificam a localização dos ambientes virtuais, os diretórios onde os projetos serão desenvolvidos e o caminho para o script associado ao pacote instalado. Essas configurações permitem que o terminal reconheça facilmente os ambientes e scripts necessários para o desenvolvimento com Django.
```path
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV_ARGS=' -p /usr/bin/python3 '
export PROJECT_HOME=$HOME/Devel
source /usr/local/bin/virtualenvwrapper.sh
```

3 - Recarregue o arquivo de startup executando o seguinte comando no Terminal:
```bash
source ~/.bashrc
```

## Parte 3: Criando um ambiente virtual

1 - Agora você pode criar um novo ambiente virtual com o comando mkvirtualenv.
```bash
mkvirtualenv meu_ambiente_django
```

## Parte 4: Usando um ambiente virtual

1 - Os comandos abaixo serão os que você usará regularmente:
- deactivate — Encerra o ambiente virtual Python corrente.
- workon — Lista ambientes virtuais disponíveis.
- workon nome_do_ambiente — Ativa o ambiente virtual Python especificado.
- rmvirtualenv nome_do_ambiente — Remove o ambiente especificado.

## Parte 5: Instalando o Django

1 - Após criar um ambiente virtual e usado o comando:
```bash
mkvirtualenv meu_ambiente_django
```

2 - Ativá-lo com o comando:
```bash
workon
```

3 - Use o `pip3` para instalar o Django:
```bash
pip3 install django
```

4 - Para testar a instalação do Django execute o seguinte comando:
```bash
python3 -m django --version
```

## Parte 6: Testando sua instalação

Um teste mais interessante é criar o esqueleto de um projeto e vê-lo funcionando.

1 - Crie uma pasta para seu site e navegue nela:
```bash
mkdir django_teste
cd django_teste
```

2 - Agora você pode criar um novo site chamado `meusite` usando a ferramenta `django-admin` e navegar dentro da pasta onde encontrará o script principal para gerenciar projetos, nomeado manage.py.
```bash
django-admin startproject meusite
cd meusite
ls -al
```

3 - Rodar o web server de desenvolvimento dentro dessa pasta usando o `manage.py` e o comando `runserver`:
```bash
python3 manage.py runserver
```

4 - Uma vez que o servidor está operando, você pode acessar o site colocando a seguinte URL no seu navegador local:http://127.0.0.1:8000/.

## Ilustrações

**DJANGO PROJECT**  
Disponível em: <https://www.djangoproject.com/community/logos/>  
Acesso em: 20 out. 2024.

## Referências

**MDN WEB DOCS - Configurando um ambiente de desenvolvimento Django**  
Disponível em: <https://developer.mozilla.org/pt-BR/docs/Learn/Server-side/Django/development_environment>  
Acesso em: 20 out. 2024.