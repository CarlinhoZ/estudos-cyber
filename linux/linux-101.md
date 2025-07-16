# Principais Comandos

### echo
Saia qualquer texto que fornecer

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





