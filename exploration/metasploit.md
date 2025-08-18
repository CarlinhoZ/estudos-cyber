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

### 🔹 Sessões

* Quando o exploit funciona, cria-se uma **sessão** (ex: Meterpreter).
* `background` ou `CTRL+Z` → coloca sessão em segundo plano.
* `sessions` → lista sessões ativas.
* `sessions -i <id>` → interage com uma sessão específica.

---

```
Em resumo:
O texto explica como navegar no Metasploit, configurar parâmetros de módulos (principalmente RHOSTS, RPORT, LHOST, LPORT), rodar exploits, lidar com sessões abertas e usar recursos como `setg` e `unset`. O exemplo todo gira em torno do exploit **MS17-010 (EternalBlue)**, mostrando passo a passo desde a configuração até abrir uma sessão **Meterpreter** no alvo.
```




















