# Funcionalidade do PowerShell
Em programação, um objeto representa um item com propriedades (características) e métodos (ações). Por exemplo, um objeto de carro pode ter propriedades como Cor, Modelo e Nível de Combustível, e métodos como Dirigir(), Buzinar() e Reabastecer().

Da mesma forma, no PowerShell, os objetos são unidades fundamentais que encapsulam dados e funcionalidades, facilitando o gerenciamento e a manipulação de informações. Um objeto no PowerShell pode conter nomes de arquivos, nomes de usuário ou tamanhos como dados (propriedades) e transportar funções (métodos), como copiar um arquivo ou interromper um processo.

Os comandos básicos do Shell de Comando tradicional são baseados em texto, o que significa que processam e geram dados como texto simples. Em vez disso, quando um cmdlet (pronuncia-se command-let) é executado no PowerShell, ele retorna objetos que mantêm suas propriedades e métodos. Isso permite uma manipulação de dados mais poderosa e flexível, já que esses objetos não exigem análise adicional de texto.

# Sintaxe Básica: Verb-Noun
Os comandos do PowerShell são conhecidos como cmdlets (pronuncia-se command-lets). Eles são muito mais poderosos do que os comandos tradicionais do Windows e permitem uma manipulação de dados mais avançada.

Os cmdlets seguem uma convenção de nomenclatura consistente Verbo-Substantivo. Essa estrutura facilita a compreensão do que cada cmdlet faz. O Verbo descreve a ação e o Substantivo especifica o objeto no qual a ação é executada. Por exemplo:

* Get-Content: Recupera (get) o conteúdo de um arquivo e o exibe no console.
* Set-Location: Altera (set) o diretório de trabalho atual.
* Get-Command: Recupera (get) os comandos que podem ser usados.
* Get-Command -CommandType "Function": Se quisermos exibir apenas os comandos disponíveis do tipo “function”.
* Get-Help: Ele fornece informações detalhadas sobre cmdlets, incluindo uso, parâmetros e exemplos.

# Onde Encontrar e Baixar Cmdlets
Outro recurso poderoso do PowerShell é a possibilidade de estender sua funcionalidade baixando cmdlets adicionais de repositórios online.

Para pesquisar módulos (coleções de cmdlets) em repositórios online como a Galeria do PowerShell, podemos usar ```Find-Module```. Às vezes, se não soubermos o nome exato do módulo, pode ser útil pesquisar módulos com um nome semelhante. Podemos fazer isso filtrando a propriedade ```-Name``` e anexando um curinga (*) ao nome parcial do módulo, usando a seguinte sintaxe padrão do PowerShell: ``` Cmdlet -Property "pattern*"```

Uma vez identificados, os módulos podem ser baixados e instalados do repositório com ```Install-Module```, disponibilizando para uso novos cmdlets contidos no módulo.

> Exercícios de reforço

```
Como você recuperaria uma lista de comandos que começam com o verbo Remove?

Get-Command -Name Remove*

Qual cmdlet tem sua contraparte tradicional echo como alias?

Write-Output

Qual é o comando para recuperar um exemplo de uso do cmdlet New-LocalUser?

Get-Help New-LocalUser -examples

Resposta correta
```

# Navegando por diretórios
O PowerShell fornece uma variedade de cmdlets para navegar em diretórios e gerenciar arquivos, muitos dos quais têm equivalentes na CLI tradicional do Windows.

Semelhante ao comando ```dir``` no Prompt de Comando (ou ls em Linux), ```Get-ChildItem``` lista os arquivos e diretórios em um local especificado com o parâmetro ```-Path```. Ele pode ser usado para explorar diretórios e visualizar seu conteúdo. Se nenhum caminho for especificado, o cmdlet exibirá o conteúdo do diretório de trabalho atual.

Para navegar para um diretório diferente, podemos usar o cmdlet ```Set-Location```. Ele altera o diretório atual, levando ao caminho especificado, semelhante ao comando ```cd``` no Prompt de Comando.

O PowerShell simplifica, fornecendo um único conjunto de cmdlets para lidar com a criação e o gerenciamento de arquivos e diretórios.
Para criar um item no PowerShell, podemos usar ```New-Item```. Precisaremos especificar o caminho do item e seu tipo (se é um arquivo ou um diretório).

Exemplo: ```New-Item -Path ".\captain-cabin\captain-wardrobe" -ItemType "Directory"```

Para removermos um arquivo ou diretório, utilizamos o ```Remove-Item```

Exemplo: ```Remove-Item -Path ".\captain-cabin\captain-wardrobe\captain-boots.txt"
            Remove-Item -Path ".\captain-cabin\captain-wardrobe" ```

Podemos copiar ou mover arquivos e diretórios da mesma forma, usando respectivamente ```Copy-Item``` (equivalente a ```copy```) e ```Move-Item``` (equivalente a ```mv```).

Exemplo: ```Copy-Item -Path .\captain-cabin\captain-hat.txt -Destination .\captain-cabin\captain-hat2.txt
            Get-ChildItem -Path ".\captain-cabin\"```

Para ler e exibir o conteúdo de um arquivo, podemos usar o cmdlet ```Get-Content```, que funciona de forma semelhante ao comando ```type``` ou ```cat```.

Exemplo: ```Get-Content -Path ".\captain-hat.txt"```

> Exercícios de reforço

```
Qual cmdlet você pode usar em vez do comando tradicional do Windows "type"?

Get-Content

Qual comando do PowerShell você usaria para exibir o conteúdo do diretório "C:\Usuários"?

Get-ChildItem -Path C:\Usuários
```
# Método Piping
Piping é uma técnica usada em ambientes de linha de comando que permite que a saída de um comando seja usada como entrada para outro. Isso cria uma sequência de operações em que os dados fluem de um comando para o próximo. Representado pelo símbolo ```|```, o piping é amplamente utilizado na CLI do Windows ou no Linux.

No PowerShell, o piping é ainda mais poderoso porque passa objetos em vez de apenas texto. Esses objetos carregam não apenas os dados, mas também as propriedades e os métodos que descrevem e interagem com os dados.

Exemplo: ```Get-ChildItem | Sort-Object Length```

Aqui, ```Get-ChildItem``` recupera os arquivos (como objetos) e o ```pipe (|)``` envia esses objetos de arquivo para ```Sort-Object```, que os classifica por sua propriedade ```Length``` (tamanho). Essa abordagem baseada em objetos permite sequências de comandos mais detalhadas e flexíveis.

Para filtrar objetos com base em condições especificadas, retornando apenas aqueles que atendem aos critérios, podemos usar o cmdlet Where-Object. Por exemplo, para listar apenas arquivos .txt em um diretório.

Exemplo: ```Get-ChildItem | Where-Object -Property "Extension" -eq ".txt" ```

Aqui, ```Where-Object``` filtra os arquivos pela propriedade ```Extension```, garantindo que apenas arquivos com ```extensão igual (-eq)``` a .txt sejam listados.

Mais alguns dos operadores mais úteis:

* ne: "diferente de". Este operador pode ser usado para excluir objetos dos resultados com base em critérios específicos.
* gt: "maior que". Este operador filtrará apenas objetos que excedam um valor especificado. É importante observar que esta é uma comparação estrita, o que significa que objetos iguais ao valor especificado serão excluídos dos resultados.
* ge: "maior ou igual a". Esta é a versão não estrita do operador anterior. Uma combinação de -gt e -eq.
* lt: "menor que". Assim como sua contraparte, "maior que", este é um operador estrito. Incluirá apenas objetos estritamente abaixo de um determinado valor.
* le: "menor ou igual a". Assim como seu equivalente -ge, esta é a versão não estrita do operador anterior. Uma combinação de -lt e -eq.

Exemplo: ```Get-ChildItem | Where-Object -Property "Name" -like "ship*"```

O cmdlet ```Select-Object``` é usado para selecionar propriedades específicas de objetos ou limitar o número de objetos retornados. É útil para refinar a saída e exibir apenas os detalhes necessários.

Exmeplo: ```Get-ChildItem | Select-Object Name,Length```

O pipeline de cmdlets pode ser expandido adicionando mais comandos, já que o recurso não se limita apenas à conexão entre dois cmdlets.

> Exemplo de fixação

```
tente construir um pipeline de cmdlets para classificar e filtrar a saída com o objetivo de exibir o maior arquivo no C:\Users\captain\Documents\captain-cabin

Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1

Como você recuperaria os itens no diretório atual com tamanho maior que 100?

Get-ChildItem | Where-Object -Property Length -gt 100
```

O ```Select-String``` busca padrões de texto em arquivos, semelhante ao ```grep``` no Linux ou ao ```findstr``` no CMD do Windows. É comumente usado para encontrar conteúdo específico em arquivos de log ou documentos. O cmdlet Select-String oferece suporte total ao uso de [expressões regulares](https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expressions). Esse recurso avançado permite a correspondência de padrões complexos dentro de arquivos, tornando-o uma ferramenta poderosa para pesquisar e analisar dados de texto.

Exemplo: ```Select-String -Path ".\captain-hat.txt" -Pattern "hat"```







