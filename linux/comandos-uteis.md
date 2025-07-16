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







