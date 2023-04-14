# Ansible


O objetivo é apresentar os conceitos básicos de Ansible e como usá-lo para gerenciar a configuração de servidores e aplicações. Comandos básicos, playbooks para automatizar tarefas de configuração de servidores e aplicações, e executar playbooks em diferentes ambientes.

<!--more-->

## Conceitos

### Automação De Infraestrutura

O Ansible é uma ferramenta open source que permitem a automação de TI,  automação cloud, gerenciamento de conformidade e segurança, fluxo automático para integração e deploy contínuo (CI/CD).
Existem outras como Puppet, Saltstack, Chef e CFEngine.

### Como funciona?
O Ansible conecta-se ao que você quer automatizar e implementa programas que executam instruções anteriormente inseridas manualmente. Em seguida, o Ansible executa determinados módulos (sobre SSH padrão) e os remove ao terminar (se aplicável).

## Parte 1: Repositórios

Para os ambientes de RHEL/CentOS 6, é necessário adicionar/instalar o repositório do EPEL(Extra Packages for Enterprise Linux):

```shell
$ sudo yum install epel-release -y
```

## Parte 2: Instalação

Arch Linux
```shell
$ paru -Sy ansible libselinux-python
```

OpenSUSE
```shell
$ sudo zypper refresh
$ sudo zypper install ansible
```

RHEL/Centos 6+
```shell
$ sudo yum install ansible libselinux-python -y
```

Fedora 24+
```shell
$ sudo dnf install ansible libselinux-python -y
```

## Parte 3: Ad-Hoc

Na Informática, uma rede ad hoc é uma ligação temporária entre vários computadores e dispositivos, utilizada para uma finalidade específica. Por exemplo: jogos em rede, partilha de documentos, partilha de impressora, partilha de internet com os utilizadores da rede, etc.

Após a conclusão da instalação, o Ansible já estará pronto para iniciar os primeiros comandos de automação.

Verificando a versão do Ansible
```shell
$ ansible --version
```

Verificar conectividade entre o Ansible Control e o Host:
```shell
$ ansible localhost -m ping
```

{{< admonition tip "Dica:" >}}
Quando nenhum arquivo de inventário é definido, somente o Host ‘localhost’ fica disponível para os comandos Ansible. Para Hosts remotos será necessário definí-los num arquivo de inventário.
{{< /admonition >}}

{{< admonition note "Info:" >}}
O módulo ‘ping’ foi informado através do parâmetro -m e, no caso de sucesso, retorna ‘pong’. A exibição dos resultados dos comandos Ansible é feita no formato json, mas pode ser alterada para yaml a partir da versão 2.5.
{{< /admonition >}}

Coletando informações do host (Gathers facts)
```shell
$ ansible localhost -m setup
```

```
O comando setup coleta as informações dos Hosts e as exibe em forma de variáveis com notação JSON. Estas variáveis podem ser utilizadas em tempo de execução para customizar ou condicionar uma ação.
```

Reiniciando um serviço
```shell
$ ansible localhost -m service -a "name=sshd state=restarted"
```

{{< admonition note "Info:" >}}
O parâmetro `-a` informa os parâmetros do módulo em questão (no exemplo, `-m service`). O uso via Ad-Hoc é com aspas (simples ou duplas), utilizando o caractere ‘=’ para atribuir o valor de cada opção/parâmetro.
{{< /admonition >}}

## Parte 4: Módulos

Verificando Os Módulos Disponíveis:

```shell
$ ansible-doc -l
```

{{< admonition note "Info:" >}}
Após a pesquisa, digitar a tecla `n` (next) para mostrar a próxima entrada ou `p` (preview) para mostrar a entrada anterior. Para sair basta digitar a letra ‘q’.
{{< /admonition >}}

Com o nome do módulo escolhido, é possível ver a documentação do módulo através do comando:

```shell
$ ansible-doc <nome_do_modulo>
$ ansible-doc add_host
```

## Parte 5: Inventário

### Primeiro Arquivo De Inventário

O Ansible foi projetado para trabalhar com múltiplos sistemas (servidores baremetal, máquinas virtuais, Dispositivos de rede etc.) ao mesmo tempo. Ele trabalha selecionando partes desses sistemas listados num arquivo de inventário, que por padrão fica salvo em `/etc/ansible/hosts`. É possível também especificar um arquivo diferente usando o parâmetro `-i <path/nome_inventario>` na linha de comando (Ad-Hoc `$ ansible` ou Playbook `$ ansible-playbook`).

Criaremos um inventário simplificado com vários hosts que apontam para localhost através da variável `ansible_connection=local`. Com isso teremos mais de um host no inventário apontando para um único servidor, simulando vários sistemas.

Copie, cole e salve o conteúdo abaixo no arquivo `/etc/ansible/hosts-teste`:

```
web1.example.com
web2.example.com
db.example.com

[webservers]
web1.example.com
web2.example.com

[dbservers]
db.example.com

[datacenter:children]
webservers
dbservers

[datacenter:vars]
ansible_connection=local
```

Verificando se todos os hosts (all) do inventário estão respondendo:

```shell
$ ansible -i /etc/ansible/hosts-teste -m ping all
```

Verificando o grupo webservers

```shell
$ ansible -i /etc/ansible/hosts-teste -m ping webservers -e 'ansible_python_interpreter=/usr/bin/python3'
```

## Parte 6: Playbook

### Primeira Playbook

Os comandos Ad-Hoc executam apenas um módulo por vez. Para criar uma sequência de tarefas será necessário criar playbooks.

Utilizando um arquivo no formato YAML, todas as tarefas podem ser definidas em sequência e chamadas através de um único comando `ansible-playbook -i <nome_inventario> <nome_playbook>`.

Uma playbook basicamente é composta por `play` e `tasks`.
- play
- tasks

Copie, cole e salve o arquivo abaixo com o nome playbook.yml

```
---
- name: 1 - Criando servidores web
  hosts: webservers

  tasks:
    # task 1
    - name: garantiar que o Apache esteja na última versão
      package: name=httpd state=latest
    # task 2
    - name: conter a linha '127.0.0.1 teste' no arquivo /etc/hosts
      lineinfile: path=/etc/hosts line='127.0.0.1 teste' state=present

- name: 2 - Criando o servidor de banco
  hosts: dbservers

  tasks:
    # task 1
    - name: garantir que o mysqld (MariaDB) está na última versão
      package: name=mariadb-server state=latest
    # task 2
    - name: garantir que o  mysqld (MariaDB) está executando (e habilitá-lo no boot)
      service: name=mariadb state=started enabled=yes
```

## Parte 7: Dicas E Truques

### Criar relação de confiança Hosts Linux

Gerar uma chave de conexão:
```shell
$ ssh-key-gen
```

Copiar o ID para o Hosts alvo:
```shell
$ ssh-copy-id <nome_host>
```

### Outras opções de conexão com os Hosts Alvo

Solicitando a senha do usuário pelo prompt:
```shell
$ ansible-playbook -i /etc/ansible/hosts-test playbook.yml --ask-pass
```

Solicitando senha para escalar privilégios pelo prompt:
```shell
$ ansible-playbook -i /etc/ansible/hosts-test playbook.yml --ask-become-pas
```

### Listagem de Hosts e Tasks das Playbooks

Listando todos os Hosts das Playbooks:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml --list-hosts
```

Listando todas as TASKS das Playbooks:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml --list-tasks
```

### Checagem de sintaxe

Checando a sintaxe YAML:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml --syntax-check
```

### Saltos

Confirmando a execução das TASKs:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml --step
```

Iniciando a Playbook a partir de uma TASK:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml --start-at-task="garantir que o mysqld (MariaDB) está na última versão"
```

Limitando a execução da playbook:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml --limit web1.example.com
```

### Depurando (Debug)

Executando a playbook em Debug modo 1:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml -v
```

Executando a playbook em Debug modo 2:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml -vv
```

Executando a playbook em Debug modo 3:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml -vvv
```

Executando a playbook em Debug de conexão:
```shell
$ sudo ansible-playbook -i /etc/ansible/hosts-test playbook.yml -vvvv
```
## Ilustrações

**PIXABAY**  
Disponível em: <https://pixabay.com/pt/photos/rede-servidor-sistema-2402637/>  
Acesso em: 22 mar. 2023.

## Fontes

**ANSIBLE-BR - Documentação ANSIBLE-BR**  
Disponível em: <http://ansible-br.org>  
Acesso em: 22 mar. 2023

**RED HAT - O que é Ansible?**  
Disponível em: <https://www.redhat.com/pt-br/technologies/management/ansible/what-is-ansible>  
Acesso em: 22 mar. 2023

