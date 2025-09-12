# Modos de operação
## NAT
* Interfaces possuem endereço IP
* Pacotes são roteados por IP
* Possui uma configuração para VDOM que quebra o firewall em duas partes, onde pode trabalhar uma parte em NAT e outra em Transparent
* Fortigate funciona como roteador, na camada OSI n° 3

## Transparent (Bridge)
* Interface sem endereços de IP
* Pacotes são apenas enviados ou bloqueados
* Possui uma configuração para VDOM, igual ao modo NAT
* Fortigate funciona como switch ou bridge, na camada OSI n° 2, não haverá roteamento, mas ainda abrirá o pacote para análise

# Configurações de fábrica
* IP: 192.168.1.99/24
* Interface MGMT em modelos high-end e mid-range
* Interface Port 1 ou Internal em modelos de entrada
* DHCP habilitado nas portas (MGMT ou Port 1)
* PING, SSH E HTTPS habilitados
* Pode ser acessado via CLI
* Usuário e senha default (admin, sem senha)

# Políticas de firewall
## Firewall Policy
* Regra comum para navegação interna, utiliza os perfils de segurança para gerenciar os aplicativos e websites permitidos.

## Multicast Policy

## Local in Policy
* tráfego interno, permitir o que o firewall pode ou não fazer, por exemplo um ping

## IPv4 DoS Policy
* configura métricas de quanto TCP SYN você pode receber, ICMP Flood












