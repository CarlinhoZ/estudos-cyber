# [HTTP e HTTPS](/redes/portas.md)
HTTP é o protocolo usado sempre que você acessa um site, desenvolvido por Tim Berners-Lee e sua equipe entre 1989 e 1991. HTTP é o conjunto de regras usado para comunicação com servidores web para a transmissão de dados de páginas web, sejam eles HTML, imagens, vídeos, etc.

HTTPS é a versão segura do HTTP. Os dados HTTPS são criptografados, o que não apenas impede que as pessoas vejam os dados que você está recebendo e enviando, mas também garante que você está se comunicando com o servidor web correto e não com algo que o esteja imitando. HTTPS significa Hypertext Transfer Protocol Secure. É basicamente HTTP sobre TLS.

Ao acessar um site, seu navegador precisa fazer solicitações a um servidor web para obter recursos como HTML e imagens, além de baixar as respostas. Antes disso, você precisa informar ao navegador especificamente como e onde acessar esses recursos. É aqui que as URLs ajudam.

# O que é uma URL?
Uma URL é, em grande parte, uma instrução sobre como acessar um recurso na internet. Ela é dividida em alguns segmentos (nem todo site utiliza todos esses segmentos).
Por exemplo na URL: http://user:password@tryhackme.com:80/view-room?id=1#task3

* **Schema:** Instrui sobre qual protocolo usar para acessar o recurso, como HTTP, HTTPS, FTP. Nesse caso é o http

* **User:** Alguns serviços exigem autenticação para efetuar login; você pode inserir um nome de usuário e uma senha na URL para efetuar login.

* **Host:** O nome de domínio ou endereço IP do servidor que você deseja acessar. Nesse caso é o tryhackme

* **Port:** A porta à qual você se conectará, geralmente 80 para HTTP e 443 para HTTPS, mas pode ser hospedada em qualquer porta entre 1 e 65535.

* **Path:** O nome do arquivo ou local do recurso que você está tentando acessar. Determinado ali por view-room

* **Query String:** Bits extras de informação que podem ser enviados para o caminho solicitado. Por exemplo, /blog?id=1 informaria ao caminho do blog que você deseja receber o artigo do blog com o ID 1.

* **Fragment:** Esta é uma referência a um local na página solicitada. Isso é comumente usado para páginas com conteúdo longo e pode ter uma determinada parte da página diretamente vinculada a ela, para que fique visível ao usuário assim que ele acessa a página. No caso é o #task3

## Fazendo uma Solicitação
É possível fazer uma solicitação a um servidor web com apenas uma linha GET / HTTP/1.1
Mas, para uma experiência web muito mais rica, também será necessário enviar outros dados. Esses outros dados são enviados nos chamados cabeçalhos, onde os cabeçalhos contêm informações extras para fornecer ao servidor web com o qual você está se comunicando.

**Exemplo de solicitação**

GET / HTTP/1.1

Host: tryhackme.com

User-Agent: Mozilla/5.0 Firefox/87.0

Referer: https://tryhackme.com/

Para detalhar cada linha desta solicitação:

Linha 1: Esta solicitação envia o método GET, solicita a página inicial com / e informa ao servidor web que estamos usando o protocolo HTTP versão 1.1.

Linha 2: Informamos ao servidor web que queremos o site tryhackme.com

Linha 3: Informamos ao servidor web que estamos usando o navegador Firefox versão 87

Linha 4: Informamos ao servidor web que a página que nos encaminhou para esta é https://tryhackme.com

Linha 5: As solicitações HTTP sempre terminam com uma linha em branco para informar ao servidor web que a solicitação foi concluída.

**Exemplo de resposta**

HTTP/1.1 200 OK

Servidor: nginx/1.15.8

Data: Sex, 09 de Abr de 2021 13:34:03 GMT

Tipo de conteúdo: text/html

Tamanho do conteúdo: 98

<html>
  
<head>
  
<title>TryHackMe</title>

</head>

<body>
  
Bem-vindo ao TryHackMe.com
</body>

</html>

Para detalhar cada linha da resposta:

Linha 1: HTTP 1.1 é a versão do protocolo HTTP que o servidor está usando, seguida pelo Código de Status HTTP, neste caso "200 OK", que indica que a solicitação foi concluída com sucesso.

Linha 2: Informa o software do servidor web e o número da versão.

Linha 3: A data, a hora e o fuso horário atuais do servidor web.

Linha 4: O cabeçalho Content-Type informa ao cliente que tipo de informação será enviada, como HTML, imagens, vídeos, PDF, XML.

Linha 5: Content-Length informa ao cliente o tamanho da resposta, para que possamos confirmar se não há dados faltando.

Linha 6: A resposta HTTP contém uma linha em branco para confirmar o término da resposta HTTP.

Linhas 7 a 14: As informações solicitadas, neste caso, a página inicial.

## Métodos de requisição
Métodos HTTP são uma forma de o cliente indicar a ação pretendida ao fazer uma solicitação HTTP.

Requisição GET

Usada para obter informações de um servidor web.

Requisição POST

Usada para enviar dados ao servidor web e, potencialmente, criar novos registros.

Requisição PUT

Usada para enviar dados a um servidor web para atualizar informações.

Requisição DELETE

Usada para excluir informações/registros de um servidor web.

## Códigos de Status HTTP

Quando um servidor HTTP responde, a primeira linha sempre contém um código de status informando o cliente sobre o resultado da solicitação e também, potencialmente, como lidar com ela. Esses códigos de status podem ser divididos em 5 intervalos diferentes:

* 100-199 - Resposta de Informação: São enviados para informar ao cliente que a primeira parte da solicitação foi aceita e que ele deve continuar enviando o restante. Esses códigos não são mais muito comuns.
* 200-299 - Sucesso: Este intervalo de códigos de status é usado para informar ao cliente que sua solicitação foi bem-sucedida.
* 300-399 - Redirecionamento: São usados para redirecionar a solicitação do cliente para outro recurso. Isso pode ser para uma página da web diferente ou para um site completamente diferente.
* 400-499 - Erros do Cliente: Usados para informar ao cliente que houve um erro na solicitação.
* 500-599 - Erros de Servidor: Isso é reservado para erros que ocorrem no lado do servidor e geralmente indicam um problema sério com o servidor que está processando a solicitação.

**Códigos de Status HTTP Comuns:**

Existem muitos códigos de status HTTP diferentes, sem contar que os aplicativos podem definir os seus próprios.

* 200 - OK. A solicitação foi concluída com sucesso.
* 201 - Criado. Um recurso foi criado (por exemplo, um novo usuário ou uma nova postagem de blog).
* 301 - Movido Permanentemente: Isso redireciona o navegador do cliente para uma nova página da web ou informa aos mecanismos de busca que a página foi movida para outro lugar e que eles devem procurá-la.
* 302 - Encontrado: Semelhante ao redirecionamento permanente acima, mas, como o nome sugere, essa é apenas uma alteração temporária e pode mudar novamente em um futuro próximo.
* 400 - Solicitação Inválida: Isso informa ao navegador que algo estava errado ou faltando na solicitação. Isso pode ser usado às vezes se o recurso do servidor web solicitado esperar um determinado parâmetro que o cliente não enviou.
* 401 - Não Autorizado. No momento, você não tem permissão para visualizar este recurso até que tenha autorização no aplicativo web, geralmente com um nome de usuário e senha.
* 403 - Proibido. Você não tem permissão para visualizar este recurso, esteja você logado ou não.
* 405 - Método Não Permitido. O recurso não permite esta solicitação de método; por exemplo, você envia uma solicitação GET para o recurso /create-account quando ele esperava uma solicitação POST.
* 404 - Página Não Encontrada. A página/recurso solicitado não existe.
* 500 - Erro Interno de Serviço. O servidor encontrou algum tipo de erro com sua solicitação que ele não sabe como tratar corretamente.
* 503 - Serviço Indisponível.

## Headers
Headers são bits de dados adicionais que você pode enviar ao servidor web ao fazer solicitações.

Embora nenhum header seja estritamente necessário ao fazer uma solicitação HTTP, você terá dificuldade para visualizar um site corretamente.

**Headers de Solicitação Comuns**

Estes são headers enviados do cliente (geralmente seu navegador) para o servidor.

* Host: Alguns servidores web hospedam vários sites, portanto, ao fornecer os headers de host, você pode informar qual deles precisa; caso contrário, receberá apenas o site padrão do servidor.

* User-Agent: Este é o software e o número da versão do seu navegador, informando ao servidor web que o software do seu navegador o ajuda a formatar o site corretamente para o seu navegador e que alguns elementos de HTML, JavaScript e CSS estão disponíveis apenas em determinados navegadores.

* Content-Length: Ao enviar dados para um servidor web, como em um formulário, o comprimento do conteúdo informa ao servidor web a quantidade de dados que ele deve esperar na solicitação. Dessa forma, o servidor pode garantir que não haja perda de dados.

* Accept-Encoding: Informa ao servidor web quais tipos de métodos de compactação o navegador suporta para que os dados possam ser reduzidos para transmissão pela internet.

* Cookie: Dados enviados ao servidor para ajudar a lembrar suas informações.

**Headers de Resposta Comuns**

Estes são os headers que são retornados ao cliente pelo servidor após uma solicitação.

* Set-Cookie: Informações a serem armazenadas e enviadas de volta ao servidor web em cada solicitação.

* Cache-Control: Por quanto tempo o conteúdo da resposta deve ser armazenado no cache do navegador antes de ser solicitado novamente.

* Content-Type: Informa ao cliente qual tipo de dado está sendo retornado, ou seja, HTML, CSS, JavaScript, Imagens, PDF, Vídeo, etc. Usando o cabeçalho "content-type", o navegador sabe como processar os dados.

* Content-Encoding: Qual método foi usado para compactar os dados e torná-los menores ao enviá-los pela internet.

## Cookies
Cookies são pequenos pedaços de dados armazenados no computador. Os cookies são salvos quando você recebe um cabeçalho "Set-Cookie" de um servidor web. A cada nova solicitação, você envia os dados do cookie de volta ao servidor web. Como o HTTP não tem estado (não rastreia suas solicitações anteriores), os cookies podem ser usados para lembrar ao servidor web quem você é, algumas configurações pessoais do site ou se você já acessou o site anteriormente.
Os cookies podem ser usados para diversas finalidades, mas são mais comumente usados para autenticação em sites. O valor do cookie geralmente não é uma sequência de texto simples onde você pode ver a senha, mas um token (código secreto exclusivo que não é facilmente adivinhado por humanos).

**Visualizando seus cookies**

É possível visualizar facilmente quais cookies seu navegador está enviando para um site usando as ferramentas do desenvolvedor em seu navegador. Se não tiver certeza de como acessar as ferramentas do desenvolvedor em seu navegador, clique no botão "Visualizar site" na parte superior desta tarefa para obter um guia prático.
Depois de abrir as ferramentas do desenvolvedor, clique na aba "Rede". Essa aba mostrará uma lista de todos os recursos solicitados pelo seu navegador. Pode clicar em cada um para receber uma análise detalhada da solicitação e da resposta. Se o seu navegador enviou um cookie, você os verá na aba "Cookies" da solicitação.

# [FTP (File Transfer Protocol)](/redes/portas.md)
O Protocolo de Transferência de Arquivos (FTP) é um protocolo projetado para auxiliar na transferência eficiente de arquivos entre sistemas diferentes e até mesmo incompatíveis. Ele suporta dois modos de transferência de arquivos: binário e ASCII (texto).

Exemplos de comandos definidos pelo protocolo FTP:

* USER é usado para inserir o nome de usuário
* PASS é usado para inserir a senha
* RETR (recuperar) é usado para baixar um arquivo do servidor FTP para o cliente.
* STOR (armazenar) é usado para enviar um arquivo do cliente para o servidor FTP.
O servidor FTP escuta na porta TCP 21 por padrão; a transferência de dados é realizada por meio de outra conexão do cliente para o servidor.

# [SMTP (Simple Mail Transfer Protocol)](/redes/portas.md)
A analogia com o protocolo SMTP é quando você vai aos correios locais para enviar um pacote. Você cumprimenta o funcionário, informa para onde deseja enviar o pacote e fornece as informações do remetente antes de entregá-lo. Dependendo do país em que você estiver, poderá ser solicitado a mostrar seu documento de identidade. Este processo não é muito diferente de uma sessão SMTP.

Vamos apresentar alguns dos comandos usados pelo seu cliente de e-mail ao transferir um e-mail para um servidor SMTP:

* HELO ou EHLO inicia uma sessão SMTP
* MAIL FROM especifica o endereço de e-mail do remetente
* RCPT TO especifica o endereço de e-mail do destinatário
* DATA indica que o cliente começará a enviar o conteúdo da mensagem de e-mail
* . é enviado em uma linha isoladamente para indicar o fim da mensagem de e-mail

# [POP3 (Post Office Protocol 3)](/redes/portas.md)
Você recebeu um e-mail e deseja baixá-lo para o seu cliente de e-mail local. O POP3 foi projetado para permitir que o cliente se comunique com um servidor de e-mail e recupere mensagens de e-mail.

Por exemplo, um cliente de e-mail envia suas mensagens usando SMTP e as recupera usando POP3. SMTP é semelhante a entregar seu envelope ou pacote aos correios, e POP3 é semelhante a verificar sua caixa de correio local em busca de novas cartas ou pacotes.

Alguns comandos POP3 comuns são:

* USER <nome de usuário> identifica o usuário
* PASS <senha> fornece a senha do usuário
* STAT solicita o número de mensagens e o tamanho total
* LIST lista todas as mensagens e seus tamanhos
* RETR <número_da_mensagem> recupera a mensagem especificada
* DELE <número_da_mensagem> marca uma mensagem para exclusão
* QUIT encerra a sessão POP3 aplicando alterações, como exclusões

# [IMAP (Internet Message Access Protocol)](/redes/portas.md)
O POP3 é suficiente para trabalhar em um único dispositivo, por exemplo, seu cliente de e-mail favorito no seu computador desktop. No entanto, e se você quiser verificar seus e-mails no computador desktop do escritório e também no seu laptop ou smartphone? Nesse cenário, você precisa de um protocolo que permita a sincronização de mensagens em vez de excluí-las após recuperá-las. Uma solução para manter uma caixa de correio sincronizada em vários dispositivos é o Internet Message Access Protocol (IMAP).

O IMAP permite a sincronização de mensagens lidas, movidas e excluídas. O IMAP é bastante conveniente quando você verifica seus e-mails em vários clientes. Ao contrário do POP3, que tende a minimizar o armazenamento do servidor, pois os e-mails são baixados e excluídos do servidor remoto, o IMAP tende a usar mais espaço, pois os e-mails são mantidos no servidor e sincronizados entre os clientes de e-mail.

Os comandos do protocolo IMAP são mais complexos do que os comandos do protocolo POP3. Listamos alguns exemplos abaixo:

* LOGIN <nome_de_usuário> <senha> autentica o usuário
* SELECT <caixa_de_correio> seleciona a pasta da caixa de correio com a qual trabalhar
* FETCH <número_de_correio> <nome_do_item_de_dados> Exemplo: fetch 3 body[] para buscar a mensagem número 3, o cabeçalho e o corpo.
* MOVE <conjunto_de_sequências> <caixa_de_correio> move as mensagens especificadas para outra caixa de correio
* COPY <conjunto_de_sequências> <nome_do_item_de_dados> copia as mensagens especificadas para outra caixa de correio
* LOGOUT desconecta

# TLS (Transfer Layer Protocol)
Assim como o SSL, seu antecessor, o TLS é um protocolo criptográfico que opera na camada de transporte do modelo OSI. Ele permite a comunicação segura entre um cliente e um servidor em uma rede insegura. Por segurança, referimo-nos à confidencialidade e à integridade; o TLS garante que ninguém possa ler ou modificar os dados trocados. Sem o TLS, não poderíamos usar a internet para muitas aplicações que agora fazem parte da nossa rotina diária.

Hoje em dia, dezenas de protocolos receberam atualizações de segurança com a simples adição do TLS. Exemplos incluem HTTP, DNS, MQTT e SIP, que se tornaram HTTPS, DoT (DNS sobre TLS), MQTTS e SIPS, onde o "S" anexado significa Seguro devido ao uso de SSL/TLS.

O primeiro passo para cada servidor (ou cliente) que precisa se identificar é obter um certificado TLS assinado. Geralmente, o administrador do servidor cria uma Solicitação de Assinatura de Certificado (CSR) e a envia a uma Autoridade Certificadora (AC); a AC verifica a CSR e emite um certificado digital. Uma vez recebido o certificado (assinado), ele pode ser usado para identificar o servidor (ou o cliente) para outros, que podem confirmar a validade da assinatura. Para que um host confirme a validade de um certificado assinado, os certificados das autoridades de assinatura precisam estar instalados no host. No mundo não digital, isso é semelhante a reconhecer os carimbos de várias autoridades. Existe um site para criar um certificado assinado totalmente gratuito chamado [Let's Encrypt](https://letsencrypt.org/).

# SSH (Secure Shell)
Embora seja muito conveniente efetuar login e administrar sistemas remotos utilizando telnet, é arriscado quando todo o tráfego é enviado em texto não criptografado. É fácil para qualquer pessoa que monitore o tráfego de rede obter suas credenciais de login depois de usar o telnet. Esse problema precisava de uma solução. Tatu Ylönen desenvolveu o protocolo Secure Shell (SSH) e lançou o SSH-1 em 1995 como freeware.

O OpenSSH oferece vários benefícios. Listaremos alguns pontos-chave:

* Autenticação segura: Além da autenticação baseada em senha, o SSH suporta chave pública e autenticação de dois fatores.
* Confidencialidade: O OpenSSH fornece criptografia de ponta a ponta, protegendo contra espionagem. Além disso, ele notifica você sobre novas chaves de servidor para proteção contra ataques do tipo "man-in-the-middle".
* Integridade: Além de proteger a confidencialidade dos dados trocados, a criptografia também protege a integridade do tráfego.
* Tunelamento: O SSH pode criar um "túnel" seguro para rotear outros protocolos através do SSH. Essa configuração leva a uma conexão semelhante a uma VPN.
* Encaminhamento X11: Se você se conectar a um sistema do tipo Unix com uma interface gráfica de usuário, o SSH permite que você use o aplicativo gráfico pela rede.

Você deve executar o comando ssh username@hostname para se conectar a um servidor SSH. Se o nome de usuário for o mesmo que o seu nome de usuário logado, você precisará apenas do ssh hostname. Em seguida, será solicitada uma senha; no entanto, se a autenticação por chave pública for usada, você será logado imediatamente.

# SFTP e FTPS
SFTP (SSH File Transfer Protocol) e permite a transferência segura de arquivos. Faz parte do conjunto de protocolos SSH e compartilha a mesma porta, 22. Se habilitado na configuração do servidor OpenSSH, você pode se conectar usando um comando como ```sftp username@hostname```. Após o login, você pode executar comandos como ```get filename``` e ```put filename``` para baixar e enviar arquivos, respectivamente. De modo geral, os comandos SFTP são do tipo Unix e podem diferir dos comandos FTP.

SFTP não deve ser confundido com FTPS. FTPS (File Transfer Protocol Secure) é protegido usando TLS, assim como HTTPS. Enquanto o FTP usa a porta 21, o FTPS geralmente usa a porta 990. Ele requer configuração de certificado e pode ser complicado de permitir em firewalls rigorosos, pois usa conexões separadas para controle e transferência de dados.

Configurar um servidor SFTP é tão fácil quanto habilitar uma opção no servidor OpenSSH. Assim como HTTPS, SMTPS, POP3S, IMAPS e outros protocolos que dependem do TLS para segurança, o FTPS requer um certificado TLS adequado para ser executado com segurança.














