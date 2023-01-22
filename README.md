# Aula 01

## APRESENTAÇÃO E PRINCIPAIS DISTRIBUIÇÕES

É importante aprendermos o Linux porque ele está presente em inúmeros lugares da internet e do mundo da tecnologia em geral.

Esse curso focará no usuário que quer utilizar o Linux para realizar as tarefas do dia a dia.

Existem várias distribuições Linux, porém, a grande maioria das distribuições foram baseadas no Debian, como o Ubuntu, e do Slackware, como o openSUSE.

O CentOS é uma distribuição inspirada no RHEL e que é mantida pela comunidade, normalmente ela é utilizada em servidores. O Fedora é uma versão inspirada no RHEL, porém, ela é mais utilizada em desktops.

O curso será focado na distribuição Ubuntu, que foi derivada do Debian.

## PREPARANDO O SETUP

É muito recomendado instalarmos uma distribuição Linux em um virtualizador, pois, dentro dele, conseguimos instalar vários sistemas operacionais, e nenhum desses sistemas operacionais afetará nada relacionado ao sistema original.

O VirtualBox é o virtualizador que será utilizado durante o curso.

As versões **LTS** do Ubuntu são as versões que possuem um suporte de longo prazo.

## INSTALANDO O LINUX

Após criarmos uma máquina virtual e instalarmos o sistema operacional, que, no curso, será o **Ubuntu Server 20.04.03**.

Nesse curso, instalaremos o Ubuntu em uma máquina virtual e acessaremos essa máquina virtual via **SSH** pela máquina física.

Para isso, devemos acessar as configurações de redes da máquina virtual que foi criada e criar um `Network Adapter` no modo `Bridged Adapter`, dessa forma, será criada uma interface lógica em cima da interface física já existente.

Nessa interface lógica, a máquina virtual obterá o IP da rede local, via DHCP, permitindo que o SSH seja realizado para essa máquina virtual.

Em ambientes de trabalho comuns, sempre acessamos as máquinas externas via SSH.

O **Open SSH Server** é o servidor que permitirá que a conexão remota seja realizada, ou seja, que esse servidor seja acessado remotamente por outras máquinas. Durante a instalação do Ubuntu Server, podemos selecionar para que o Open SSH Server já seja instalado.

# Aula 02

## ACESSANDO O LINUX REMOTAMENTE

Primeiramente, para realizarmos a conexão SSH, devemos saber o IP da máquina virtual, para isso, devemos utilizar o comando `ip addr`. Após sabermos o endereço da máquina que queremos conectar, basta utilizarmos o comando `ssh nome-do-usuario@ip-da-maquina-virtual`.

O `apt` é uma ferramenta para o gerenciamento de pacotes. Sempre que vamos instalar uma aplicação em um servidor, baixamos essa aplicação de um repositório

O comando `sudo apt update` atualiza as referências locais dos pacotes e informa ao sistema se há pacotes mais novos disponíveis ou não.

O comando `sudo` permite a execução de um comando com privilégios administrativos.

O comando `sudo apt install nome-do-pacote` permite o download de um determinado pacote dos repositórios que estão na lista de repositórios válidos de nossa máquina.

## UTILIZANDO UMA INSTÂNCIA DA NUVEM

Podemos criar uma máquina remotamente na EC2 da AWS, por exemplo, e acessá-la através de SSH. A própria AWS fornece as chaves de autenticação, que devem ser inseridas no terminal, e a string de conexão SSH para nos conectarmos à máquina da AWS.

Alguns provedores de máquinas virtuais, como a AWS, fornecem distribuições Linux customizadas.

# AULA 03

## NAVEGANDO NO SISTEMA - PWD E LS

A linha inicial do terminal, que possui algo parecido com `rafael@computador-do-rafael:~/Desktop$`. A notação utilizada nessa linha é `nome-do-usuario@nome-do-host:diretorio-atual privilegio-administrativo-ou-comum(#/$)`

O comando `pwd` exibirá o diretório atual em que estamos. O significado da sigla `pwd` é `print working directory`

O comando `ls` serve para listar o conteúdo do diretório. Se utilizarmos o comando `ls -a` listaremos o conteúdo do diretório, incluindo os arquivos ocultos. O comando `ls -la` serve para listar de forma detalhada todos os arquivos.

O comando `ll` é um **atalho do Ubuntu** para o comando `ls -la`.

O comando `clear` serve para limparmos a tela do terminal.

O comando `ls --help` exibe uma ajuda para esse comando.

O comando `man nome-do-comando` exibirá a página do manual para um determinado comando.

## HIERARQUIA NO FILESYSTEM - FHS

O comando `cd` leva o usuário para a sua `/home` específica.

O comando `cd nome-do-diretorio` leva o usuário para um diretório específico.

A árvore de diretório do Linux é chamada de `FHS`, e ela começa no diretório `/`.

## ATALHOS DE NAVEGAÇÃO

O comando `cd -` serve para acessarmos o último diretório em que estivemos, ou seja, o penúltimo diretório existente.

O `.` significa o diretório atual, e o `..` significa o diretório-pai do diretório atual.

O comando `cd ~` envia o usuário para o diretório `/home` do usuário atual.

# AULA 04

## CRIANDO DIRETÓRIOS

O comando `mkdir nome-do-diretorio` é utilizado para criarmos um diretório.

O comando `mkdir -p dir1/dir2/dir3/dir4` permite a criação de vários diretórios ao mesmo tempo.

O comando `touch nome-do-arquivo` é utilizado para criarmos arquivos vazios.

O comando `touch .nome-do-arquivo` é utilizado para criarmos um arquivo oculto vazio.

## REMOVENDO DIRETÓRIOS E ARQUIVOS

O comando `rmdir nomeDoDiretorio` serve para remover diretórios que estão vazios.

O comando `rm nomeDoArquivo` serve para removermos arquivos.

O comando `rm -r nomeDoDiretorio` serve para apagarmos um diretório e todos os arquivos que estão dentro desse diretório.

O comando `rm -rf nomeDoDiretorio` força a remoção de **TODOS** os arquivos que estão dentro de um determinado diretório.

Para criarmos um diretório com espaço, temos que **escapar** o espaço, por exemplo: `mkdir Área\ de\ Trabalho`, dessa forma, estaremos criando o diretório `Área de Trabalho`.

## COPIANDO ARQUIVOS COM O CP

O comando `cp -r * dir2` permite que realizemos a cópia de todos os arquivos do diretório atual para o diretório `dir2`. O `*` engloba todos os arquivos de um determinado diretório.

## MOVENDO E RENOMEANDO COM O MV

O comando `mv dir1 dir4` serve para movermos o diretório `dir1` para o diretório `dir4` se ele não existir, ou seja, estamos **renomeando** o diretório `dir1` para `dir4`.

Se, nesse exemplo, o diretório `dir4` existisse, o diretório `dir1` seria enviado para dentro do diretório `dir4`.

Caso queiramos mover apenas os arquivos do `dir1`, devemos inserir o comando `mv dir1/* dir4`.

## HISTÓRICO

O comando `history` exibirá o histórico dos comandos que foram executados no bash.

# AULA 05

## GLOBBING

O comando `ls *` exibirá todos os arquivos que não estão ocultos.

O comando `ls arq*` exibirá todos os arquivos que começam com o `arq` e tenham qualquer coisa em sua sequência. Se tivermos um arquivo com o nome `arq`, ele também será exibido, pois o comando `ls arq*` retornará até os arquivos que tiverem o prefixo `arq` e que não tiverem nada na sequência.

Basicamente, o `*` significa tudo ou nada, assim, se tivermos um arquivo chamado `arq`, como no exemplo acima, ele também será listado.

O comando `ls arq1?` exibirá todos os arquivos que tiverem o prefixo `arq1` e que tiverem apenas um caractere após o `1`, ou seja, os arquivos `arq10`, `arq11` e etc, serão listados.

Se utilizarmos o comando `ls arq[1-5]`, serão exibidos os arquivos `arq1`, `arq2`, `arq3`, `arq4` e `arq5`, pois estamos passando o `range` de `1` até `5` para o comando `ls`.

Se quisermos, ao invés de um `range`, passar os arquivos que tenham apenas os números `1` e `5`, basta separarmos esses valores por vírgula, como em `ls arq[1, 5]`, assim, apenas os arquivos `arq1` e `arq5` serão listados.
