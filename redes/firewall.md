# Firewall

Um firewall é um dispositivo dentro de uma rede responsável por determinar qual tráfego tem permissão para entrar e sair. Pense em um firewall como a segurança de fronteira de uma rede. Um administrador pode configurar um firewall para permitir ou negar a entrada ou saída de tráfego de uma rede com base em vários fatores, como:

* De onde vem o tráfego? (o firewall foi instruído a aceitar/negar tráfego de uma rede específica?)
* Para onde o tráfego está indo? (o firewall foi instruído a aceitar/negar tráfego destinado a uma rede específica?)
* Para qual porta o tráfego se destina? (o firewall foi instruído a aceitar/negar tráfego destinado apenas à porta 80?)
* Qual protocolo o tráfego está usando? (o firewall foi instruído a aceitar/negar tráfego UDP, TCP ou ambos?)

Os firewalls realizam a inspeção de pacotes para determinar as respostas a essas perguntas.

Firewalls vêm em todos os formatos e tamanhos. De peças de hardware dedicadas que podem lidar com uma grande quantidade de dados a roteadores residenciais ou softwares como o Snort, os firewalls podem ser categorizados em 2 a 5 categorias. O firewall atua na camada de rede e transporte.

As duas principais categorias de firewall são:

* **Com estado**
Este tipo de firewall utiliza todas as informações de uma conexão; em vez de inspecionar um pacote individual, este firewall determina o comportamento de um dispositivo com base em toda a conexão.
Este tipo de firewall consome muitos recursos em comparação com firewalls sem estado, pois a tomada de decisão é dinâmica. Por exemplo, um firewall pode permitir as primeiras partes de um handshake TCP que posteriormente falhariam.
Se uma conexão de um host for ruim, ele bloqueará todo o dispositivo.

* **Sem Estado**
Este tipo de firewall utiliza um conjunto estático de regras para determinar se pacotes individuais são aceitáveis ou não. Por exemplo, o envio de um pacote inválido por um dispositivo não significa necessariamente que todo o dispositivo seja bloqueado.
Embora esses firewalls utilizem muito menos recursos do que as alternativas, eles são muito mais "burros". Por exemplo, esses firewalls são eficazes apenas conforme as regras definidas neles. Se uma regra não for exatamente correspondida, ela é efetivamente inútil.
No entanto, esses firewalls são ótimos para receber grandes volumes de tráfego de um conjunto de hosts (como em um ataque de DDOS).
