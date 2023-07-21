# Midnight Commander


O **Midnight Commander** é uma ferramenta muito poderosa. Permitindo você pode copiar, mover, renomear e excluir arquivos e diretórios.

<!--more-->

## Conceito

O **GNU Midnight Commander** é um gerenciador de arquivos visual, qualificado como Software Livre. É um aplicativo de modo texto de tela cheia rico em recursos que permite copiar, mover e excluir arquivos e árvores de diretórios inteiras, pesquisar arquivos e executar comandos na subshell.

## Instalação

A instalação pode ser feita utilizando as ferramentas de gerenciamento de pacotes de acordo com a sua distruição linux.

Debian, Ubuntu, e derivados:
```shell
$ sudo apt install mc
```

Arch Linux e derivados:
```shell
$ sudo pacman -S mc
```

Fedora, RHEL e derivados:
```shell
$ sudo dnf install mc
```

OpenSUSE:
```shell
$ sudo zypper install mc
```

## Utilizando

E para iniciar seu uso, basta utilizar o comando abaixo no terminal:
```shell
$ mc
```

Teclas de atalho `Ctrl` e `Shift` significam as mesmas teclas do teclado, Meta é metakey, no PC é `Alt` ou pressionamento único da tecla `Esc`. `Fn` (Onde N > 10) significa `Shift-F(n-10)`, ou seja, `F19` é `Shift-F9`.

- F3	Visualizar arquivo.
- F4	Editar arquivo.
- F13	Exibir arquivo bruto sem extensão específica.
- F14	Criar novo arquivo.
- F19	Ative o último elemento de menu usado.
- F20	Saída tranquila, sem confirmação.
- Inserir	Selecione 'objeto atual' 1
- +	selecione um grupo de arquivos. (expressão regular pode ser usada)
- \	Desmarque um grupo de arquivos. Isso é o oposto da tecla Mais.
- Meta+Enter	Insira 'objeto atual' 1 na linha de comando.
- Meta+.	Mostrar/ocultar arquivos e diretórios ocultos (que começam com '.').
- Meta+,	Altere o modo de visualização dividida do painel para vertical/horizontal.
- Meta+a ou Ctrl+x,p	Insira no caminho da linha de comando do painel ativo.
- Meta+c	Exibe a caixa de diálogo de alteração de diretório para o painel ativo.
- Meta+h	Exibe o histórico de comandos.
- Meta+i	Torne o diretório atual do painel atual também o diretório atual do outro painel. Coloque o outro painel no modo listagem, se necessário. Se o painel atual estiver em painel, o outro painel não ficará em painel.
- Meta+n ou Meta+p	Use essas teclas para navegar pelo histórico de comandos. Meta-p leva você para a última entrada, Meta-n leva você para a próxima.
- Meta+o	Se o arquivo atualmente selecionado for um diretório, carregue esse diretório no outro painel e mova a seleção para o próximo arquivo.
- Meta+g ou Meta+r ou Meta+j	Usado para selecionar o arquivo superior/meio/inferior em um painel, respectivamente
- Meta+t	Alterar visualização do painel ('Completo','Breve','Longo')
- Meta+Shift+?	Achar arquivo.
- Meta+Shift+A ou Ctrl+x, Ctrl+p	Inserir no caminho do painel inativo da linha de comando.
- Meta+Shift+H	Exibe o histórico do diretório.
- Ctrl+\	Exibir lista de favoritos do diretório.
- Ctrl+l	Redefina todas as informações no comandante da meia-noite.
- Ctrl+o	Mostrar/ocultar painel.
- Ctrl+r	Releia o conteúdo do diretório atual.
- Ctrl+s	Pesquisa rápida.
- Ctrl+Espaço	Mostra o tamanho do diretório.
- Ctrl+x,a	Mostrar lista VFS ativa.
- Ctrl+x,c	Chmod (Alterar modo de arquivo) para arquivo ou diretório.
- Ctrl+x,i	Defina o outro modo de exibição do painel para informações.
- Ctrl+x,j	Mostrar trabalhos em segundo plano.
- Ctrl+x,l	Crie hardlink para arquivo ou diretório ativo.
- Ctrl+x,o	Chown (alterar proprietário) para arquivo ou diretório.
- Ctrl+x,q	Defina o outro modo de exibição do painel para visualização rápida.
- Ctrl+x,s	Crie um link simbólico para o arquivo ou diretório ativo.
- Ctrl+x,t	Insira os nomes selecionados na linha de comando.
- Ctrl+x, Ctrl+s	Editar link simbólico.

## Ilustrações

**PIXABAY**  
Disponível em: <https://pixabay.com/vectors/windows-vista-folder-directory-open-149750/>  
Acesso em: 24 jul. 2023.

## Referências

**TECLINUX - Midnight Commander: gerenciador de arquivos poderoso funciona no terminal do Linux**  
Disponível em: <https://teclinux.com/midnight-commander-gerenciador-de-arquivos-poderoso-funciona-no-terminal-do-linux/>  
Acesso em: 24 jul. 2023.

**MIDNIGHT COMMANDER - Oficial**  
Disponível em: <http://midnight-commander.org/>  
Acesso em: 24 jul. 2023.
