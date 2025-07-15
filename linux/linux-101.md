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
