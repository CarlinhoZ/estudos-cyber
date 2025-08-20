# Busca de informações em Windows Server 2019.
A primeira exploração que realizei foi acessar uma porta SMB aberta (como era um laboratório teste, eu havia o usuário e senha, junto do IP interno). O sistema operacional era Windows Server 2019

O primeiro passo que realizei foi conectar ao console do metasploit utilizando o comando ```msfconsole```.

Usei o exploit psexec (exploit/windows/smb/psexec), inseri o IP da "vítima" e inseri a porta aberta (445).
Ao conectar na máquina (meterpreter), utilizei o ```systeminfo``` para descobrir qual o nome do computador ```ACME-TEST```.
Para descobrir o domínio, rodei um ```shell``` para conectar no CMD do servidor, após isso utilizei o ```ipconfig /all``` para verificar as configurações de rede, consequentemente seu domínio.
Busquei qual era os compartilhamentos de rede, ainda no CMD, usando ```net share``` encontrando o speedster.
Também busquei o hash NTLM do usuário jchambers, mudando o PID de um serviço, utilizando o ```migrate```, após isso utilizei o ```hashdump```.
Depois busquei qual era o retorno real do hash, por plataforma online, me retornando a senha ```Trustno1```.
No CMD, busquei qual o local do arquivo utilizando o ```where /R C:\ "arquivo.txt".

Assim, conclui a primeira pós-exploração usando o meterpreter.
