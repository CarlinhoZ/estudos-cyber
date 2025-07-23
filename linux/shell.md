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





































