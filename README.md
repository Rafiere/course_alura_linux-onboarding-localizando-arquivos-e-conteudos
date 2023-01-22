# AULA 01

Nesse curso, aprenderemos a **localizar arquivos** e a trabalhar com alguns conteúdos.

## FILTRANDO O CONTEÚDO

O comando `cat nomeDoArquivo` exibe o conteúdo do arquivo, se esse arquivo for um arquivo de texto.

O comando `grep http services` exibirá todas as ocorrências da string `http` dentro do arquivo `services` do diretório atual.

O comando `grep -i http services` procurará, ignorando o case, a string `http` no arquivo `services`.

O comando `grep -l ricardo *`, procurará, no diretório atual, todos os arquivos que contém a string `ricardo`, e retornará o **nome** desses arquivos.

O comando `grep -L ricardo *`, ao contrário do exemplo anterior, fará a mesma busca e retornará os arquivos que **não possuírem** a string `ricardo`.

## RECURSIVIDADE NO GREP

O comando `grep HTTP -r *` procurará, em todos os arquivos e pastas no diretório atual, de forma recursiva, os arquivos que tiverem a string `HTTP`.

## FORMATANDO A SAÍDA DA TELA

O comando `more nome-do-arquivo` realiza a paginação do arquivo, transformando o arquivo em algo paginado. Nesse comando, o `espaço` rola a tela para baixo, e o `enter` pula de linha em linha. A tecla `B` volta uma página. A tecla `q` sai do paginador.

O comando `less nome-do-arquivo` é uma versão mais atualizada do comando `more`, pois ela permite que a paginação seja realizada com as teclas do cursor, como `seta para baixo`, `seta para cima` e etc.

O comando `tail nome-do-arquivo` exibe as últimas dez linhas de um arquivo. O comando `head nome-do-arquivo` exibe as dez primeiras linhas de um arquivo.

O comando `tail -n 3 nome-do-arquivo` permite que visualizemos as últimas três linhas de um determinado arquivo.

# AULA 02

## PROCURANDO ARQUIVOS NO SISTEMA

O comando `find diretorioInicialDaBusca -name .*conf` buscará todos os arquivos, nesse diretório inicial e de forma recursiva, que terminam com o sufixo `.conf`.

O comando `find /etc --maxdepth 2 -name *.conf` procurará, no diretório `/etc` e em mais um diretório, a partir do `/etc`, de profundidade, todos os arquivos que terminarem com o sufixo `.conf`.

## MAIS RECURSOS DO FIND - AMIN, ATIME, INAME

O comando `find . -amin -5` permite que procuremos, no diretório atual e de forma recursiva, todos os arquivos que foram alterados (?) nos últimos cinco minutos.

O comando `find . -atime -2` realiza a query por **dias**, assim, temos os arquivos que foram alterados (?) nos últimos dois dias.

O comando `find / -size +100M` listará todos os arquivos que possuirem um tamanho maior que `100mb`.

Se não utilizarmos o sinal de `+`, estaremos procurando por arquivos que tenham o **tamanho exato** de `100mb`.

O comando `find /etc -maxdepth 2 -iname *.conf` procurará, no diretório `/etc`, com dois diretórios de profundidade, ou seja, o diretório `/etc` e mais um, os arquivos que terminam com `.conf` e o parâmetro `-iname` ignorará o case das palavras.

O comando `ls -lh` exibe os arquivos formatados para a **leitura humana**.

# AULA 03

## REDIRECIONANDO A SAÍDA PADRÃO PARA UM ARQUIVO

Quando executamos um comando no Linux, como o comando `grep ssh services`, por exemplo, o output padrão desse comando será exibido na tela do usuário.

Para redirecionarmos a saída padrão de um comando para um arquivo, podemos utilizar o comando `grep ssh services > listagem.txt`, dessa forma, a saída padrão do comando `grep` será enviada para um determinado arquivo.

Quando utilizamos o comando `grep ssh services > listagem.txt`, o shell, primeiramente, criará o arquivo `listagem.txt`, assim, se utilizarmos o operador `>`, todo o conteúdo do arquivo `listagem.txt` será perdido, e ele apenas terá o output do comando `grep` dentro dele.

O comando `grep ssh services >> listagem.txt` fará o `append`, ou seja, concatenará o conteúdo já existente do arquivo `listagem.txt` com a saída padrão do comando `grep`.

O operador `|` obtém a saída padrão de um comando e redireciona essa saída para a entrada padrão de outro comando, assim, se utilizarmos o comando `cat /etc/passwd | grep teste`, a saída padrão do comando `cat`, que lista todos os conteúdos de um arquivo de texto, será passada para a entrada padrão do comando `grep`, que procurará, nesse texto, pela string `teste`.

Podemos utilizar o comando `cat /etc/passwd | grep teste > listagem.txt`, estamos redirecionando a saída padrão do comando `grep teste` para o arquivo `listagem.txt`.

## FILTRANDO AS INFORMAÇÕES COM O CUT

O comando `cat syslog | grep systemd | wc` exibirá três informações, que são `numero-de-linhas numero-de-palavras informacao-em-bytes`.

O comando `cat syslog | grep systemd | wc -l` exibirá a quantidade de linhas desse arquivo.

O comando `cut -d`. O `-d` é o **delimitador**, ou seja, ele indica o que está separando uma coluna de outra em um arquivo. Se o arquivo estiver separado por `:` e utilizarmos o comando `cat logs | cut -d ":" -f1`, o conteúdo do arquivo `logs` será dividido em colunas, ou seja, a cada `:`, teremos uma coluna, e o `-f1` indicará que pegaremos apenas a primeira coluna dessa divisão.

O comando `cat logs | cut -d " " -f6-` exibirá todas as colunas da divisão, da sexta coluna até o final do arquivo.

Podemos utilizar a `,` para separarmos as colunas, assim, se utilizarmos o comando `cat logs | cut -d " " -f1-3,6-`, estamos obtendo as colunas de `1` até `3` e, após isso, da coluna `6` até a última coluna que foi feita essa divisão.

# AULA 04

## REGEX COM O GREP

O comando `grep -E` permite que utilizemos uma expressão regular, ou _RegEx_, para realizarmos uma busca em um arquivo por esse padrão.

O comando `grep -E "^computer"` permite que procuremos todas as palavras que comecem com `computer`.

O comando `grep -E "computer$"` exibirá todas as palavras que terminam com `computer`.

O comando `grep -E "^computer$"` permite que exibamos apenas as linhas que possuam a **exatamente** a palavra `computer`.

O comando `echo string` exibe uma string na saída padrão do terminal.

O comando `cat american-english | grep -iE "^computer$"` permite que procuremos, dentro do conteúdo do arquivo `american-english`, a palavra `computer`, ignorando o case.

O comando `grep -E` possui a mesma função do comando `egrep`.

O comando `cat american-english | grep -iE "smartphone|computer"` verificará, dentro do conteúdo do arquivo `american-english`, se existe alguma string que tenha as palavras `smartphone` ou `computer`, sempre ignorando o case, por causa do parâmetro `-i`. O `|` indica o `ou`.

O comando `egrep "^.oot$"` procurará todas as palavras que terminem em `oot` e que o primerio caractere seja qualquer letra. O operador `.` possui o mesmo conceito do `?` no _globbing_

O comando `egrep "^[aeiou]oot..$"` pegará qualquer arquivo que comece com os caracteres `a`, `e`, `i`, `o` ou `u`, que tenha os caracteres `oot` depois desse primeiro caractere e que tenha mais dois caracteres quaisquer após isso.

O `grep` somado com o `regex` consegue localizar quase qualquer conteúdo dentro de um arquivo.

# AULA 05

## EDITORES DE TEXTO NANO E VI

### NANO

O comando `nano nome-do-arquivo` abrirá o editor de textos `Nano` em um determinado arquivo.

### VI

Algumas máquinas não possuem o editor `nano` por padrão. O `vi` é um editor mais famoso e que está na maioria das máquinas.

As novas distribuições do Linux já usam o `vim` ao invés do `vi`, que é uma versão melhorada do `vi`.

Dentro do `vi`, se utilizarmos a tecla `esc`, alternamos entre os modos do editor.

Dentro do modo de comandos, o comando `:q` serve para sairmos do editor `Vim`.

Se apertarmos a tecla `i`, mudamos para o modo de inserção e conseguimos realizar inserções dentro do texto.

O comando `:qw` serve para sairmos do editor e salvarmos o arquivo.

O comando `:q!` serve para sairmos de um arquivo sem salvar.

Ao apertarmos o comando `r`, conseguimos fazer o _replace_ de um caractere por outro.

O comando `:w nome-do-arquivo` serve para salvarmos o arquivo atual com outro nome.

O comando `dd` serve para recortarmos uma linha.

Se utilizarmos o comando `11dd`, a partir do cursor no `vi`, 11 linhas serão deletadas.

O comando `:20` posiciona o cursor na linha 20 do arquivo atual.

O comando `gg` leva até o início do arquivo.

O comando `G` leva até o final do arquivo.

### CÓPIA, COLA E REPLACE

O comando `/ssh` procura pelo caractere `ssh`.

O comando `p` serve para colarmos uma linha depois da linha atual. O comando `P` serve para colarmos uma linha antes do cursor.

O comando `undo` desfaz o último comando.

Para copiarmos uma linha, devemos utilizar o comando `yy`. Para copiarmos 4 linhas a partir do cursor atual, por exemplo, devemos usar o comando `4yy`.

O comando `s/ssh/SSH` serve para substituirmos a primeira string, que é a `ssh`, para o `SSH`. Isso serve apenas para a linha atual. O comando `s/ssh/SSH/g` substitui todas as ocorrências nessa linha, ao invés de apenas a primeira ocorrência da linha.

O comando `%s/domain/teste/g` serve para substituir, **no arquivo inteiro**, todas as palavras `domain` e trocá-las pelo `teste`.
