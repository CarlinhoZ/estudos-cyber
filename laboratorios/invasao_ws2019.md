# Laboratório de Testes de Invasão – Windows Server 2019

O objetivo deste exercício foi realizar a **coleta de informações e pós-exploração** em um ambiente controlado com Windows Server 2019. Como se tratava de um laboratório, eu possuía credenciais válidas (usuário e senha) e o IP interno da máquina alvo.

O primeiro passo foi iniciar o **Metasploit Framework**, utilizando o comando `msfconsole`. Com isso, carreguei o módulo **exploit/windows/smb/psexec**, que permite a execução remota de comandos em sistemas Windows através de SMB, informando o IP da vítima e a porta padrão (445) aberta para SMB.

Ao estabelecer a sessão **Meterpreter**, realizei uma análise inicial do sistema com `systeminfo`, identificando o nome do computador como **ACME-TEST**. Para determinar o domínio da rede, utilizei um shell interativo (`shell`) e executei `ipconfig /all`, obtendo as informações de rede e o domínio associado.

Na sequência, investiguei os **compartilhamentos de rede** disponíveis com o comando `net share`, identificando o compartilhamento chamado **speedster**. Em seguida, foquei na extração de credenciais: migrei para um processo do sistema (`migrate`) e utilizei o comando `hashdump` para obter os **hashes NTLM** dos usuários, incluindo o usuário **jchambers**. Ao consultar o hash em plataformas de quebra de senha, obtive a senha em texto claro: **Trustno1**.

Para localizar arquivos específicos no servidor, utilizei o comando do Windows:

```
where /R C:\ "arquivo.txt"
```

Com isso, concluí a primeira etapa de pós-exploração utilizando o Meterpreter, realizando coleta de informações críticas, análise de compartilhamentos, extração de credenciais e localização de arquivos sensíveis.
