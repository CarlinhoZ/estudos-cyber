# Descoberta de Host
O Nmap utiliza várias maneiras de especificar seus alvos:

* Intervalo de IP usando -: Se você deseja escanear todos os endereços IP de 192.168.0.1 a 192.168.0.10, você pode escrever 192.168.0.1-10
* Sub-rede IP usando /: Se você deseja escanear uma sub-rede, você pode expressá-la como 192.168.0.1/24, o que seria equivalente a 192.168.0.0-255
* Nome do host: Você também pode especificar seu alvo pelo nome do host, por exemplo, example.thm

Digamos que você queira descobrir os hosts online em uma rede. O Nmap oferece a opção -sn, ou seja, ping scan.

Executar o Nmap como um usuário local (não root) limitaria a tipos fundamentais de varredura, como varreduras de eco ICMP e varreduras de conexão TCP.

# Varredura de uma Rede Local
Supondo que meu endereço IP é 192.168.66.89, vamos varrer a rede 192.168.66.0/24. O comando é:```nmap -sn 192.168.66.0/24```.
Como estamos escaneando a rede local, onde estamos conectados via Ethernet ou Wi-Fi, podemos consultar os endereços MAC dos dispositivos. Consequentemente, podemos descobrir os fornecedores das placas de rede, o que é uma informação útil, pois pode nos ajudar a adivinhar o tipo de dispositivo(s) alvo.

Ao escanear uma rede conectada diretamente, o Nmap começa enviando requisições ARP. Quando um dispositivo responde à requisição ARP, o Nmap o rotula com "Host ativo".

# Varredura de uma Rede Remota
Neste contexto, remota significa que pelo menos um roteador separa nosso sistema dessa rede. Como resultado, todo o nosso tráfego para os sistemas de destino deve passar por um ou mais roteadores. Ao contrário da varredura de uma rede local, não podemos enviar uma solicitação ARP ao destino.

Por fim, o Nmap oferece uma varredura de lista com a opção ```-sL```. Essa varredura lista apenas os alvos a serem varridos, sem realmente varrê-los. Por exemplo, nmap -sL 192.168.0.1/24 listará os 256 alvos que serão varridos. Essa opção ajuda a confirmar os alvos antes de executar a varredura propriamente dita.

Como mencionamos anteriormente, -sn visa descobrir hosts ativos sem tentar descobrir os serviços em execução neles. Essa varredura pode ser útil se você quiser descobrir os dispositivos em uma rede sem causar muito ruído. No entanto, isso não nos informará quais serviços estão em execução. Se quisermos aprender mais sobre os serviços de rede em execução nos hosts ativos, precisamos de um tipo de varredura mais "ruidosa", que exploraremos na próxima tarefa.

Clique no botão Iniciar AttackBox no topo da página e aguarde o carregamento. Assim que o AttackBox estiver pronto, abra o terminal para acessar o nmap e responder às perguntas desta e das tarefas posteriores. Além disso, clique no botão Iniciar Máquina abaixo para preparar o sistema de destino para as tarefas posteriores.

# Scan de Porta
Anteriormente, se usa o ```-sn``` para descobrir os hosts ativos, agora queremos descobrir os serviços de rede que escutam nesses hosts ativos. Por serviço de rede, queremos dizer qualquer processo que esteja escutando conexões de entrada em uma porta TCP ou UDP. Serviços de rede comuns incluem servidores web, que geralmente escutam nas portas TCP 80 e 443, e servidores DNS, que normalmente escutam na porta UDP (e TCP) 53.

* Escaneando Portas TCP
A maneira mais fácil e básica de saber se uma porta TCP está aberta seria tentar usar um telnet para a porta. Se você estiver inclinado a escanear com um cliente Telnet, tente estabelecer uma conexão TCP com cada porta de destino. Em outras palavras, você tenta completar o handshake triplo TCP com cada porta de destino; no entanto, apenas portas TCP abertas responderiam adequadamente e permitiriam o estabelecimento de uma conexão TCP. Este procedimento não é muito diferente do escaneamento de conexão do Nmap.

* Escaneamento de Conexão
O escaneamento de conexão pode ser acionado usando ```-sT```. Ele tenta completar o handshake TCP triplo com cada porta TCP de destino. Se a porta TCP estiver aberta e o Nmap se conectar com sucesso, o Nmap interromperá a conexão estabelecida.

Na captura de tela abaixo, tem o endereço IP 192.168.124.148 e o sistema de destino tem a porta TCP 22 aberta e a porta 23 fechada. Na parte marcada com 1, você pode ver como o handshake TCP triplo foi concluído e posteriormente interrompido com um pacote TCP RST-ACK pelo Nmap. A parte marcada com 2 mostra uma tentativa de conexão a uma porta fechada, e o sistema de destino respondeu com um pacote TCP RST-ACK.

<img width="1199" height="715" alt="image" src="https://github.com/user-attachments/assets/2341b7ac-5d67-4eb5-8c88-30eace76ad8a" />

# Varredura SYN (Stealth)
Ao contrário da varredura de conexão, que tenta se conectar à porta TCP de destino, ou seja, concluir um handshake triplo, a varredura SYN executa apenas a primeira etapa: envia um pacote TCP SYN. Consequentemente, o handshake triplo TCP nunca é concluído. A vantagem é que isso deve gerar menos logs, já que a conexão nunca é estabelecida e, portanto, é considerada uma varredura relativamente furtiva. Você pode selecionar a varredura SYN usando o sinalizador ```-sS```.

Na captura de tela abaixo, varremos o mesmo sistema com a porta 22 aberta. A parte marcada com 1 mostra o serviço de escuta respondendo com um pacote TCP SYN-ACK. No entanto, o Nmap respondeu com um pacote TCP RST em vez de concluir o handshake triplo TCP. A parte marcada com 2 mostra uma tentativa de conexão TCP com uma porta fechada. Nesse caso, a troca de pacotes é a mesma da varredura de conexão.

<img width="1199" height="715" alt="image" src="https://github.com/user-attachments/assets/41ab6045-8ee1-4eb6-8231-1d213e69c3a5" />

# Escaneando Portas UDP
Embora a maioria dos serviços utilize TCP para comunicação, muitos utilizam UDP. Exemplos incluem DNS, DHCP, NTP (Network Time Protocol), SNMP (Simple Network Management Protocol) e VoIP (Voice over IP). O UDP não exige o estabelecimento de uma conexão e sua posterior interrupção. Além disso, é muito adequado para comunicação em tempo real, como transmissões ao vivo. Todos esses são motivos para considerar a busca e a descoberta de serviços que escutam em portas UDP.

O Nmap oferece a opção ```-sU``` para buscar serviços UDP. Como o UDP é mais simples que o TCP, esperamos que o tráfego seja diferente. A captura de tela abaixo mostra várias respostas ICMP de destino inalcançável (porta inalcançável) enquanto o Nmap envia pacotes UDP para portas UDP fechadas.

<img width="1220" height="735" alt="image" src="https://github.com/user-attachments/assets/b5e1370c-4a99-4dc5-b257-e6a00e2a18a7" />

# Limitando as Portas de Destino
O Nmap verifica as 1.000 portas mais comuns por padrão. No entanto, isso pode não ser o que você procura. Portanto, o Nmap oferece mais algumas opções.

* ```-F``` é para o modo Rápido, que verifica as 100 portas mais comuns (em vez das 1.000 portas padrão).
* ```-p[intervalo]``` permite especificar um intervalo de portas a serem verificadas. Por exemplo, ```-p10-1024``` verifica da porta 10 à porta 1024, enquanto ```-p-25``` verifica todas as portas entre 1 e 25. Observe que ```-p-``` verifica todas as portas e é equivalente a ```-p1-65535```, sendo a melhor opção se você quiser ser o mais completo possível.

# Detecção de Versão
## Detecção de SO
Você pode habilitar a detecção de SO adicionando a opção ```-O```. Como o nome indica, a opção de detecção de SO faz com que o Nmap se baseie em vários indicadores para fazer uma estimativa precisa do SO de destino. Nesse caso, ele detecta se o alvo possui Linux 4.x ou 5.x em execução. Isso é verdade. No entanto, não existe um detector de SO perfeitamente preciso. A afirmação de que está entre 4.15 e 5.8 é muito próxima, pois o SO do host de destino é 5.15.

## Detecção de Serviço e Versão
Você descobriu várias portas abertas e quer saber quais serviços estão escutando nelas. ```-sV``` habilita a detecção de versão. Isso é muito conveniente para coletar mais informações sobre o seu alvo com menos pressionamentos de tecla. A saída do terminal abaixo mostra uma coluna adicional chamada "version", indicando a versão do servidor SSH detectada.
E se você pudesse ter ```-O```, ```-sV``` e mais algumas opções em uma única opção? Seria ```-A```. Essa opção permite a detecção do sistema operacional, verificação de versão e traceroute, entre outras funções.

# Forçando a Varredura
Quando executamos nossa varredura de portas, como usando ```-sS```, existe a possibilidade de o host de destino não responder durante a fase de descoberta de hosts (por exemplo, um host não responde a solicitações ICMP). Consequentemente, o Nmap marcará esse host como inativo e não iniciará uma varredura de portas nele. Podemos solicitar ao Nmap que trate todos os hosts como online e faça uma varredura de portas em todos os hosts, incluindo aqueles que não responderam durante a fase de descoberta de hosts. Essa opção pode ser acionada adicionando a opção ```-Pn```.

# Velocidade das análises de porta
O Nmap oferece várias opções para controlar a velocidade e o tempo de varredura.

Executar sua varredura em velocidade normal pode acionar um IDS ou outras soluções de segurança. É razoável controlar a velocidade de uma varredura. O Nmap oferece seis modelos de temporização, e os nomes dizem tudo: paranoico (0), furtivo (1), educado (2), normal (3), agressivo (4) e insano (5). Você pode escolher o modelo de temporização pelo nome ou número. 









