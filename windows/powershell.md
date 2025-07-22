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

# Informações de sistema e rede
O cmdlet ```Get-ComputerInfo``` recupera informações abrangentes do sistema, incluindo informações do sistema operacional, especificações de hardware, detalhes do BIOS, etc.. Ele fornece um instantâneo de toda a configuração do sistema em um único comando. Seu equivalente tradicional, ```systeminfo```, recupera apenas um pequeno conjunto dos mesmos detalhes.

Essencial para gerenciar contas de usuários e entender a configuração de segurança da máquina, o ```Get-LocalUser``` lista todas as contas de usuários locais no sistema. A saída padrão exibe, para cada usuário, o nome de usuário, o status da conta e a descrição.

```Get-NetIPConfiguration``` fornece informações detalhadas sobre as interfaces de rede no sistema, incluindo endereços IP, servidores DNS e configurações de gateway.

Caso precisemos de detalhes específicos sobre os endereços IP atribuídos às interfaces de rede, o cmdlet ```Get-NetIPAddress``` mostrará detalhes de todos os endereços IP configurados no sistema, incluindo aqueles que não estão ativos no momento.

# Análise de processos em tempo real
O ```Get-Process``` fornece uma visão detalhada de todos os processos em execução, incluindo o uso de CPU e memória, tornando-se uma ferramenta poderosa para monitoramento e solução de problemas.

Da mesma forma, o ```Get-Service``` permite a recuperação de informações sobre o status dos serviços na máquina, como quais serviços estão em execução, parados ou pausados. É amplamente utilizado na solução de problemas por administradores de sistema, mas também por analistas forenses que buscam serviços anômalos instalados no sistema.

Para monitorar conexões de rede ativas, o ```Get-NetTCPConnection``` exibe as conexões TCP atuais, fornecendo insights sobre endpoints locais e remotos. Este cmdlet é particularmente útil durante uma tarefa de resposta a incidentes ou análise de malware, pois pode descobrir backdoors ocultos ou conexões estabelecidas com um servidor controlado por um invasor.

Além disso, mencionaremos ```Get-FileHash``` como um cmdlet útil para gerar hashes de arquivos, o que é particularmente valioso em resposta a incidentes, detecção de ameaças e análise de malware, pois ajuda a verificar a integridade dos arquivos e detectar possíveis adulterações.

> Pequeno desafio para reforçar o conhecimento
```
Um serviço vital foi instalado neste navio pirata para garantir que o capitão possa sempre navegar com segurança. Mas algo não está funcionando como esperado, e o capitão se pergunta o porquê. Investigando, eles finalmente descobrem a verdade: o serviço foi adulterado! O sujeito suspeito de antes modificou o nome de exibição do serviço para refletir seu próprio lema, o mesmo que ele colocou em sua descrição de usuário.

Com essas informações e o conhecimento de PowerShell que você adquiriu até agora, você consegue encontrar o nome do serviço?

```
Inicialmente utilizei o ```Set-Location``` para a pasta do usuário p1r4t3, em busca de pistas, porém percebi que deveria buscar um serviço com o nome desse usuário.
Foi aí que utilizei o ```Get-Service -Name "p1r4t3"``` e me retornou o serviço ```p1r4t3-s-compass```.

# Scripting
Scripting é o processo de escrever e executar uma série de comandos contidos em um arquivo de texto, conhecido como script, para automatizar tarefas que geralmente seriam executadas manualmente em um shell, como o PowerShell.

Em termos simples, scripting é como dar a um computador uma lista de tarefas, onde cada linha do script é uma tarefa que o computador executará automaticamente. Isso economiza tempo, reduz a chance de erros e permite executar tarefas muito complexas ou tediosas para serem feitas manualmente. 

* Para profissionais de Blue Team, como respondedores de incidentes, analistas de malware e caçadores de ameaças, os scripts do PowerShell podem automatizar diversas tarefas, incluindo análise de logs, detecção de anomalias e extração de indicadores de comprometimento (IOCs). Esses scripts também podem ser usados para realizar engenharia reversa de código malicioso (malware) ou automatizar a varredura de sistemas em busca de sinais de intrusão.

* Para o Red Team, incluindo testadores de penetração e hackers éticos, os scripts do PowerShell podem automatizar tarefas como enumeração de sistemas, execução de comandos remotos e criação de scripts ofuscados para contornar defesas. Sua profunda integração com todos os tipos de sistemas o torna uma ferramenta poderosa para simular ataques e testar a resiliência dos sistemas contra ameaças do mundo real.

* Mantendo-se no contexto da segurança cibernética, os administradores de sistemas se beneficiam dos scripts do PowerShell para automatizar verificações de integridade, gerenciar configurações de sistemas e proteger redes, especialmente em ambientes remotos ou de grande porte. Os scripts do PowerShell podem ser projetados para aplicar políticas de segurança, monitorar a integridade dos sistemas e responder automaticamente a incidentes de segurança, aprimorando assim a postura geral de segurança.

O ```Invoke-Command``` é essencial para a execução de comandos em sistemas remotos, tornando-o fundamental para administradores de sistemas, engenheiros de segurança e testadores de penetração. O ```Invoke-Command``` permite o gerenciamento remoto eficiente e, combinado com scripts, a automação de tarefas em várias máquinas. Ele também pode ser usado para executar payloads ou comandos em sistemas alvo durante um ataque por testadores de penetração — ou mesmo por invasores.

Utilizando o ```Get-Help Invoke-Command -examples```, nos retorna informações valiosas sobre seu funcionamento.

> Exercício para fixação
```
Qual é a sintaxe para executar o comando Get-Service em um computador remoto chamado "RoyalFortune"? Suponha que você não precise fornecer credenciais para estabelecer a conexão.

Invoke-Command -ComputerName RoyalFortune -ScriptBlock { Get-Service }
```











