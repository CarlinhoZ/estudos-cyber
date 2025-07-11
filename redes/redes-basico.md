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
