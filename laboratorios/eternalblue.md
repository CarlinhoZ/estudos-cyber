# Eternal Blue
Realizei um ataque em uma máquina Windows explorando a vulnerabilidade SMB MS17-010 Eternal Blue.

A fase inicial é o reconhecimento, utilizei o nmap para buscar portas abertas no IP fornecido (lembrando que é um laboratório, então o IP já é incluso).
Após isso, descobri 4 portas úteis para uma invasão, porém usei a 445 (SMB). Com isso, utilizando o Metasploit, junto do payload ```exploit eternalblue```. Quando acessei o dispositivo, deixei em modo background, para utilizar outro payload, o ```shell_to_meterpreter```, que funciona para escalonar os privilégios. Quando acesso o dispositivo em modo root, migro o processo usando o comando ```migrate```.
Com a permissão na mão, utilizei o ```hashdump``` para buscar o hash das senhas armazenadas, que após, utilizei um site externo para traduzir este valor, assim conseguindo a senha.
Por fim, busquei três flags deste laboratório. Localizei cada uma, no Windows, utilizando o comando ```where /r C:\ "flag1.txt"```, onde:

* where: comando de busca do Windows
* /r: parâmetro que busca em todo o caminho inserido a sua direita
* C:\: caminho que decidi buscar o arquivo

E depois, utilizando o ```type```, consegui retirar todas as flags necessárias.
