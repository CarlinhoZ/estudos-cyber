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
....* -CommandType "Function": Se quisermos exibir apenas os comandos disponíveis do tipo “function”.
* Get-Help: Ele fornece informações detalhadas sobre cmdlets, incluindo uso, parâmetros e exemplos.

