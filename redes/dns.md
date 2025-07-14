# DNS
O Domain Name System (DNS) é o protocolo responsável por resolver nomes de host, como google.com, para seus respectivos endereços IP.
O DNS oferece uma maneira simples de nos comunicarmos com dispositivos na internet sem precisar nos lembrar de números complexos. Assim como cada casa tem um endereço único para enviar encomendas diretamente para ela, cada computador na internet tem seu próprio endereço único para se comunicar com ele, chamado de endereço IP. Um endereço IP se parece com o seguinte: 172.217.28.174, composto por 4 conjuntos de dígitos variando de 0 a 255, separados por um ponto final. Quando você deseja visitar um site, não é exatamente conveniente lembrar desse conjunto complexo de números, e é aí que o DNS pode ajudar. Então, em vez de se lembrar de 172.217.28.174, você pode se lembrar de tryhackme.com.

# Hierarquia de Domínio
## TLD (Top-Level Domain)

Um TLD é a parte mais à direita de um nome de domínio. Por exemplo, o TLD google.com é .com. Existem dois tipos de TLD: gTLD (Generic Top Level) e ccTLD (Country Code Top Level Domain). Historicamente, um gTLD tinha como objetivo informar ao usuário a finalidade do nome de domínio; por exemplo, um .com seria para fins comerciais, .org para uma organização, .edu para educação e .gov para governo. E um ccTLD era usado para fins geográficos, por exemplo, .ca para sites localizados no Canadá, .co.uk para sites localizados no Reino Unido e assim por diante. Devido a essa demanda, há um fluxo de novos gTLDs, que variam de .online, .club, .website, .biz e muitos outros.

## Second-Level Domain

Tomando google.com como exemplo, a parte .com é o TLD, e tryhackme é o Domínio de Segundo Nível. Ao registrar um nome de domínio, o domínio de segundo nível é limitado a 63 caracteres + o TLD e pode usar apenas a-z 0-9 e hifens (não pode começar ou terminar com hifens ou ter hifens consecutivos).

## Subdomain

Um subdomínio fica à esquerda do Domínio de Segundo Nível, usando um ponto para separá-lo; por exemplo, no nome admin.google.com, a parte admin é o subdomínio. Um nome de subdomínio tem as mesmas restrições de criação que um Second-Level Domain, sendo limitado a 63 caracteres e pode usar apenas a-z 0-9 e hifens (não pode começar ou terminar com hifens ou ter hifens consecutivos). Você pode usar vários subdomínios separados por pontos para criar nomes mais longos, como jupiter.servers.tryhackme.com. Mas o comprimento deve ser limitado a 253 caracteres ou menos. Não há limite para o número de subdomínios que você pode criar para o seu nome de domínio.

# Registros DNS
O DNS não serve apenas para sites, e existem vários tipos de registro DNS.

Registro A

Esses registros resolvem para endereços IPv4, por exemplo, 104.26.10.229

Registro AAAA

Esses registros resolvem para endereços IPv6, por exemplo, 2606:4700:20::681a:be5

Registro CNAME

Esses registros resolvem para outro nome de domínio, por exemplo, a loja online TryHackMe tem o nome de subdomínio store.tryhackme.com, que retorna um registro CNAME shops.shopify.com. Outra solicitação DNS seria então feita para shops.shopify.com para calcular o endereço IP.

Registro MX

Esses registros resolvem para o endereço dos servidores que gerenciam o e-mail para o domínio que você está consultando; por exemplo, uma resposta de registro MX para tryhackme.com seria algo como alt1.aspmx.l.google.com. Esses registros também vêm com um sinalizador de prioridade. Isso informa ao cliente em que ordem testar os servidores, o que é perfeito caso o servidor principal caia e o e-mail precise ser enviado para um servidor de backup.

Registro TXT

Os registros TXT são campos de texto livre onde qualquer dado baseado em texto pode ser armazenado. Os registros TXT têm múltiplos usos, mas alguns comuns podem ser listar servidores que têm autoridade para enviar um e-mail em nome do domínio (isso pode ajudar no combate a spam e e-mails falsos). Eles também podem ser usados para verificar a propriedade do nome de domínio ao contratar serviços de terceiros.

# Como funciona uma requisição DNS?
1. Ao solicitar um nome de domínio, seu computador primeiro verifica o cache local para ver se você já pesquisou o endereço recentemente; caso contrário, será feita uma solicitação ao seu Servidor DNS Recursivo.

2. Um Servidor DNS Recursivo geralmente é fornecido pelo seu provedor de internet, mas você também pode escolher o seu. Este servidor também possui um cache local de nomes de domínio pesquisados recentemente. Se um resultado for encontrado localmente, ele é enviado de volta ao seu computador e sua solicitação termina aqui (isso é comum para serviços populares e muito solicitados, como Google, Facebook e Twitter). Se a solicitação não puder ser encontrada localmente, inicia-se uma jornada para encontrar a resposta correta, começando pelos servidores DNS raiz da internet.

3. Os servidores raiz atuam como a espinha dorsal do DNS da internet; sua função é redirecioná-lo para o TLD correto, dependendo da sua solicitação. Se, por exemplo, você solicitar www.tryhackme.com, o servidor raiz reconhecerá o TLD .com e o encaminhará para o servidor TLD correto que lida com endereços .com.

4. O servidor TLD armazena registros de onde encontrar o servidor autoritativo para responder à solicitação de DNS. O servidor autoritativo também é frequentemente conhecido como servidor de nomes do domínio. Por exemplo, o servidor de nomes para tryhackme.com é kip.ns.cloudflare.com e uma.ns.cloudflare.com. Você frequentemente encontrará vários servidores de nomes para um nome de domínio para atuar como backup caso um deles fique inativo.

5. Um servidor DNS autoritativo é o servidor responsável por armazenar os registros DNS de um nome de domínio específico e onde quaisquer atualizações nos registros DNS do seu nome de domínio seriam feitas. Dependendo do tipo de registro, o registro DNS é então enviado de volta ao Servidor DNS Recursivo, onde uma cópia local será armazenada em cache para solicitações futuras e, em seguida, retransmitida ao cliente original que fez a solicitação. Todos os registros DNS vêm com um valor TTL (Time To Live). Esse valor é um número representado em segundos pelos quais a resposta deve ser salva localmente até que você precise consultá-la novamente. O cache evita a necessidade de fazer uma solicitação de DNS toda vez que você se comunicar com um servidor.
