# O que é HTTP e HTTPS?
HTTP é o protocolo usado sempre que você acessa um site, desenvolvido por Tim Berners-Lee e sua equipe entre 1989 e 1991. HTTP é o conjunto de regras usado para comunicação com servidores web para a transmissão de dados de páginas web, sejam eles HTML, imagens, vídeos, etc.

HTTPS é a versão segura do HTTP. Os dados HTTPS são criptografados, o que não apenas impede que as pessoas vejam os dados que você está recebendo e enviando, mas também garante que você está se comunicando com o servidor web correto e não com algo que o esteja imitando.

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
