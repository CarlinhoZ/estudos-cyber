# Web Server

## O que é um servidor web?
Um servidor web é um software que monitora conexões de entrada e utiliza o protocolo HTTP para entregar conteúdo web aos seus clientes. Os softwares de servidor web mais comuns que você encontrará são Apache, Nginx, IIS e NodeJS. Um servidor web entrega arquivos do que é chamado de diretório raiz, definido nas configurações do software. Por exemplo, Nginx e Apache compartilham o mesmo local padrão, /var/www/html, em sistemas operacionais Linux, e o IIS usa C:\inetpub\wwwroot para sistemas operacionais Windows. Assim, por exemplo, se você solicitasse o arquivo http://www.example.com/picture.jpg, ele enviaria o arquivo /var/www/html/picture.jpg de seu disco rígido local.

## Hosts Virtuais
Servidores web podem hospedar vários sites com nomes de domínio diferentes; para isso, eles usam hosts virtuais. O software do servidor web verifica o nome do host solicitado nos cabeçalhos HTTP e o compara com seus hosts virtuais (hosts virtuais são apenas arquivos de configuração baseados em texto). Se encontrar uma correspondência, o site correto será fornecido. Se nenhuma correspondência for encontrada, o site padrão será fornecido.

Hosts virtuais podem ter seu diretório raiz mapeado para diferentes locais no disco rígido. Por exemplo, one.com sendo mapeado para /var/www/website_one, e two.com sendo mapeado para /var/www/website_two.
Não há limite para o número de sites diferentes que você pode hospedar em um servidor web.

## Conteúdo Estático vs. Dinâmico

Conteúdo estático, como o nome sugere, é aquele que nunca muda. Exemplos comuns disso são imagens, JavaScript, CSS, etc., mas também pode incluir HTML que nunca muda. Além disso, são arquivos que são servidos diretamente do servidor web sem nenhuma alteração.

Conteúdo dinâmico, por outro lado, é aquele que pode mudar com diferentes solicitações. Considere, por exemplo, um blog. Na página inicial do blog, serão exibidas as entradas mais recentes. Se uma nova entrada for criada, a página inicial será atualizada com a entrada mais recente, ou um segundo exemplo pode ser uma página de busca em um blog. Dependendo da palavra que você pesquisar, resultados diferentes serão exibidos.

Essas alterações são feitas no que é chamado de Backend, com o uso de linguagens de programação e script. É chamado de Backend porque tudo o que está sendo feito é feito nos bastidores. Você não pode visualizar o código-fonte HTML dos sites e ver o que está acontecendo no Backend, enquanto o HTML é o resultado do processamento do Backend. Tudo o que você vê no seu navegador é chamado de Frontend.

## Linguagens de Script e Backend

Não há limites para o que uma linguagem de backend pode alcançar, e são elas que tornam um site interativo para o usuário. Alguns exemplos dessas linguagens são PHP, Python, Ruby, NodeJS, Perl e muitas outras. Essas linguagens podem interagir com bancos de dados, chamar serviços externos, processar dados do usuário e muito mais. Um exemplo básico disso em PHP seria se você solicitasse o site http://example.com/index.php?name=adam

Se index.php fosse construído assim:
```
<html><body>Olá <?php echo $_GET["nome"]; ?></body></html>
```
A saída seria a seguinte para o cliente:
```
<html><body>Olá adam</body></html>
```
Você notará que o cliente não vê nenhum código PHP porque está no Backend. Essa interatividade abre muito mais problemas de segurança para aplicativos web que não foram criados com segurança.
