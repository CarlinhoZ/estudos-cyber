# Exploração da Vulnerabilidade MS17-010 – EternalBlue

Neste exercício, explorei uma máquina Windows vulnerável à **MS17-010**, conhecida como **EternalBlue**, focando em coleta de informações, escalonamento de privilégios e captura de flags do laboratório.

A primeira fase foi o **reconhecimento**. Utilizei o **Nmap** para mapear portas abertas no IP fornecido (lembrando que, por se tratar de um laboratório, o IP já era conhecido). Foram identificadas quatro portas relevantes para exploração, sendo escolhida a porta **445 (SMB)** como vetor de ataque.

Em seguida, utilizei o **Metasploit Framework** para carregar o módulo **exploit/windows/smb/eternalblue**, executando o payload inicial. Ao estabelecer acesso à máquina vulnerável, deixei a sessão em **background** para utilizar o **payload `shell_to_meterpreter`**, que permite escalonamento de privilégios e integração com o Meterpreter.

Após obter privilégios elevados (**root/administrador**), migrei o processo crítico com o comando `migrate`, garantindo persistência da sessão e acesso estável. Com as permissões necessárias, executei `hashdump` para extrair os **hashes NTLM** das senhas armazenadas no sistema. Os hashes foram posteriormente convertidos em senhas em texto claro utilizando ferramentas online de quebra de hash, obtendo credenciais válidas.

Por fim, busquei as três **flags do laboratório**. Para localizar cada arquivo, utilizei o comando do Windows:

```
where /R C:\ "flag1.txt"
```

* `where`: comando de busca do Windows
* `/R`: parâmetro que realiza busca recursiva em todos os diretórios do caminho especificado
* `C:\`: caminho base da pesquisa

Após localizar os arquivos, utilizei o comando `type` para exibir o conteúdo das flags e concluir a coleta com sucesso.
