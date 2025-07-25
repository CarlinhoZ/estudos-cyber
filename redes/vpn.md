# VPN

Uma Virtual Private Network (VPN) é uma maneira de criar um "túnel" seguro entre duas redes. VPNs também são comumente usadas para que um funcionário faça login em seu local de trabalho quando não está no local (como trabalhando em casa ou viajando a trabalho). VPNs também são usadas onde as redes (como cafeterias) não oferecem criptografia e são uma ótima maneira de impedir que outras pessoas leiam o tráfego da sua rede.
Por exemplo, apenas dispositivos dentro da mesma rede (como dentro de uma empresa) podem se comunicar diretamente. No entanto, uma VPN permite que dois escritórios estejam conectados.

Quando a Internet foi projetada, o conjunto de protocolos TCP/IP se concentrava na entrega de pacotes. Por exemplo, se um roteador ficar fora de serviço, os protocolos de roteamento podem se adaptar e escolher uma rota diferente para enviar seus pacotes. Se um pacote não for reconhecido, o TCP possui mecanismos integrados para detectar essa situação e reenviá-lo. No entanto, não há mecanismos para garantir que todos os dados que entram ou saem de um computador estejam protegidos contra divulgação e alteração. Uma solução popular foi a configuração de uma conexão VPN.

Uma vez estabelecido um túnel VPN, todo o nosso tráfego de internet geralmente será roteado pela conexão VPN, ou seja, através do túnel VPN. Consequentemente, quando tentamos acessar um serviço de internet ou aplicativo web, eles não verão nosso endereço IP público, mas sim o do servidor VPN. É por isso que alguns usuários da internet se conectam via VPN para contornar restrições geográficas. Além disso, o ISP local verá apenas o tráfego criptografado, o que limita sua capacidade de censurar o acesso à internet.

Em outras palavras, se um usuário se conectar a um servidor VPN no Japão, ele aparecerá para os servidores que acessa como se estivesse localizado no Japão. Esses servidores personalizarão sua experiência de acordo, redirecionando-os, por exemplo, para a versão japonesa do serviço.

Por fim, embora em muitos cenários seja possível estabelecer uma conexão VPN para rotear todo o tráfego pelo túnel VPN, algumas conexões VPN não fazem isso. O servidor VPN pode estar configurado para fornecer acesso a uma rede privada, mas não para rotear seu tráfego. Além disso, alguns servidores VPN vazam seu endereço IP real, embora devam rotear todo o seu tráfego pela VPN. Dependendo do motivo pelo qual você está usando uma conexão VPN, pode ser necessário executar mais alguns testes, como um teste de vazamento de DNS.

## Benefícios da VPN

* Permite que redes em diferentes localizações geográficas sejam conectadas: Por exemplo, uma empresa com vários escritórios achará as VPNs benéficas, pois isso significa que recursos como servidores/infraestrutura podem ser acessados de outro escritório.

* Oferece privacidade: A tecnologia VPN utiliza criptografia para proteger os dados. Isso significa que eles só podem ser entendidos entre os dispositivos de onde foram enviados e para os quais se destinam, o que significa que os dados não são vulneráveis a sniffing.
Essa criptografia é útil em locais com Wi-Fi público, onde a rede não fornece criptografia. Você pode usar uma VPN para proteger seu tráfego de ser visualizado por outras pessoas.

* Oferece anonimato: Jornalistas e ativistas dependem de VPNs para cobrir com segurança questões globais em países onde a liberdade de expressão é controlada.
Normalmente, seu tráfego pode ser visualizado pelo seu provedor de internet e outros intermediários e, portanto, rastreado.
O nível de anonimato que uma VPN oferece depende da forma como outros dispositivos na rede respeitam a privacidade. Por exemplo, uma VPN que registra todos os seus dados/histórico é essencialmente o mesmo que não usar uma VPN nesse sentido.

A tecnologia VPN evoluiu ao longo dos anos. Algumas tecnologias VPN existentes abaixo:

* **PPP:** Esta tecnologia é usada pelo PPTP para permitir autenticação e fornecer criptografia de dados. VPNs funcionam usando uma chave privada e um certificado público (semelhante ao SSH). A chave privada e o certificado devem ser correspondentes para que você se conecte. Esta tecnologia não é capaz de sair de uma rede por si só (não roteável).

* **PPTP:** O Point-to-Point Tunneling Protocol (PPTP) é a tecnologia que permite que os dados do PPP trafeguem e saiam de uma rede.
O PPTP é muito fácil de configurar e é suportado pela maioria dos dispositivos. No entanto, sua criptografia é fraca em comparação com outras alternativas.

* **IPSec:** O Ínternet Protocol Security (IPsec) criptografa dados usando a estrutura existente do IP.
O IPSec é difícil de configurar em comparação com alternativas; no entanto, se for bem-sucedido, ele oferece criptografia forte e também é compatível com muitos dispositivos.
