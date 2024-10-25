---
title:  "Git e GitHub"
date:   2024-01-13 09:00:00 +0530
img: "git-github.png"
categories: [Git, GitHub]
author: "Suzano Bitencourt"
profile:
  attrs:
    - key: 
      val: 
    - key: 
      val: 
---

Sistema de controle de versão que ajuda a acompanhar as mudanças feitas no código base.

<!--more-->

## Conceito

O **Git** é um sistema de controle de versão distribuído de código aberto e gratuito, projetado para lidar com tudo, desde projetos pequenos a muito grandes, com velocidade e eficiência.

O **GitHub** é um serviço baseado em nuvem que hospeda um sistema de controle de versão (VCS) chamado Git. Ele permite que os desenvolvedores colaborem e façam mudanças em projetos compartilhados enquanto mantêm um registro detalhado do seu progresso.

## Parte 1: Instalação do Git

Se você estiver em uma distribuição baseada no Debian, como o Ubuntu, tente o apt :
```shell
$ sudo apt install git-all
```

Distribuição Arch Linux:

```shell
$ paru -Sy git
```

Para sistemas Windows, entre no site <https://git-scm.com> e faça o download do instalador:

Verifique se o git está instalador:
```shell
$ git --help
```

## Parte 2: Configurar o Git

Abra o terminal no seu computador e digite os seguintes comandos:
```shell
$ git config --global user.email "seu_email@exemplo.com"
$ git config --global user.name "Seu Nome"
```

```shell
$ ls -al ~/.ssh
$ ssh-keygen -t ed25519 -C "seu_email@exemplo.com"
$ cat ~/.ssh/id_ed25519.pub
```

## Parte 3: Conta no GitHub

O **GitHub** é um projeto de gestão baseado em nuvem e uma plataforma de organização que incorpora os recursos de controle de versão do Git. 

Para criar uma conta no GitHub, acesse o site <https://github.com>.

Procure o botão "Se inscrever" ou "Sign Up".

Siga os passos para criar sua conta.

## Parte 4: Iniciar um repositório

No seu computador crie uma pasta para seu projeto:
```shell
$ mkdir pasta-do-projeto
$ cd pasta-do-projeto
$ git init
$ nano arquivo-do-projeto.txt (Escreva algo, salve e feche)
$ git status
$ git add "arquivo-do-projeto.txt"
```

Criar uma versão do código:
```shell
$ git commit -m "Commit inicial"
```

## Parte 5: Enviar Alterações Usando Git Push

O **GitHub** hospeda milhões de repositórios, para criar o seu repositório abra o site do GitHub (https://github.com).

Faça o login da sua conta e clique no botão 'New', escreva um nome para o seu repositório no campo 'Repository name
*' e depois clique em 'Create repository'.

Copie o link ou url referente ao repositório criado.


O repositório "remoto" que é o destino de uma operação de envio através de uma operação "push".
```shell
$ git remote add origin <<link_do repositorio_aqui>>
$ git push --set-upstream origin master
$ git push
```

## Parte 6: Verificar Histórico de Atualizações

Os registros log de referência ou "reflogs", registram quando o cume dos ramos, assim como, quais as outras referências que foram atualizadas no repositório local.

```shell
$ git reflog
```

## Parte 7: Navegar Entre Versões

Para navegar entre versões do seu código:
```shell
$ git reflog (Observe que cada versão possui um ID. Copie o ID da versão desejada)
$ git reset --hard <id-da-versao>
```

## Parte 8: Branches

**Branch** é uma ramificação no git. É um ponto para as alterações feitas nos arquivos do projeto.

Branches disponíveis:
```shell
$ git branch

```

Como criar uma branch:
```shell
$ git branch staging
$ git branch
```

Alternar de uma branch para outra:
```shell
$ git checkout staging
$ git branch
```

## Parte 9: Merge

Após criar várias ramificações da branch principal no decorrer do desenvolvimento do seu projeto, será necessário unificação ou mesclar os branches temporários ni branch principal. Para isso, use o parâmetro 'merge':
```shell
$ git branch (visualizar os branches criados)
$ git checkout master (alternar para o branch principal)
$ git pull (certificar que o branch master está igual o localizado em seu PC)
$ git merge staging (unifica o branch staging ao master)
$ git push (atualiza o repositório remoto)
```

## Parte 10: Passos

1. Garantir que seu repositório local está igual ao repositório remoto, ou seja da branch master ($ git pull)
2. Gerar uma nova branch a partir da branch master para adicionar novas funcionalidades e testa-las  ($ git checkout -b sistema-de-login master)
3. Checar se você está trabalhando na nova branch e adionar novas funcionalidades ($ git branch)
4. Depois de finalizar o trabalho na branch temporária ($ git add . && git commit -m "Descrição" && git push --set-upstream origin sistema-de-login)
5. Navegue até a branch master ($ git checkout master && git branch)
6. Certifique-se que seu repositório local está igual ao repositório remoto, ou seja da branch master ($ git pull)
7. Unir(merge) o código da branch temporária com a branch master ($ git merge sistema-de-login master)
8. Faça envio para dar alterações para o repositório remoto ($ git push)


## Parte 11: Git Ignore

O *.gitignore* é um arquivo de texto oculto que geralmente fica na raiz do repositório, utilizado para descrever ao Git as pastas e arquivos que devem ser ignorados pelo push.

```
$ touch .gitignore
$ nano .gitignore (Escreva os nomes das pastas e arquivos que serão ignorados)
$ git push
```

## Parte 12: Considerações Finais

```
# Inicializa um novo repositório
$ git init

# Adiciona os arquivos atauais ao próximo commit
$ git add .

# Verificar o status atual dos repositórios git
$ git status

# Cria um novo commit com uma mensagem
$ git commit -m "mensagem do commit"

# Envia as atualizações para a nuvem na branch atualmente ativa
$ git push

# Permite listar e ver qual branch está ativa atualmente
$ git branch

# Permite mudar para uma nova branch
$ git checkout nome-da-branch

# Permite mudar e criar uma nova branch com base em outra
$ git checkout -b "nome-da-branch-de-origem" "nome-da-nova-branch" 

# Permite fazer o merge da branch ativa atualmente com outra branch
$ git merge "branch-a-receber-merge"

# Atualiza a branch ataualmente ativa
$ git pull                                                          # 
```

## Ilustrações

**GITHUB OCTODEX**  
Disponível em: <https://octodex.github.com/original/>  
Acesso em: 13 jan. 2024.

## Referências

**GIT --distributed-even-if-your-workflow-isnt**  
Disponível em: <https://git-scm.com>  
Acesso em: 13 jan. 2024.

**GITHUB**  
Disponível em: <https://github.com>  
Acesso em: 13 jan. 2024.

**HOSTINGER - Tutoriais**  
Disponível em: <https://www.hostinger.com.br/tutoriais/o-que-github>  
Acesso em: 13 jan. 2024.

**YOUTUBE - Curso de Git e Github COMPLETO 2021 [Iniciantes] + Desafios + Muita Prática**  
Disponível em: <https://www.youtube.com/watch?v=kB5e-gTAl_s>  
Acesso em: 13 jan. 2024.