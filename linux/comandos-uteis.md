### echo
Saia qualquer texto que fornecer

### whoami
Descubra qual usuário está logado

### ls
Listar todos os arquivos de uma pasta

### cd
Mudar de diretório

### cat
Faz a leitura de conteúdos de um arquivo
Pro tip: você pode usar cat para exibir o conteúdo de um arquivo dentro de diretórios sem precisar navegar até ele usando cat e o nome do diretório. Por exemplo, ```cat /home/ubuntu/Documents/todo.txt```

### pwd
Basicamente serve para descobrir qual diretório estamos trabalhando, retornando o caminho completo

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
