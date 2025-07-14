## O que é o MAC Address?

Em inglês MAC (Media Access Control) é a digital do seu dispositivo, ele é único. É separado em seis setores, contendo dois caracteres e separado por dois pontos cada, esses dois pontos são considerados separadores. Por exemplo, a4:c3:f0:85:ac:2d. Os primeiros seis caracteres representam a empresa que fez a interface de rede, e os últimos seis é um número único.
Apesar de único, existe a possibilidade de falsificar o endereço MAC, por um método chamado "Falsificação"
Um firewall está configurado para permitir qualquer comunicação de e para o endereço MAC do administrador. Se um dispositivo fingisse ou "falsifasse" esse endereço MAC, o firewall agora pensaria que está recebendo comunicação do administrador quando não está.

## Ping

Utiliza o protocolo ICMP (Internet Control Message Protocol) para determinar o desempenho de conexão entre dispositivos, enviando um pacote de eco e retornando a resposta.

## Topologias
### Topologia Estrela
Os dispositivos estão conectados em um dispositivo central (geralmente um switch). Como é uma rede altamente escavável, é uma das mais utilizadas atualmente, apesar do custo elevado, comparado à outras topologias, pois permite adicionar novos dispositivos com mais facilidade. O malefício desta topologia está em quanto mais escalar, mais manutenção será necessária para manter em ordem, além de que se o dispositivo central falhar, o restante dos dispositivos conectados não terão mais acesso, apesar desses dispositivos centrais serem geralmente mais robustos.

### Topologia de barramento
Uma topologia extremamente barata e simples. Todos os dispositivos estão conectados à um cabo backbone, podendo comparar este tipo como um galho de árvore, onde o galho é o backbone e as folhas serão os dispositivos. A maior contrapartida desta topologia é a falta de redundância, onde se o cabo falhar, todos os dispositivos ficarão sem comunicação.

### Topologia Anel
Dispositivos como computadores são conectados diretamente entre si para formar um loop, o que significa que há pouco cabeamento necessário e menos dependência de hardware dedicado, como dentro de uma topologia em estrela.
Uma topologia de anel funciona enviando dados através do loop até chegar ao dispositivo destinado, usando outros dispositivos ao longo do loop para encaminhar os dados. Curiosamente, um dispositivo só enviará dados recebidos de outro dispositivo nesta topologia se não tiver nenhum para enviar.
Se acontecer de o dispositivo ter dados para enviar, ele enviará seus próprios dados primeiro antes de enviar dados de outro dispositivo.
Por último, as topologias em anel são menos propensas a gargalos, como dentro de uma topologia de barramento, já que grandes quantidades de tráfego não viajam pela rede ao mesmo tempo. O design desta topologia significa, no entanto, que uma falha, como um cabo cortado ou um dispositivo quebrado, resultará na quebra de toda a rede.

## O que é um switch?
Os switches são dispositivos dedicados dentro de uma rede que são projetados para agregar vários outros dispositivos, como computadores, impressoras ou qualquer outro dispositivo compatível com rede. Os switches monitoram qual dispositivo está conectado a qual porta. Dessa forma, quando eles recebem um pacote, em vez de repetir esse pacote para todas as portas como um hub faria, ele apenas o envia para o alvo pretendido, reduzindo assim o tráfego de rede. Tanto os switches quanto os roteadores podem ser conectados entre si. A capacidade de fazer isso aumenta a redundância de uma rede, adicionando vários caminhos para os dados tomarem. Se um caminho for para baixo, outro pode ser usado. Embora isso possa reduzir o desempenho geral de uma rede porque os pacotes precisam levar mais tempo para viajar, não há tempo de inatividade.

## O que é um roteador?
É função de um roteador conectar redes e passar dados entre elas. Roteamento é o rótulo dado ao processo de deslocamento de dados pelas redes. O roteamento envolve a criação de um caminho entre as redes para que esses dados possam ser entregues com sucesso.

## ARP
O Protocolo de Resolução de Endereços (ARP) é responsável por encontrar o endereço MAC (hardware) relacionado a um endereço IP específico. Ele funciona transmitindo uma consulta ARP: "Quem tem este endereço IP?". E a resposta é no formato: "O endereço IP está neste endereço MAC".
O ARP permite que um dispositivo associe seu endereço MAC a um endereço IP na rede. Cada dispositivo em uma rede manterá um registro dos endereços MAC associados a outros dispositivos.
Quando os dispositivos desejam se comunicar, eles enviam um broadcast para toda a rede em busca do dispositivo específico. Os dispositivos podem usar o ARP para encontrar o endereço MAC de um dispositivo.

Há dois tipos de mensagem ARP

**Solicitação ARP**
**Resposta ARP**
Quando uma **solicitação ARP** é enviada, uma mensagem é transmitida na rede para outros dispositivos perguntando: "Qual é o endereço MAC que possui este endereço IP?". Quando os outros dispositivos recebem essa mensagem, eles só responderão se possuírem esse endereço IP e enviarão uma **resposta ARP** com seu endereço MAC. O dispositivo solicitante agora pode se lembrar desse mapeamento e armazená-lo em seu cache ARP para uso futuro.

## DHCP
O Dynamic Host Configuration Protocol (DHCP) é um protocolo de gerenciamento de rede usado em redes de protocolo de Internet (IP) para atribuir automaticamente endereços IP e outros parâmetros de comunicação a dispositivos conectados à rede usando uma arquitetura client–server.
Quando um dispositivo se conecta a uma rede, caso ainda não tenha recebido um endereço IP manualmente, ele envia uma solicitação **(DHCP Discover)** para verificar se há servidores DHCP na rede. O servidor DHCP então responde com um endereço IP que o dispositivo poderia usar **(DHCP Offer)**. O dispositivo então envia uma resposta confirmando que deseja o endereço IP oferecido **(DHCP Request)** e, por fim, o servidor DHCP envia uma resposta confirmando a conclusão da solicitação, e o dispositivo pode começar a usar o endereço IP **(DHCP ACK)**.

DHCP Discover: CLIENTE: "ei, sou novo aqui, poderia me fornecer um IP?"
DHCP Offer: SERVIDOR: "claro, podes ficar com o 192.168.1.10"
DHCP Request: CLIENTE: "show, vou ficar com esse endereço IP"
DHCP ACK: SERVIDOR: "você poderá usar esse endereço IP pelas próximas 24 horas" (ou a quantidade de tempo definida no escopo)

## Modelo OSI (Open Systems Interconnection)
É um modelo crucial para as redes de computadores, que ditam o que cada dispositivo da rede enviará, receberá e interpretará os dados. Cada camada individual efetua uma tarefa, um processo que se chama encapsulamento.

### Camada Física
A primeira camada do medelo OSI, os dispositivos usam sinais elétricos para transferir dados entre si em um sistema de numeração binária (1 e 0). O principal meio físico utilizado é o cabo ethernet conectado aos dispositivos.

### Camada de Enlace
Dentro de um dispositivo, há uma placa chamada NIC (Network Interface Card), que possui um endereço MAC (Media Access Control) pré definido pela fabricante do dispositivo. Então é a missão da camada de enlace, determinar para aonde as informações devem ir. Também é função desta camada, apresentar os dados em um formato adequado para transmissão.

### Camada de Rede
É a camada onde ocorre o roteamento e remotagem de dados. O roteamento determina o caminho mais adequado para onde esses dados deverão ser enviados. Os protocolos nessa camada, determinam o melhor caminho por meio do OSPF (Open Shortest Path First) e RIP (Routing Information Protocol). Os fatores que são utilizados para decidir o caminho são:

Qual caminho é o mais curto? Ou seja, tem a menor quantidade de dispositivos pelos quais o pacote precisa viajar.
Qual caminho é o mais confiável? Ou seja, pacotes foram perdidos nesse caminho antes?
Qual caminho tem a conexão física mais rápida? Ou seja, um caminho usa uma conexão de cobre (mais lenta) ou uma fibra (consideravelmente mais rápida)?

Nesta camada, tudo é tratado através de endereços IP como 192.168.1.100. Dispositivos como roteadores capazes de entregar pacotes usando endereços IP são conhecidos como dispositivos de Camada 3 — porque são capazes de funcionar na terceira camada do modelo OSI.

### Camada de Transporte
Essa é uma camada extremamente essencial para o transporte de dados pela rede. Quando os dados são enviados entre os dispositivos, eles seguem um dos dois protocolos distintos de rede, que são definidos por alguns fatores específicos. O TCP e o UDP.

**TCP**
TCP (Transmission Control Protocol) é um protocolo orientado à conexão que requer um handshake TCP triplo para estabelecer uma conexão. O TCP proporciona transferência confiável de dados, controle de fluxo e controle de congestionamento. Protocolos de nível superior, como HTTP, POP3, IMAP e SMTP, utilizam TCP. Este protocolo foi projetado com confiabilidade e garantia em mente. Este protocolo reserva uma conexão constante entre os dois dispositivos durante o tempo necessário para que os dados sejam enviados e recebidos.

Além disso, o TCP incorpora a verificação de erros em seu design. A verificação de erros é a forma como o TCP garante que os dados enviados dos pequenos blocos na camada de sessão (camada 5) foram recebidos e remontados na mesma ordem.

O TCP é usado em situações como compartilhamento de arquivos, navegação na internet ou envio de e-mail. Esse uso se deve ao fato de que esses serviços exigem que os dados sejam precisos e completos.
Ao envio, um arquivo é dividido em pequenos pedaços de dados (conhecidos como pacotes) a partir do "servidor web", onde o "computador" reconstrói o arquivo.

*Vantagens do TCP*

* Garante a precisão dos dados.
* Capaz de sincronizar dois dispositivos para evitar que um ao outro seja inundado com dados.
* Executa muito mais processos para garantir a confiabilidade.

*Desvantagens do TCP*

* Requer uma conexão confiável entre os dois dispositivos. Se um pequeno bloco de dados não for recebido, todo o bloco de dados não poderá ser utilizado.
* Uma conexão lenta pode causar gargalos em outro dispositivo, pois a conexão ficará reservada no computador receptor o tempo todo.
* O TCP é significativamente mais lento que o UDP porque mais trabalho precisa ser feito pelos dispositivos que usam este protocolo.

**UDP**
UDP (User Datagram Protocol) é um protocolo sem conexão; o UDP não exige o estabelecimento de uma conexão. O UDP é adequado para protocolos que dependem de consultas rápidas, como DNS, e para protocolos que priorizam comunicações em tempo real, como conferências de áudio/vídeo e transmissão. Este protocolo não é tão avançado quanto o protocolo TCP. Ele não possui os muitos recursos oferecidos pelo TCP, como verificação de erros e confiabilidade. Na verdade, todos os dados enviados via UDP são enviados ao computador, independentemente de chegarem lá ou não. Não há sincronização entre os dois dispositivos nem garantias.

*Vantagens do UDP*

* UDP é muito mais rápido que o TCP
* O UDP deixa a camada de aplicação (software do usuário) decidir se há algum controle sobre a velocidade de envio dos pacotes.
* O UDP não reserva uma conexão contínua em um dispositivo como o TCP faz.

*Desvantagens do UDP*

* O UDP não leva em consideração a garantia de entrega
* Apesar da flexibilidade para desenvolvedores, se a conexão de internet for lenta, a experiência de usuário será péssima

O UDP é útil em situações em que há pequenos pedaços de dados sendo enviados. Por exemplo, protocolos usados para descobrir dispositivos (ARP e DHCP) ou arquivos maiores, como streaming de vídeo (onde não há problema se alguma parte do vídeo estiver pixelada. Pixels são apenas pedaços de dados perdidos!)
