---
title:  "Múltiplas chaves SSH para GitHub"
date:   2024-01-31 09:00:00 +0530
img: "git-github.png"
categories: [Git, GitHub, GitLab]
author: "Suzano Bitencourt"
profile:
  attrs:
    - key: 
      val: 
    - key: 
      val: 
---

Gerenciamento de várias contas do GitHub ou GitLab na mesma máquina surge em algum momento.

<!--more-->

## Conceito

Uma chave SSH é um par de chaves que são usadas para autenticar um usuário em um servidor. A chave pública é usada para criptografar os dados e a chave privada é usada para descriptografar os dados. A chave pública é compartilhada com o servidor e a chave privada é mantida em segredo pelo usuário.

## Parte 1: Geração das chaves SSH

1 - Verificar se temos chaves SSH existentes.
```bash
$ ls -al ~/.ssh
```

2 - Gerar chaves SSH
```bash
$ ssh-keygen -t rsa -C "usuario1@email.com" -b 4096 -f ~/.ssh/usuario1_rsa
$ ssh-keygen -t rsa -C "usuario2@email.com" -b 4096 -f ~/.ssh/usuario2_rsa
$ ssh-keygen -t ed25519 -C "usuario3@email.com" -f ~/.ssh/usuario3_ed25519
```

O `RSA` e `ED25519`, são opções de algoritmos de chave pública que podemos usar para segurança e criptografia. O `ED25519` é, em geral, mais seguro, rápido e eficiente, tornando-se a melhor escolha para a maioria dos casos modernos, especialmente onde desempenho e segurança são essenciais.

## Parte 2: Inclusão da nova chave SSH na conta do GitHub.

1 - Copie a chave pública
```bash
$ pbcopy < ~/.ssh/usuario1_rsa.pub
```

2 - Entre em sua conta pessoal do `GitHub`.
- Vá até `Settings`
- Selecione `SSH and GPG keys` no menu à esquerda.
- Clique em `New SSH key`, dê a ela um `título` adequado, e `cole a chave` na caixa que aparece
- Clique em `Add key` — e pronto!

## Parte 3: Adicionar as chaves ao SSH-Agent

Para usar as chaves, precisamos registrá-las com o `SSH-Agent` em nossa máquina.

1 - Certifique-se de que o `ssh-agent` está em execução usando o comando:
```bash
$ eval "$(ssh-agent -s)"
```

2 - Adicionar uma chave ao `ssh-agent`:
```bash
$ ssh-add ~/.ssh/usuario1_rsa
$ ssh-add ~/.ssh/usuario2_rsa
$ ssh-add ~/.ssh/usuario3_ed25519
```

3 - Para listar as chaves atualmente carregadas no `ssh-agent`, use o comando:
```bash
$ ssh-add -l
```

## Parte 4: Criar o arquivo de configuração de SSH

Adicionando regras de configuração de SSH para hosts diferentes, declarando que arquivo de identidade usar para cada domínio.

1 - Edite o arquivo `~/.ssh/config` se ele existir, ou crie-o, caso contrário:
```bash
$ cd ~/.ssh/
$ touch config
$ code config
```

2 - Escreva as entradas de configuração para as contas relevantes do GitHub:
```bash
# Conta do GitHub (Pessoal)
Host github.com_usuario1
   HostName github.com
   User git
   IdentityFile ~/.ssh/usuario1_rsa
   
# Conta do GitHub (Trabalho)
Host github.com-work_usuario2   
   HostName github.com
   User git
   IdentityFile ~/.ssh/usuario2_rsa
```

**Dica:** Uma notação muito usada para diferenciar as várias contas do Git. "github.com-work_user1", mas você também pode usar a notação "work_user1.github.com".
 Lembre-se de ser consistente com a notação de nome de host que você usa. Isso é relevante ao clonar um repositório ou quando você define remote origin para um repositório local.

## Parte 5: Testando

1 - Para testar a conexão com GitHub:
```bash
$ ssh -T git@github.com
# Hi Usuário! You've successfully authenticated, but GitHub does not provide shell access.
$ ssh -T git@gitlab.com
# Welcome to GitLab, @Usuário!
```

## Parte 6: Clonagem dos repositórios

1 - Durante a clonagem, usarmos como nome de host e que usamos na configuração do SSH.
`git clone git@github.com:personal_account_name/repo_name.git`
```bash
$ git clone git@github.com_usuario1:conta/nome_repo.git
```

## Parte 7: Para repositórios locais existentes

1 - Liste o Git remote do repositório:
```bash
$ git remote -v
```

2 - Verifique se o URL corresponde ao nosso host do GitHub:
```bash
git remote set-url origin git@github.com_usuario1:conta/nome_repo.git
```

3 - Se estiver criando um novo repositório no local:
```bash
$ git remote add origin git@github.com_usuario1:conta/nome_repo.git
```

4 - Faça o push do Commit para o repositório do GitHub:
```bash
git add .
git commit -m "Initial commit"
git push -u origin master
```

## Ilustrações

**GITHUB OCTODEX**  
Disponível em: <https://octodex.github.com/original/>  
Acesso em: 31 jan. 2024.

## Referências

**GITHUB - Múltiplas chaves SSH para GitHub e GitLab**  
Disponível em: <https://gist.github.com/EdnilsonRobert/b4e37785e23a21d0f1eba8974032a77e>  
Acesso em: 31 jan. 2024.

**FREECODECAMP - Como gerenciar diversas contas do GitHub em uma única máquina com as chaves SSH**  
Disponível em: <https://www.freecodecamp.org/portuguese/news/como-gerenciar-diversas-contas-do-github-em-uma-unica-maquina-com-chaves-ssh/>  
Acesso em: 31 jan. 2024.

**YOUTUBE - Configurando acesso SSH em múltiplas contas do Github**  
Disponível em: <https://www.youtube.com/watch?v=n3sldctfF68>  
Acesso em: 31 jan. 2024.