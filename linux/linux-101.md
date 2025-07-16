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




