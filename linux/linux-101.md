# Principais Comandos

### pipe
Um pipe (representado pelo caractere "|") é um mecanismo que permite conectar a saída de um comando à entrada de outro, criando uma sequência de comandos onde a saída de um se torna a entrada do próximo. Isso permite que você crie comandos complexos combinando vários comandos menores, de forma eficiente e organizada.

Exemplos:

* ls -l | less: Lista os arquivos do diretório atual e exibe a saída paginada no less. 
* cat file.txt | grep "texto": Lê o conteúdo de file.txt e filtra as linhas que contêm a palavra "texto". 
* ps aux | grep "httpd" | wc -l: Lista todos os processos em execução, filtra aqueles que contêm "httpd" e conta o número de linhas resultantes, mostrando quantos processos httpd estão ativos.

# gunzip
Descompactar arquivos em formato .gz

# tar
Descompactar arquivos em formato .tar

### echo
Saia qualquer texto que fornecer

### ps
Veja os processos atualmente rodando na máquina, no usuário atual.
* O argumento ```aux``` utilizado em conjunto, fornece todos os processos atualmente rodando na máquina, de todos os usuários.
* O comando ```top``` serve para mostrar, em tempo real, os processos de todos os usuários.

### whoami
Descubra qual usuário está logado

### ls
Listar todos os arquivos de uma pasta
* Pode se usar o argumento ```-a``` para listar conteúdos ocultos em uma pasta, com o início em ```.```
* O argumento ```--help``` lhe mostra todas as opções possíveis deste comando.
* O argumento ```-l``` retorna as permissões de um determinado conteúdo. Ex: ```ls -lh``` (lembrando que utilizar o ```h``` retorna informações "mais humanas".

### cd
Mudar de diretório

### cat
Faz a leitura de conteúdos de um arquivo.
Pro tip: você pode usar cat para exibir o conteúdo de um arquivo dentro de diretórios sem precisar navegar até ele usando cat e o nome do diretório. Por exemplo, ```cat /home/ubuntu/Documents/todo.txt```

### pwd
Basicamente serve para descobrir qual diretório estamos trabalhando, retornando o caminho completo

### su
Comando para trocar entre os usuários dentro de um sistema Linux. Ex: ```su user1```.
Aparecerá a requisição da senha deste usuário. Após colocar, você estará neste usuário.

### find
Comando muito útil para não precisar gastar tempo buscando um arquivo por cada diretório.
Se por exemplo quero buscar um arquivo .txt chamado senhas:
```find -name senhas.txt``` ou ```find -name *.txt``` <= para buscar qualquer .txt no diretório atualmente conectado

### grep
Permite pesquisar o conteúdo dos arquivos em busca de valores específicos que procuramos.
Usando um comando como cat não vai servir muito bem aqui. Digamos, por exemplo, se quiséssemos pesquisar este arquivo de log para ver as coisas que um determinado usuário/endereço IP visitou? Analisar todas as entradas não é tão eficiente, considerando que queremos encontrar um valor específico.

Podemos usar grep para pesquisar todo o conteúdo deste arquivo por quaisquer entradas do valor que procuramos. Indo com o exemplo do log de acesso de um servidor web, queremos ver tudo o que o endereço IP "45.155.205.181" visitou.

### wc
Abreviação de word count. Serve para analisar a contagem de elementos presente de um log, no diretório acessado, por exemplo.
Pro tip: -l mostrará a quantidade de linhas específicas do arquivo
```wc -l access.log```

### man
Abreviação de manual, retorna o manual do comando que desejamos entender. Ex: ```man nome_do_comando```

### touch
Comando para criar um arquivo no diretório atual. Ex: ```touch nome_do_arquivo```

### mkdir
Cria uma pasta no diretório atual. Ex: ```mkdir nome_da_pasta```

### cp 
Copia uma pasta ou um arquivo. Esse comando copia um arquivo, no diretório, com o nome que se é especificado. Ex: ```cp arquivo1 arquivo2```

### mv
Move uma pasta ou um arquivo

### rm	
Remove uma pasta ou um arquivo. Para remover um arquivo basta digitar ```rm nome_do_arquivo``` e para remover uma pasta, deve-se acrescentar o argumento -R, ou seja, ```rm -R nome_da_pasta```

### file 
Determina qual o tipo do arquivo selecionado

### nano
Edita um arquivo de texto

# Operadores Linux

### Operador "&"
Este operador nos permite executar comandos em segundo plano. Por exemplo, digamos que queremos copiar um arquivo grande. Isso obviamente levará bastante tempo e nos deixará impossibilitados de fazer qualquer outra coisa até que o arquivo seja copiado com sucesso.
O operador de shell "&" nos permite executar um comando e executá-lo em segundo plano, permitindo-nos fazer outras coisas!

### Operador "&&"
Este operador de shell é um pouco enganoso no sentido de quão familiar é com seu parceiro "&". Ao contrário do operador "&", podemos usar "&&" para criar uma lista de comandos a serem executados, por exemplo, comando1 && comando2. No entanto, vale a pena notar que comando2 só será executado se comando1 for bem-sucedido.

### Operador ">"
Este operador é o que conhecemos como redirecionador de saída. O que isso significa essencialmente é que pegamos a saída de um comando que executamos e a enviamos para outro lugar.

Um ótimo exemplo disso é redirecionar a saída do comando echo. É claro que executar algo como echo howdy retornará "howdy" para o nosso terminal — isso não é muito útil. O que podemos fazer em vez disso é redirecionar "howdy" para algo como um novo arquivo!

Digamos que queremos criar um arquivo chamado "welcome" com a mensagem "hey". Podemos executar echo hey > welcome onde queremos que o arquivo seja criado com o conteúdo "hey" assim:
```echo hey > welcome```

```
cat welcome
hey
```

### Operador ">>"
Este operador também é um redirecionador de saída, como o operador anterior (>) que discutimos. No entanto, o que o diferencia é que, em vez de sobrescrever qualquer conteúdo dentro de um arquivo, por exemplo, ele apenas coloca a saída no final.

Continuando com nosso exemplo anterior, onde temos o arquivo "welcome" que contém o conteúdo "hey". Se usássemos echo para adicionar "hello" ao arquivo usando o operador >, o arquivo agora teria apenas "hello" e não "hey".

O operador >> permite anexar a saída ao final do arquivo — em vez de substituir o conteúdo como:

```echo hello >> welcome```

```
cat welcome
hey
hello
```

#### Pergunta & Resposta
Se eu quero rodar um comando em segundo plano, qual operador devo usar?

```&```

Se eu quisesse substituir o conteúdo de um arquivo chamado "passwords" pela palavra "password123", qual seria meu comando?

```echo password123 > passwords```

Agora, se eu quisesse adicionar "tryhackme" a este arquivo chamado "passwords", mas também manter "passwords123", qual seria meu comando?

```echo tryhackme >> passwords```

# SSH (Secure Shell)
Secure Shell (SSH) refere-se a um protocolo de rede criptográfico usado na comunicação segura entre dispositivos. O SSH criptografa dados usando algoritmos criptográficos, como o Advanced Encryption System (AES), e é frequentemente usado para fazer login remotamente em um computador ou servidor. Usando criptografia, qualquer entrada que enviamos em um formato legível por humanos é criptografada para trafegar pela rede — onde é descriptografada ao chegar à máquina remota.

Para acessar um servidor, por exemplo, em um terminal, utilize o comando ```ssh usuario@IP``` Se estiver correto, o terminal irá requisitar a senha deste usuário.

## Autenticação ao servidor 
<img width="696" height="202" alt="image" src="https://github.com/user-attachments/assets/b7d316b9-a9a8-40cd-a91c-bd8b84329585" />

Na interação acima, o cliente SSH confirma se reconhecemos a "fingerprint" da chave pública do servidor. ED25519 é o algoritmo de chave pública usado para geração e verificação de assinatura digital neste exemplo. Nosso cliente SSH não reconheceu essa chave e está nos pedindo para confirmar se queremos continuar com a conexão. Este aviso ocorre porque um ataque do tipo "man-in-the-middle" é provável; um servidor malicioso pode ter interceptado a conexão e respondido, fingindo ser o servidor alvo.

Neste caso, o usuário deve autenticar o servidor, ou seja, confirmar a identidade do servidor verificando a assinatura da chave pública. Assim que você responder "yes", o cliente SSH registrará essa assinatura da chave pública para este host. No futuro, ele se conectará silenciosamente, a menos que este host responda com uma chave pública diferente.

## Autenticando o Cliente
Agora que confirmamos que estamos "falando" com o servidor correto, precisamos nos identificar e nos autenticar. Em muitos casos, os usuários SSH são autenticados usando nomes de usuário e senhas, como se estivessem logando em uma máquina física. No entanto, considerando os problemas inerentes às senhas, isso não se enquadra nas melhores práticas de segurança.

Em algum momento, certamente encontraremos uma máquina com SSH configurado com autenticação por chave. Essa autenticação usa chaves públicas e privadas para provar que o cliente é um usuário válido e autorizado no servidor. Por padrão, as chaves SSH são ```chaves RSA```. Você pode escolher qual algoritmo gerar e adicionar uma senha para criptografar a chave SSH.

```ssh-keygen``` é o programa normalmente usado para gerar pares de chaves. Ele suporta vários algoritmos.

### Nomes comuns de chaves criptografadas
* DSA (Algoritmo de Assinatura Digital): é um algoritmo de criptografia de chave pública projetado especificamente para assinaturas digitais.
* ECDSA (Algoritmo de Assinatura Digital de Curva Elíptica): é uma variante do DSA que utiliza criptografia de curva elíptica para fornecer tamanhos de chave menores para segurança equivalente.
* ECDSA-SK (ECDSA com Chave de Segurança): é uma extensão do ECDSA. Ele incorpora chaves de segurança baseadas em hardware para proteção aprimorada de chaves privadas.
* ED25519: é um sistema de assinatura de chave pública que utiliza o EdDSA (Algoritmo de Assinatura Digital de Curva de Edwards) com o Curve25519.
* ED25519-SK (Ed25519 com Chave de Segurança): é uma variante do Ed25519. Semelhante ao ECDSA-SK, ele utiliza uma chave de segurança baseada em hardware para proteção aprimorada de chaves privadas.

<img width="543" height="366" alt="image" src="https://github.com/user-attachments/assets/0a1fe256-3c1f-4735-9c47-5d3a6ff8279a" />

## Chaves Privadas SSH
Devemos tratar chaves privadas SSH como senhas. Nunca podemos compartilhar em hipótese alguma; elas são chamadas de chaves privadas por um motivo. Alguém com sua chave privada pode efetuar login em servidores que a aceitam, ou seja, incluí-la entre as chaves autorizadas, a menos que a chave esteja criptografada com uma senha.

É muito importante mencionar que a senha usada para descriptografar a chave privada não o identifica para o servidor; ela apenas descriptografa a chave privada SSH. A senha nunca é transmitida e nunca sai do seu sistema.

Usando ferramentas como o John the Ripper, você pode atacar uma chave SSH criptografada para tentar encontrar a senha, destacando a importância de usar uma senha complexa e manter sua chave privada privada.

Ao gerar uma chave SSH para efetuar login em uma máquina remota, você deve gerar as chaves na sua máquina e, em seguida, copiar a chave pública, pois isso significa que a chave privada nunca existirá na máquina de destino usando ```ssh-copy-id```. No entanto, isso não importa tanto para chaves temporárias geradas para acessar caixas CTF.

As permissões devem ser configuradas corretamente para usar uma chave SSH privada; caso contrário, seu cliente SSH ignorará o arquivo e emitirá um aviso. Somente o proprietário deve poder ler ou gravar na chave privada (600 ou mais restrita). ```ssh -i privateKeyFileName user@host``` é como você especifica uma chave para o cliente OpenSSH Linux padrão.

### Chaves Confiáveis pelo Host Remoto
A pasta ```~/.ssh``` é o local padrão para armazenar essas chaves para o OpenSSH. O arquivo authorized_keys (observe a ortografia em inglês americano) neste diretório contém chaves públicas que têm acesso permitido ao servidor se a autenticação de chave estiver habilitada. Por padrão, em muitas distribuições Linux, a autenticação de chave é habilitada, pois é mais segura do que usar uma senha para autenticação. Somente a autenticação de chave deve ser aceita se você quiser permitir acesso SSH para o usuário root.

##Usando Chaves SSH para Obter um "Shell Melhor"
Durante CTFs, testes de penetração e exercícios de red teaming, chaves SSH são uma excelente maneira de "atualizar" um shell reverso, desde que o usuário tenha o login habilitado. Observe que ```www-data``` geralmente não permite isso, mas usuários comuns e root podem funcionar. **```Deixar uma chave SSH no arquivo authorized_keys em uma máquina pode ser uma backdoor útil```**, e você não precisa lidar com nenhum dos problemas de shells reversos não estabilizados, como Control-C ou falta de conclusão de tabulação.

# Diretórios Comuns

### /etc
Este diretório raiz é um dos diretórios raiz mais importantes do seu sistema. A pasta etc (abreviação de etcetera) é um local comum para armazenar arquivos de sistema usados pelo seu sistema operacional.

### /var
O diretório "/var", abreviação de "variable data" (dados variáveis), é uma das principais pastas raiz encontradas em uma instalação Linux. Esta pasta armazena dados que são frequentemente acessados ou gravados por serviços ou aplicativos em execução no sistema. Por exemplo, arquivos de log de serviços e aplicativos em execução são gravados aqui (/var/log), ou outros dados que não estão necessariamente associados a um usuário específico (por exemplo, bancos de dados e similares).

### /root
Ao contrário do diretório /home, a pasta /root é, na verdade, o diretório inicial do usuário "root" do sistema. Não há nada mais a ser dito sobre essa pasta além da compreensão de que este é o diretório inicial do usuário "root". Vale a pena mencionar, pois a presunção lógica é que esse usuário teria seus dados em um diretório como "/home/root" por padrão.

### /tmp
Este é um diretório raiz exclusivo encontrado em uma instalação do Linux. Abreviação de "temporário", o diretório /tmp é volátil e é usado para armazenar dados que precisam ser acessados apenas uma ou duas vezes. Semelhante à memória do seu computador, assim que o computador é reiniciado, o conteúdo desta pasta é limpo.

O que é útil para nós em testes de penetração é que qualquer usuário pode escrever nesta pasta por padrão. Ou seja, quando temos acesso a uma máquina, ela serve como um bom local para armazenar coisas como nossos scripts de enumeração.

# Edição de texto com nano e VIM

### nano
Para criar ou editar um arquivo usando o nano, simplesmente usamos ```nano filename``` — substituindo "filename" pelo nome do arquivo que você deseja editar.
Assim que pressionarmos Enter para executar o comando, o nano será iniciado! Podemos simplesmente começar a inserir ou modificar nosso texto. Você pode navegar por cada linha usando as teclas de seta para cima e para baixo ou iniciar uma nova linha usando a tecla Enter do seu teclado.
O Nano possui alguns recursos fáceis de lembrar e abrangem os aspectos mais gerais que você espera de um editor de texto, incluindo:
* Buscar texto
* Copiar e Colar
* Ir para um número de linha
* Descobrir em qual número de linha você está

Você pode usar esses recursos do Nano pressionando a tecla "Ctrl" (representada por um ^ no Linux) e a letra correspondente. Por exemplo, para sair, pressionaríamos "Ctrl" e "X" para sair do Nano.

### VIM
Alguns dos benefícios do VIM, embora levem muito mais tempo para se familiarizar, incluem:

* Personalizável - você pode modificar os atalhos de teclado conforme sua preferência
* Destaque de Sintaxe - útil se você estiver escrevendo ou mantendo código, tornando-o uma escolha popular para desenvolvedores de software
* O VIM funciona em todos os terminais onde o nano não esteja instalado

# Download de Arquivos (wget)
Um recurso fundamental da computação é a capacidade de transferir arquivos. Por exemplo, você pode querer baixar um programa, um script ou até mesmo uma imagem. Felizmente para nós, existem várias maneiras de recuperar esses arquivos.

Vamos abordar o uso do wget. Este comando nos permite baixar arquivos da web via HTTP — como se você estivesse acessando o arquivo em seu navegador. Precisamos apenas fornecer o endereço do recurso que desejamos baixar. Por exemplo, se eu quisesse baixar um arquivo chamado "myfile.txt" para minha máquina, supondo que eu soubesse o endereço da web, seria algo assim:

```wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt```

# Transferindo Arquivos do Seu Host - SCP (SSH)

Cópia Segura, ou SCP, é um meio de copiar arquivos com segurança. Ao contrário do comando cp comum, este comando permite transferir arquivos entre dois computadores usando o protocolo SSH para fornecer autenticação e criptografia.
Trabalhando com um modelo de ORIGEM e DESTINO, o SCP permite:
* Copiar arquivos e diretórios do seu sistema atual para um sistema remoto
* Copiar arquivos e diretórios de um sistema remoto para o seu sistema atual

Desde que saibamos os nomes de usuário e senhas de um usuário no seu sistema atual e de um usuário no sistema remoto. Por exemplo:
* Endereço IP do sistema remoto: 192.168.1.30
* Usuário no sistema remoto: Ubuntu
* Nome do arquivo no sistema local: important.txt
* Nome que desejamos usar para armazenar o arquivo no sistema remoto: registered.txt

Com essas informações, vamos criar nosso comando scp (lembrando que o formato do SCP é apenas ORIGEM e DESTINO)

```scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt```

E agora vamos reverter isso e definir a sintaxe para usar o SCP para copiar um arquivo de um computador remoto no qual não estamos conectados.
* Endereço IP do sistema remoto: 192.168.1.30
* Usuário no sistema remoto: Ubuntu
* Nome do arquivo no sistema remoto: documents.txt
* Nome que desejamos usar para armazenar o arquivo no nosso sistema: notes.txt

```scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt```

# Armazenando Arquivos do Seu Host - WEB

Documentação Pyhton3 ```https://docs.python.org/3/library/http.server.html```

Máquinas com Ubuntu vêm pré-instaladas com python3. O Python fornece um módulo leve e fácil de usar chamado "HTTPServer". Este módulo transforma seu computador em um servidor web rápido e fácil de usar que você pode usar para armazenar seus próprios arquivos, de onde eles podem ser baixados por outro computador usando comandos como ```curl``` e ```wget```

O "HTTPServer" do Python3 servirá os arquivos no diretório onde você executar o comando, mas isso pode ser alterado fornecendo opções que podem ser encontradas nas páginas do manual. Simplesmente, tudo o que precisamos fazer é executar ```python3 -m http.server``` no terminal para iniciar o módulo.
Agora, vamos usar o wget para baixar o arquivo usando o endereço 10.10.233.201 e o nome do arquivo. Lembre-se: como o servidor python3 está executando a porta 8000, você precisará especificar isso no seu comando wget. Por exemplo:

```wget http://10.10.233.201:8000/myfile```

Observe que você precisará abrir um novo terminal para usar o wget e sair daquele em que você iniciou o servidor web Python3. Isso ocorre porque, depois que você iniciar o servidor web Python3, ele será executado nesse terminal até que você o cancele.

Lembre-se, você precisará executar o comando wget em outro terminal (mantendo ativo o terminal que está executando o servidor Python3).

# Processos Ativos no Kernel
Processos são os programas em execução na sua máquina. Eles são gerenciados pelo kernel, onde cada processo terá um ID associado, também conhecido como PID. O PID aumenta na ordem em que o processo é iniciado. Ou seja, o 60º processo terá um PID de 60.

### Visualizando Processos

Podemos usar o comando amigável ```ps``` para fornecer uma lista dos processos em execução como a sessão do nosso usuário e algumas informações adicionais, como seu código de status, a sessão que o está executando, quanto tempo de uso da CPU ele está usando e o nome do programa ou comando que está sendo executado.

### Gerenciando Processos

Você pode enviar comandos que encerram processos; há uma variedade de tipos de sinais que se correlacionam com o quão "limpo" o processo é tratado pelo kernel. Para encerrar um comando, podemos usar o comando apropriadamente nomeado "kill" e o PID associado que desejamos encerrar. Ou seja, para encerrar o PID 1337, usaríamos ```kill 1337```

Abaixo estão alguns dos comandos que podemos enviar a um processo quando ele é encerrado:

* SIGTERM - Encerra o processo, mas permite que ele execute algumas tarefas de limpeza previamente
* SIGKILL - Encerra o processo - não realiza nenhuma limpeza posterior
* SIGSTOP - Interrompe/suspende um processo

### Como os Processos Iniciam?

Vamos começar falando sobre namespaces. O Sistema Operacional (SO) usa namespaces para, em última análise, dividir os recursos disponíveis no computador entre processos (como CPU, RAM e prioridade). Pense nisso como dividir seu computador em fatias — semelhante a um bolo. Os processos dentro dessa fatia terão acesso a uma certa quantidade de poder computacional, porém, será uma pequena parte do que está realmente disponível para todos os processos em geral.

Namespaces são ótimos para segurança, pois são uma forma de isolar processos uns dos outros — somente aqueles que estão no mesmo namespace poderão se ver.

O processo com ID 0 é um processo que é iniciado quando o sistema inicializa. Esse processo é o init do sistema no Ubuntu, como o systemd, que é usado para fornecer uma maneira de gerenciar os processos de um usuário e fica entre o sistema operacional e o usuário.

Por exemplo, assim que um sistema inicializa, o systemd é um dos primeiros processos a ser iniciado. Qualquer programa ou software que queiramos iniciar será iniciado como um processo filho do systemd. Isso significa que ele é controlado pelo systemd, mas será executado como um processo próprio (embora compartilhe os recursos do systemd) para facilitar a identificação e afins.

### Inicializando Processos/Serviços na Inicialização

Alguns aplicativos podem ser iniciados na inicialização do sistema que possuímos. Por exemplo, servidores web, servidores de banco de dados ou servidores de transferência de arquivos. Esses softwares costumam ser críticos e, com frequência, são instruídos a iniciar durante a inicialização do sistema pelos administradores.

Neste exemplo, vamos instruir o servidor web Apache a iniciar o Apache manualmente e, em seguida, instruir o sistema a iniciar o Apache2 na inicialização.

Entramos em cena com o comando ```systemctl``` — este comando nos permite interagir com o processo/daemon do systemd. Continuando com nosso exemplo, systemctl é um comando fácil de usar que possui a seguinte formatação: ```systemctl [opção] [serviço]```

Por exemplo, para instruir o Apache a iniciar, usaremos ```systemctl start apache2```. Se quiséssemos parar o Apache, bastaríamos substituir a [opção] por stop (em vez de start).

Podemos fazer quatro opções com systemctl:

* start
* stop
* enable
* disable

### Introdução ao Primeiro e Segundo Plano no Linux

Os processos podem ser executados em dois estados: em segundo plano e em primeiro plano. Por exemplo, comandos que você executa no seu terminal, como "echo" ou algo do tipo, serão executados em primeiro plano, pois é o único comando fornecido que não foi instruído a ser executado em segundo plano. "Echo" é um ótimo exemplo, pois a saída de echo retornará para você em primeiro plano, mas não em segundo plano.

Por exemplo executamos ```echo "hello world"```, onde esperamos que a saída seja retornada como no início. Mas, após adicionar o operador ```&``` ao comando, recebemos apenas o ID do processo echo em vez da saída real — já que ele está sendo executado em segundo plano.

Isso é ótimo para comandos como copiar arquivos, pois significa que podemos executar o comando em segundo plano e continuar com quaisquer outros comandos que desejarmos (sem ter que esperar a cópia do arquivo terminar primeiro).

Podemos fazer exatamente o mesmo ao executar coisas como scripts — em vez de depender do operador ```&```, podemos usar ```Ctrl + Z``` no teclado para colocar um processo em segundo plano. Também é uma maneira eficaz de "pausar" a execução de um script ou comando.
Este script continuará repetindo "This will keep on looping until I stop!" até que você pare ou suspenda o processo. Usando Ctrl + Z (conforme indicado por T^Z). Agora nosso terminal não estará mais cheio de mensagens — até que o coloquemos em primeiro plano.

### Automação
Os usuários podem querer agendar uma determinada ação ou tarefa para ocorrer após a inicialização do sistema. Por exemplo, executar comandos, fazer backup de arquivos ou iniciar seus programas favoritos, como Spotify ou Google Chrome.

Vamos falar sobre o processo ```cron```, mas, mais especificamente, como podemos interagir com ele por meio do uso de ```crontabs```. O Crontab é um dos processos iniciados durante a inicialização, responsável por facilitar e gerenciar tarefas do cron.
Um crontab é simplesmente um arquivo especial com formatação reconhecida pelo processo cron para executar cada linha passo a passo.
Crontabs requerem 6 valores específicos:
* ```MIN Em que minuto executar```
* ```HOUR Em que hora executar```
* ```DOM Em que dia do mês executar```
* ```MON Em que mês do ano executar```
* ```DOW Em que dia da semana executar```
* ```CMD O comando real que será executado```

Por exemplo um backup de arquivos. Você pode querer fazer backup dos "Documentos" do "ubuntu" a cada 12 horas. Usaríamos a seguinte formatação:

0 */12 * * * cp -R /home/ubuntu/Documentos/var/backups/

Um recurso interessante dos crontabs é que eles também suportam o curinga ou asterisco (*). Se não quisermos fornecer um valor para aquele campo específico, ou seja, não importa o mês, dia ou ano em que ele é executado — apenas que ele seja executado a cada 12 horas — simplesmente colocamos um asterisco.

Um ótimo site para gerar crontabs é o Cronguru
Os crontabs podem ser editados usando crontab -e, onde você pode selecionar um editor (como o Nano) para editar seu crontab.

### Pacotes e Repositórios de Software

Quando os desenvolvedores desejam enviar software para a comunidade, eles o enviam para um repositório ```apt```.

Se aprovados, seus programas e ferramentas serão disponibilizados. Dois dos recursos mais vantajosos do Linux se destacam aqui:
* a acessibilidade do usuário
* mérito das ferramentas de código aberto.

Ao usar o comando ```ls``` em uma máquina Linux Ubuntu 20.04, esses arquivos servem como gateway/registro.

Embora os fornecedores de sistemas operacionais mantenham seus próprios repositórios, você também pode adicionar repositórios da comunidade à sua lista! Isso permite ampliar os recursos do seu sistema operacional. Repositórios adicionais podem ser adicionados usando o comando ```add-apt-repository``` ou listando outro fornecedor! Por exemplo, alguns fornecedores terão um repositório mais próximo de sua localização geográfica.

### Gerenciando Seus Repositórios (Adicionando e Removendo)

Normalmente, usamos o comando ```apt``` para instalar software em nosso sistema Ubuntu. O comando ```apt``` faz parte do software de gerenciamento de pacotes, também chamado de apt. O Apt contém um conjunto completo de ferramentas que nos permite gerenciar os pacotes e fontes do nosso software, além de instalar ou remover software simultaneamente.
Embora você possa instalar software usando instaladores de pacotes como o ```dpkg```, os benefícios do apt significam que, sempre que atualizamos nosso sistema, o repositório que contém os softwares que adicionamos também é verificado em busca de atualizações.

# Logs
Os logs estão ocalizados no diretório /var/log, esses arquivos e pastas contêm informações de log para aplicativos e serviços em execução no seu sistema. O Sistema Operacional (SO) se tornou bastante eficiente em gerenciar esses logs automaticamente em um processo conhecido como "rotação".
Esses serviços e logs são uma ótima maneira de monitorar a saúde do seu sistema e protegê-lo. Além disso, os logs de serviços como um servidor web contêm informações sobre cada solicitação, permitindo que desenvolvedores ou administradores diagnostiquem problemas de desempenho ou investiguem a atividade de um intruso.
