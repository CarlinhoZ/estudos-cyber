# Shell
A maioria das distribuições Linux usa o Bash (Bourne Again Shell) como shell padrão. No entanto, o shell padrão exibido ao abrir o terminal depende da sua distribuição Linux.
/etc/shells contém todos os shells instalados em um sistema Linux

Para alternar entre esses shells, você pode digitar o nome do shell que está presente no seu sistema operacional e ele será aberto para você.
Se quiser alterar permanentemente o shell padrão, por exemplo use o comando: ```chsh -s /usr/bin/zsh```. Isso tornará este shell o shell padrão do seu terminal.

## Bourne Again Shell
O Bourne Again Shell (Bash) é o shell padrão para a maioria das distribuições Linux. Ao abrir o terminal, o bash está presente para você inserir comandos. Antes do bash, alguns shells, como sh, ksh e csh, tinham recursos diferentes. O Bash surgiu como um substituto aprimorado para esses shells, incorporando recursos de todos eles. Isso significa que ele possui muitos dos recursos desses shells antigos e algumas de suas habilidades únicas.
* Bash é um shell amplamente utilizado com recursos de script.
* Ele oferece um recurso de conclusão com tabulação, o que significa que, se você estiver no meio da conclusão de um comando, pode pressionar a tecla Tab no seu teclado. Ele completará o comando automaticamente com base em uma possível correspondência ou oferecerá várias sugestões para concluí-lo.
* O Bash mantém um arquivo de histórico e registra todos os seus comandos. Você pode usar as teclas de seta para cima e para baixo para usar os comandos anteriores sem digitá-los novamente. Você também pode digitar ```history``` para exibir todos os seus comandos anteriores.

## Friendly Interactive Shell (FISH)
O Friendly Interactive Shell (Fish) também não é padrão na maioria das distribuições Linux. Como o próprio nome sugere, ele se concentra mais na facilidade de uso do que outros shells. 
* Ele oferece uma sintaxe muito simples, viável para usuários iniciantes.
* Ao contrário do bash, ele possui correção ortográfica automática para os comandos que você escreve.
* Você pode personalizar o prompt de comando com alguns temas interessantes usando o fish.
* O recurso de destaque de sintaxe do fish colore diferentes partes de um comando com base em suas funções, o que pode melhorar a legibilidade dos comandos. Ele também nos ajuda a identificar erros com suas cores exclusivas.
* O fish também oferece funcionalidades de script, preenchimento automático por tabulação e histórico de comandos, como os shells mencionados nesta tarefa.

## Z Shell
O Z Shell (Zsh) não é instalado por padrão na maioria das distribuições Linux. É considerado um shell moderno que combina as funcionalidades de alguns shells anteriores.
* O Zsh oferece preenchimento automático de tabulação avançado e também é capaz de escrever scripts.
* Assim como o fish, ele também oferece correção ortográfica automática para os comandos.
* Ele oferece ampla personalização, o que pode torná-lo mais lento do que outros shells.
* Ele também oferece preenchimento automático de tabulação, funcionalidade de histórico de comandos e vários outros recursos.

# Scriping com Shell
Um script de shell nada mais é do que um conjunto de comandos. Suponha que uma tarefa repetitiva exija que você insira vários comandos usando um shell. Em vez de inseri-los um após o outro a cada repetição da tarefa, o que pode levar mais tempo, você pode combiná-los em um script. Para executar todos esses comandos, você executará apenas o script, e todos os comandos serão executados. Todos os shells mencionados nas tarefas anteriores possuem recursos de script. Scripts nos ajudam a automatizar tarefas. Antes de aprender a escrever um script, precisamos saber que, embora os shells do Linux tenham recursos de script, isso não significa que você só pode criar um script usando um shell. Scripts também podem ser feitos em várias linguagens de programação. No entanto, o escopo desta sala é abordar scripts usando um shell.

O primeiro passo é abrir o terminal e selecionar um shell. Vamos usar o shell bash, o shell padrão e amplamente utilizado na maioria das distribuições.

Ao contrário dos outros comandos que digitamos no shell, primeiro precisamos criar um arquivo usando qualquer editor de texto para o script. O arquivo deve ter a extensão .sh, a extensão padrão para scripts bash.

Exemplo: ```nano first_script.sh``` <= lembrando que o ```nano``` é um editor de texto base do Linux

Todo script deve começar com shebang. Shebang é uma combinação de alguns caracteres adicionados no início de um script, começando com ```#!``` seguido pelo nome do interpretador a ser usado durante a execução do script. Como escrevi em bash, vou defini-lo como o interpretador no shebang.

```#!/bin/bash```

## Variáveis
Uma variável armazena um valor dentro dela. Suponha que você precise usar alguns valores complexos, como uma URL, um caminho de arquivo, etc., várias vezes em seu script. Em vez de memorizá-los e escrevê-los repetidamente, você pode armazená-los em uma variável e usar o nome da variável onde precisar.

O script abaixo exibe uma string na tela: "Ei, qual é o seu nome?". Isso é feito pelo comando echo. A segunda linha do script contém o código ```read name```. ```read``` é usado para receber a entrada do usuário e "name" é a variável na qual a entrada seria armazenada. A última linha usa "echo" para exibir a linha de boas-vindas para o usuário, juntamente com seu nome armazenado na variável.
```
# Definindo o Interpretador
#!/bin/bash
echo "Ei, qual é o seu nome?"
"read name"
echo "Bem-vindo, $name"
```

Para executar o script, primeiro precisamos garantir que ele tenha permissões de execução. Para conceder essas permissões ao script, podemos digitar o seguinte comando em nosso terminal:

```chmod +x first_script.sh```

Agora que o script tem permissões de execução, use ```./``` antes do nome do script para executá-lo. Usamos ```./``` antes do script para executá-lo, em vez de digitar o nome do script diretamente, porque ```./``` informa ao shell para executar o arquivo presente no diretório atual. Se você não definir ```./``` antes do nome do script, o shell pesquisará o script na variável de ambiente PATH (que contém todos os diretórios, exceto o atual) e não encontrará o script definido em nenhum desses diretórios, gerando um erro.

```./first_script.sh```

## Loops
Por exemplo, você tem uma lista de muitos amigos e quer enviar a mesma mensagem para eles. Em vez de enviá-los individualmente, você pode criar um loop no seu script, fornecer sua lista de amigos ao loop e a mensagem, e ele enviará essa mensagem para todos os seus amigos.

```
#!/bin/bash
for i in {1..10};
do
echo $i
done
```

A primeira linha contém a variável ```i``` que iterará de 1 a 10 e executará o código abaixo a cada iteração. ```do``` indica o início do código do loop e ```done``` indica o fim. Entre eles, deve ser escrito o código que queremos executar no loop. O loop ```for``` pegará cada número entre parênteses e o atribuirá à variável ```i``` em cada iteração. O comando ```echo $i``` exibirá o valor dessa variável a cada iteração.

## Instruções Condicionais
Instruções condicionais são uma parte essencial da criação de scripts. Elas ajudam a executar um código específico somente quando uma condição é satisfeita; caso contrário, você pode executar outro código. Suponha que você queira criar um script que mostre um segredo ao usuário. No entanto, você deseja que ele seja mostrado apenas para alguns usuários, apenas para o usuário de alta autoridade. Você criará uma instrução condicional que primeiro perguntará o nome do usuário e, se esse nome corresponder ao nome do usuário de alta autoridade, o segredo será exibido.

```
#!/bin/bash
echo "Por favor, insira seu nome primeiro:"
read name
if [ "$name" = "Stewart" ]; then
echo "Bem-vindo, Stewart! Aqui está o segredo: THM_Script"
else
echo "Desculpe! Você não está autorizado a acessar o segredo."
fi
```

O script acima recebe o nome do usuário como entrada e o armazena em uma variável. A instrução condicional começa com ```if``` e compara o valor dessa variável com a string ```Stewart```; se houver correspondência, exibirá o segredo para o usuário, ou então não. O ```fi``` é usado para encerrar a condição.

## Comentários
Às vezes, o código pode ser muito extenso. Nesse cenário, o código pode confundi-lo ao examiná-lo depois de algum tempo ou compartilhá-lo com alguém. Uma maneira fácil de resolver esse problema é usar comentários em diferentes partes do código. Um comentário é uma frase que escrevemos em nosso código apenas para facilitar o entendimento. É escrito com um sinal de # seguido por um espaço e a frase que você precisa escrever.
Comentários são feitos em scripts, utilizando o ```#```.

## Reforço de conhecimento

Um usuário possui um armário em um banco. Para proteger o armário, precisamos de um script que verifique o usuário antes de abri-lo. Ao ser executado, o script deve solicitar o nome, o nome da empresa e o PIN do usuário. Se o usuário inserir os seguintes dados, ele deverá ter permissão para entrar, ou então o acesso deverá ser negado.

Nome de usuário: John
Nome da empresa: Tryhackme
PIN: 7385

```
# Definindo o Interpretador
#!/bin/bash

# Definindo as variáveis
username=""
companyname=""
pin=""

# Definindo o loop
for i in {1..3}; do

# Definindo as instruções condicionais
if [ "$i" -eq 1 ]; then
echo "Digite seu nome de usuário:"
read username
elif [ "$i" -eq 2 ]; then
echo "Digite o nome da sua empresa:"
read companyname
else
echo "Digite seu PIN:"
read pin
fi
done

# Verificando se o usuário inseriu os dados corretos
if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
echo "Autenticação bem-sucedida. Agora você pode acessar seu armário, John."
senão
echo "Autenticação negada!!"
fi
```
















