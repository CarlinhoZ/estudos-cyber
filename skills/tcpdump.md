# Comandos
A primeira coisa a decidir é qual interface de rede escutar usando ```-i INTERFACE```. Você pode optar por escutar em todas as interfaces disponíveis usando ```-i any```; como alternativa, você pode especificar uma interface na qual deseja escutar, como ```-i eth0```.

Um comando como ```ip address show (ou simplesmente ip a s)``` listaria as interfaces de rede disponíveis.

# Salvar os pacotes capturados
Em muitos casos, você deve verificar os pacotes capturados novamente mais tarde. Isso pode ser feito salvando-os em um arquivo usando ```-w NOME_DO_ARQUIVO```. A extensão do arquivo é geralmente definida como ```.pcap```. Os pacotes salvos podem ser inspecionados posteriormente usando outro programa, como o Wireshark. Você não verá os pacotes rolando ao escolher a opção -w.

# Ler Pacotes Capturados de um Arquivo
Você pode usar o Tcpdump para ler pacotes de um arquivo usando ```-r NOME_DO_ARQUIVO```. Isso é muito útil para aprender sobre o comportamento do protocolo. Você pode capturar o tráfego de rede durante um período de tempo adequado para inspecionar um protocolo específico e, em seguida, ler o arquivo capturado enquanto aplica filtros para exibir os pacotes de seu interesse. Além disso, pode ser um arquivo de captura de pacotes que contém um ataque de rede ocorrido, e você o inspeciona para analisar o ataque.

# Limite o Número de Pacotes Capturados
Você pode especificar o número de pacotes a serem capturados especificando a contagem usando ```-c QUANTIDADE```. Sem especificar uma contagem, a captura de pacotes continuará até que você a interrompa, por exemplo, pressionando CTRL-C. Dependendo do seu objetivo, você precisa apenas de um número limitado de pacotes.

# Não resolva endereços IP e números de porta
O Tcpdump resolverá endereços IP e imprimirá nomes de domínio amigáveis sempre que possível. Para evitar tais consultas de DNS, você pode usar o argumento ```-n```. Da mesma forma, se você não quiser que os números de porta sejam resolvidos, como 80 sendo resolvido para http, você pode usar o argumento ```-nn``` para interromper as consultas de DNS e de número de porta.

# Produzir uma Saída (Mais) Detalhada
Se desejar imprimir mais detalhes sobre os pacotes, você pode usar ```-v``` para produzir uma saída um pouco mais detalhada. De acordo com a página de manual do Tcpdump ```man tcpdump```, a adição de ```-v``` imprimirá "o tempo de vida, a identificação, o comprimento total e as opções em um pacote IP", entre outras verificações. O -vv produzirá uma saída mais detalhada; o ```-vvv``` fornecerá ainda mais detalhes.

# Cheat Sheet
Explicação do Comando
* ```tcpdump -i INTERFACE``` Captura pacotes em uma interface de rede específica
* ```tcpdump -w NOME_DO_ARQUIVO``` Grava os pacotes capturados em um arquivo
* ```tcpdump -r NOME_DO_ARQUIVO``` Lê os pacotes capturados de um arquivo
* ```tcpdump -c QUANTIDADE``` Captura um número específico de pacotes
* ```tcpdump -n``` Não resolve endereços IP
* ```tcpdump -nn``` Não resolve endereços IP e não resolve números de protocolo
* ```tcpdump -v``` Exibição detalhada; a verbosidade pode ser aumentada com ```-vv``` e ```-vvv```

Exemplos:

* ```tcpdump -i eth0 -c 50 -v``` captura e exibe 50 pacotes escutando na interface eth0, que é uma Ethernet com fio, e os exibe detalhadamente.
* ```tcpdump -i wlo1 -w data.pcap``` captura pacotes escutando na interface wlo1 (a interface WiFi) e grava os pacotes em data.pcap. A captura continua até que o usuário interrompa a captura pressionando CTRL-C.
* ```tcpdump -i any -nn``` captura pacotes em todas as interfaces e os exibe na tela sem resolução de nome de domínio ou protocolo.

# Filtros
## Filtrando por Host
Digamos que você esteja interessado apenas em pacotes IP trocados com sua impressora de rede ou um servidor de jogo específico. Você pode facilmente limitar os pacotes capturados a este host usando o IP do host ou o NOME DO HOST. Por exemplo, capturar todos os pacotes trocados com example.com e os salvamos em http.pcap. É importante observar que a captura de pacotes requer que você esteja logado como root ou use o comando sudo.
Se quiser limitar os pacotes àqueles de um endereço IP de origem ou nome de host específico, você deve usar src host IP ou src host HOSTNAME. Da mesma forma, você pode limitar os pacotes àqueles enviados para um destino específico usando dst host IP ou dst host HOSTNAME.

## Filtrando por Porta
Se desejar capturar todo o tráfego DNS, você pode limitar os pacotes capturados àqueles na porta 53. Lembre-se de que o DNS usa as portas UDP e TCP 53 por padrão. No exemplo a seguir, podemos ver todas as consultas DNS lidas pela nossa placa de rede. O terminal abaixo mostra duas consultas DNS: a primeira consulta solicita o endereço IPv4 usado por example.org, enquanto a segunda solicita o endereço IPv6 associado a example.org.

## Filtragem por Protocolo
O último tipo de filtragem que abordaremos é a filtragem por protocolo. Você pode limitar a captura de pacotes a um protocolo específico; exemplos incluem: ip, ip6, udp, tcp e icmp. 

## Operadores Lógicos
Três operadores lógicos que podem ser úteis:

* and: Captura pacotes onde ambas as condições são verdadeiras. Por exemplo, ```tcpdump host 1.1.1.1 and tcp``` captura tráfego tcp com o host 1.1.1.1.
* or: Captura pacotes quando qualquer uma das condições é verdadeira. Por exemplo, ```tcpdump udp or icmp``` captura tráfego UDP ou ICMP.
* not: Captura pacotes quando a condição não é verdadeira. Por exemplo, ```tcpdump not tcp``` captura todos os pacotes, exceto segmentos TCP; esperamos encontrar pacotes UDP, ICMP e ARP entre os resultados.

## Cheat Sheet
* tcpdump host IP or tcpdump host HOSTNAME:	Filtra pacotes por IP ou hostname
* tcpdump src host IP or: Filtra pacotes de um host origem
* tcpdump dst host IP:	Filtra pacotes de um host destino
* tcpdump port PORTA:	Filtra pacotes por uma porta
* tcpdump src port PORTA:	Filtra pacotes por uma porta de origem
* tcpdump dst port PORTA:	Filtra pacotes por uma porta de destino
* tcpdump PROTOCOLO:	Filtra pacotes por protocolo

## Exemplos
```tcpdump -i any tcp port 22``` escuta em todas as interfaces e captura pacotes tcp de ou para a porta 22, ou seja, tráfego SSH.
```tcpdump -i wlo1 udp port 123``` escuta na placa de rede Wi-Fi e filtra o tráfego udp para a porta 123, o Protocolo de Tempo de Rede (NTP).
```tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap``` escutará na eth0, a interface Ethernet com fio, e filtrará o tráfego trocado com example.com que usa tcp e a porta 443. Em outras palavras, este comando está filtrando o tráfego HTTPS relacionado a example.com.

## Exercícios de fortalecimento de conhecimento
* P: Quantos pacotes em traffic.pcap usam o protocolo ICMP?
* R: 26

```Utilizei o comando tcpdump icmp -r traffic.pcap```

* P: Qual é o endereço IP do host que solicitou o endereço MAC 192.168.124.137?
* R: 192.168.124.148

```Utilizei um ARP, pelo comando tcpdump arp -r traffic.pcap```

* P: Qual nome de host (subdomínio) aparece na primeira consulta DNS?
* R: mirrors.rockylinux.org

```
Utilizei a busca do DNS pela porta padrão (53).
O comando utilizado foi tcpdump -r traffic.pcap port 53
```







