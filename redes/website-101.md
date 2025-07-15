# Funcionamento de Website
Quando você visita um site, seu navegador (como Safari ou Google Chrome) faz uma solicitação a um servidor web solicitando informações sobre a página que você está visitando. Ele responderá com dados que seu navegador usa para mostrar a página; um servidor web é apenas um computador dedicado, em algum outro lugar do mundo, que processa suas solicitações.

Existem dois componentes principais que compõem um site:

* Front-end (lado do cliente) - a maneira como seu navegador renderiza um site.
* Back-end (lado do servidor) - um servidor que processa sua solicitação e retorna uma resposta.

## Construção de um Website

* HTML, para construir sites e definir sua estrutura
* CSS, para tornar os sites mais atraentes adicionando opções de estilo
* JavaScript, para implementar recursos complexos nas páginas usando interatividade

### HTML

O HyperText Markup Language (HTML) é a linguagem em que os sites são escritos. Os elementos (também conhecidos como tags) são os blocos de construção das páginas HTML e informam ao navegador como exibir o conteúdo. O trecho de código abaixo mostra um documento HTML simples, cuja estrutura é a mesma para todos os sites:

```
<!DOCTYPE html>
<html>
<head>
<title>Title of the document</title>
</head>
<body>
The content of the document......
</body>
</html>

```

A estrutura HTML possui os seguintes componentes:

* O elemento <!DOCTYPE html> define que a página é um documento HTML5. Isso ajuda na padronização entre diferentes navegadores e informa ao navegador para usar HTML5 para interpretar a página.
* O elemento <html> é o elemento raiz da página HTML - todos os outros elementos vêm depois deste elemento.
* O elemento <head> contém informações sobre a página (como o título da página).
* O elemento <body> define o corpo do documento HTML; somente o conteúdo dentro do corpo é exibido no navegador.

```
Existem muitos outros elementos (tags) usados para diferentes propósitos. Por exemplo, existem tags para botões (<button>), imagens (<img>), listas e muito mais.
As tags podem conter atributos como o atributo class, que pode ser usado para estilizar um elemento (por exemplo, definir uma cor diferente para a tag) <p class="bold-text">, ou o atributo src, que é usado em imagens para especificar a localização de uma imagem: <img src="img/cat.jpg">. Um elemento pode ter vários atributos, cada um com sua própria finalidade exclusiva, por exemplo, <p attribute1="value1" attribute2="value2">.
```

```
Os elementos também podem ter um atributo id (<p id="example">), que é exclusivo para o elemento. Ao contrário do atributo class, em que vários elementos podem usar a mesma classe, um elemento deve ter IDs diferentes para ser identificado de forma única. Os IDs dos elementos são usados para estilização e para identificá-lo por JavaScript.
Você pode visualizar o HTML de qualquer site clicando com o botão direito do mouse e selecionando "Exibir código-fonte da página" (Chrome).
```

### JavaScript
JavaScript (JS) é uma das linguagens de programação mais populares do mundo e permite que as páginas se tornem interativas. O HTML é usado para criar a estrutura e o conteúdo do site, enquanto o JavaScript é usado para controlar a funcionalidade das páginas web — sem JavaScript, uma página não teria elementos interativos e seria sempre estática.
O JavaScript pode atualizar a página dinamicamente em tempo real, oferecendo a funcionalidade de alterar o estilo de um botão quando um evento específico ocorre na página (como quando um usuário clica em um botão) ou de exibir animações em movimento.

```
O JavaScript é adicionado ao código-fonte da página e pode ser carregado dentro das tags <script> ou incluído remotamente com o atributo src: <script src="/location/of/javascript_file.js"></script>
O código JavaScript a seguir encontra um elemento HTML na página com o ID "demo" e altera o conteúdo do elemento para "Hack the Planet":
```

```
document.getElementById("demo").innerHTML = "Hack the Planet";
```

Elementos HTML também podem ter eventos, como "onclick" ou "onhover", que executam JavaScript quando o evento ocorre. O código a seguir altera o texto do elemento com o ID de demonstração para Botão Clicado:

```
<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>
```

Eventos onclick também podem ser definidos dentro das tags de script JavaScript, e não diretamente nos elementos.






