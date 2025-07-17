# Sistema de Arquivos
O sistema de arquivos usado nas versões modernas do Windows é o New Technology File System ou [NTFS](https://learn.microsoft.com/en-us/windows-server/storage/file-server/ntfs-overview).

Antes do NTFS, havia o FAT16/FAT32 (File Allocation Table) e o HPFS (High Performance File System).

Você ainda vê partições FAT em uso hoje. Por exemplo, normalmente você vê partições FAT em dispositivos USB, cartões MicroSD, etc., mas tradicionalmente não em computadores/laptops pessoais com Windows ou servidores Windows.

O NTFS é conhecido como um sistema de arquivos com registro em diário. Em caso de falha, o sistema de arquivos pode reparar automaticamente as pastas/arquivos no disco usando as informações armazenadas em um arquivo de log. Essa função não é possível com o FAT.

O NTFS aborda muitas das limitações dos sistemas de arquivos anteriores, como:

* Suporta arquivos maiores que 4 GB
* Definir permissões específicas para pastas e arquivos
* Compactação de pastas e arquivos
* Criptografia ([Encryption File System](https://learn.microsoft.com/en-us/windows/win32/fileio/file-encryption) ou EFS)
Documentação oficial da Microsoft em relação ao sistema de arquivos [aqui](https://learn.microsoft.com/en-us/troubleshoot/windows-client/backup-and-storage/fat-hpfs-and-ntfs-file-systems).

Em volumes NTFS, você pode definir permissões que concedem ou negam acesso a arquivos e pastas.

As permissões são:

* Controle total
* Modificar
* Ler e executar
* Listar o conteúdo da pasta
* Ler
* Gravar

Um explicativo da própria documentação da Microsoft, em relação as permissões, pode ser visto [aqui](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/bb727008(v=technet.10)?redirectedfrom=MSDN).

### Alternate Data Streams (ADS)
Outro recurso do NTFS são os Alternate Data Streams  (ADS).
Os ADS são um atributo de arquivo específico do Windows NTFS.
Cada arquivo possui pelo menos um fluxo de dados ($DATA), e o ADS permite que os arquivos contenham mais de um fluxo de dados. Nativamente, o Windows Explorer não exibe o ADS para o usuário. Existem executáveis de terceiros que podem ser usados para visualizar esses dados, mas o PowerShell oferece a capacidade de visualizar o ADS para arquivos.
Do ponto de vista da segurança, criadores de malware têm usado o ADS para ocultar dados.
Nem todos os seus usos são maliciosos. Por exemplo, quando você baixa um arquivo da Internet, há identificadores gravados no ADS para identificar que o arquivo foi baixado da Internet.
Para saber mais sobre o ADS, veja o seguinte link do MalwareBytes [aqui](https://www.malwarebytes.com/blog/101/2015/07/introduction-to-alternate-data-streams).

# Diretório Windows
A pasta Windows (C:\Windows) é tradicionalmente conhecida como a pasta que contém o sistema operacional Windows.
A pasta não precisa necessariamente residir na unidade C. Ela pode residir em qualquer outra unidade e, tecnicamente, pode residir em uma pasta diferente.
É aqui que as variáveis de ambiente, mais especificamente as variáveis de ambiente do sistema, entram em ação. Embora ainda não tenha sido discutida, a variável de ambiente do sistema para o diretório Windows é **%windir%.**

De acordo com a Microsoft, "Variáveis de ambiente armazenam informações sobre o ambiente do sistema operacional. Essas informações incluem detalhes como o caminho do sistema operacional, o número de processadores usados pelo sistema operacional e a localização das pastas temporárias".

A pasta System32 contém os arquivos importantes para o sistema operacional.
Você deve ter extremo cuidado ao interagir com esta pasta. Excluir acidentalmente quaisquer arquivos ou pastas dentro do System32 pode tornar o sistema operacional inoperante. Saiba mais sobre esta ação [aqui](https://www.howtogeek.com/346997/what-is-the-system32-directory-and-why-you-shouldnt-delete-it/).

# Contas de usuário, perfis e permissões
As contas de usuário podem ser de dois tipos em um sistema Windows local típico: **Administrador** e **Usuário Padrão.**

O tipo de conta de usuário determinará quais ações o usuário pode executar naquele sistema Windows específico.

* Um Administrador pode fazer alterações no sistema: adicionar usuários, excluir usuários, modificar grupos, modificar configurações do sistema, etc.
* Um Usuário Padrão só pode fazer alterações em pastas/arquivos atribuídos ao usuário e não pode realizar alterações no nível do sistema, como instalar programas.

Quando uma conta de usuário é criada, um perfil é criado para o usuário. O local para cada pasta de perfil de usuário será C:\Usuários.

Por exemplo, a pasta de perfil de usuário para a conta de usuário Max será C:\Usuários\Max.

A criação do perfil do usuário é feita no login inicial. Quando uma nova conta de usuário faz login em um sistema local pela primeira vez, ela verá várias mensagens na tela de login. Uma das mensagens, "Serviço de Perfil de Usuário", permanece na tela de login por um tempo, enquanto cria o perfil do usuário.

Outra maneira de acessar essas informações, e muito mais, é usando o Gerenciamento de Usuários e Grupos Locais.
Clique com o botão direito no Menu Iniciar e clique em Executar. Digite ```lusrmgr.msc```

No lusrmgr, você verá duas pastas: Usuários e Grupos.

Se clicar em Grupos, você verá todos os nomes dos grupos locais, juntamente com uma breve descrição de cada grupo.

Cada grupo possui permissões definidas, e os usuários são atribuídos/adicionados a grupos pelo Administrador. Quando um usuário é atribuído a um grupo, ele herda as permissões desse grupo. Um usuário pode ser atribuído a vários grupos.

# User Account Control (UAC)
A grande maioria dos usuários domésticos está conectada aos seus sistemas Windows como administradores locais.
Um usuário não precisa executar tarefas com privilégios altos (elevados) no sistema, como navegar na Internet, trabalhar em um documento do Word, etc. Esse privilégio elevado aumenta o risco de comprometimento do sistema, pois facilita a infecção por malware. Consequentemente, como a conta do usuário pode fazer alterações no sistema, o malware seria executado no contexto do usuário conectado.

Para proteger o usuário local com esses privilégios, a Microsoft introduziu o Controle de Conta de Usuário (UAC). Esse conceito foi introduzido pela primeira vez com o breve Windows Vista e continuou nas versões subsequentes do Windows.

### Como funciona o UAC?
Quando um usuário com o tipo de conta "administrador" efetua login em um sistema, a sessão atual não é executada com permissões elevadas. Quando uma operação que requer privilégios de nível superior precisar ser executada, o usuário será solicitado a confirmar se permite a execução da operação.
[Aqui](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/how-it-works) há uma docuentação oficial da Microsoft sobre UAC.

# Configuração de Sistema (MSConfig)
O utilitário de configuração do sistema (MSConfig) é usado para solução de problemas avançada e seu principal objetivo é ajudar a diagnosticar problemas de inicialização.
Documentação oficial da Microsoft relacionado a mais funções presentes no utilitário [aqui](https://learn.microsoft.com/en-us/troubleshoot/windows-client/performance/system-configuration-utility-troubleshoot-configuration-errors).

O utilitário possui cinco abas na parte superior. Abaixo estão os nomes de cada aba.

1. Geral
2. Inicialização
3. Serviços
4. Inicialização
5. Ferramentas

* Na aba Geral, podemos selecionar quais dispositivos e serviços do Windows serão carregados na inicialização. As opções são: Normal, Diagnóstico ou Seletivo.
* Na aba Inicialização, podemos definir várias opções de inicialização para o Sistema Operacional.
* A aba Serviços lista todos os serviços configurados para o sistema, independentemente de seu estado (em execução ou parado). Um serviço é um tipo especial de aplicativo executado em segundo plano.
* Na aba Inicialização, você não verá nada de interessante na VM anexada. Abaixo está uma captura de tela da aba Inicialização do MSConfig da minha máquina local.
* Há uma lista de vários utilitários (ferramentas) na aba Ferramentas que podemos executar para configurar melhor o sistema operacional. Há uma breve descrição de cada ferramenta para fornecer algumas informações sobre sua finalidade.

## Gerenciamento do Computador (compmgmt)
O utilitário Gerenciamento do Computador (compmgmt) tem três seções principais: Ferramentas do Sistema, Armazenamento e Serviços e Aplicativos.

### Ferramentas do Sistema

Segundo a Microsoft, com o Agendador de Tarefas, podemos criar e gerenciar tarefas comuns que nosso computador executará automaticamente nos horários que especificarmos.

Uma tarefa pode executar um aplicativo, um script, etc., e pode ser configurada para ser executada a qualquer momento. Uma tarefa pode ser executada no login ou no logout. As tarefas também podem ser configuradas para serem executadas em um agendamento específico, por exemplo, a cada cinco minutos.

### Visualizador de Eventos.

O Visualizador de Eventos nos permite visualizar eventos que ocorreram no computador. Esses registros de eventos podem ser vistos como uma trilha de auditoria que pode ser usada para entender a atividade do sistema do computador. Essas informações são frequentemente usadas para diagnosticar problemas e investigar ações executadas no sistema.

O Visualizador de Eventos possui três painéis.
* O painel à esquerda fornece uma lista hierárquica dos provedores de log de eventos (como mostrado na imagem acima).
* O painel do meio exibirá uma visão geral e um resumo dos eventos específicos de um provedor selecionado.
* O painel à direita é o painel de ações.

Existem cinco tipos de eventos que podem ser registrados. A Microsoft fornece uma breve descrição de cada um, em sua [documentação](https://learn.microsoft.com/en-us/windows/win32/eventlog/event-types).

Os logs padrão estão visíveis em Logs do Windows. A Microsoft fornece uma breve descrição de cada um, em sua [documentação](https://learn.microsoft.com/en-us/windows/win32/eventlog/eventlog-key).

# Pastas Compartilhadas
Pastas compartilhadas é onde você verá uma lista completa de compartilhamentos e pastas compartilhadas às quais outros podem se conectar.

### Compartilhamentos
Ali estão o compartilhamento padrão do Windows, C$, e os compartilhamentos de administração remota padrão criados pelo Windows, como ADMIN$.
Como em qualquer objeto no Windows, você pode clicar com o botão direito do mouse em uma pasta para visualizar suas propriedades, como Permissões (quem pode acessar o recurso compartilhado).

### Sessões
Você verá uma lista de usuários que estão conectados aos compartilhamentos. Nesta VM, você não verá ninguém conectado aos compartilhamentos.
Todas as pastas e/ou arquivos que os usuários conectados acessam serão listados em Arquivos Abertos.

### Desempenho
Você verá um utilitário chamado Monitor de Desempenho (perfmon).

O Perfmon é usado para visualizar dados de desempenho em tempo real ou a partir de um arquivo de log. Este utilitário é útil para solucionar problemas de desempenho em um sistema de computador, seja ele local ou remoto.

### Gerenciador de Dispositivos
Permite visualizar e configurar o hardware, como desabilitar qualquer hardware conectado ao computador.

### Armazenamento

Em Armazenamento, você encontrará Backup e Gerenciamento de Disco do Windows Server e Gerenciamento de Disco.
O Gerenciamento de Disco é um utilitário de sistema do Windows que permite executar tarefas avançadas de armazenamento. Algumas tarefas são:

* Configurar uma nova unidade
* Estender uma partição
* Reduzir uma partição
* Atribuir ou alterar uma letra de unidade (ex.: E:)

## Ferramenta de Informações do Sistema (msinfo32)

Segundo a Microsoft, "o Windows inclui uma ferramenta chamada Informações do Sistema Microsoft (Msinfo32.exe). Essa ferramenta coleta informações sobre o seu computador e exibe uma visão abrangente do hardware, dos componentes do sistema e do ambiente de software, que você pode usar para diagnosticar problemas no computador."

As informações no Resumo do Sistema são divididas em três seções:

* Recursos de Hardware
* Componentes
* Ambiente de Software

### Resumo do Sistema
Exibirá especificações técnicas gerais do computador, como marca e modelo do processador.

### Recursos de Hardware
Recursos de hardware são os caminhos de barramento endereçáveis e atribuíveis que permitem que dispositivos periféricos e processadores do sistema se comuniquem entre si. Recursos de hardware normalmente incluem endereços de porta de E/S, vetores de interrupção e blocos de endereços de memória relativos ao barramento.

### Componentes
Você pode ver informações específicas sobre os dispositivos de hardware instalados no computador. Algumas seções não mostram nenhuma informação, mas outras mostram, como Vídeo e Entrada.

### Ambiente de Software
Você pode ver informações sobre o software incorporado ao sistema operacional e o software que você instalou. Outros detalhes também são visíveis nesta seção, como as Variáveis de Ambiente e Conexões de Rede.

## Monitor de Recursos (resmon)
O que é o Monitor de Recursos (resmon)?

De acordo com a Microsoft, "O Monitor de Recursos exibe informações de uso de CPU, memória, disco e rede por processo e agregadas, além de fornecer detalhes sobre quais processos estão usando identificadores de arquivo e módulos individuais. A filtragem avançada permite que os usuários isolem os dados relacionados a um ou mais processos (aplicativos ou serviços), iniciem, parem, pausem e retornem serviços, e fechem aplicativos que não respondem a partir da interface do usuário. Ele também inclui um recurso de análise de processos que pode ajudar a identificar processos travados e conflitos de bloqueio de arquivos, para que o usuário possa tentar resolver o conflito em vez de fechar um aplicativo e potencialmente perder dados."

Este utilitário é voltado principalmente para usuários avançados que precisam executar soluções de problemas avançadas no sistema do computador.

Na guia Visão Geral, o Resmon possui quatro seções:

* CPU
* Disco
* Rede
* Memória

## Prompt de Comando (cmd)
Neste [link](https://ss64.com/nt/) haverá um A-Z de todos os comandos que podem ser utilizados no CMD.

## Registro do Windows
O Registro do Windows é um banco de dados hierárquico central usado para armazenar as informações necessárias para configurar o sistema para um ou mais usuários, aplicativos e dispositivos de hardware.

O Registro contém informações que o Windows consulta continuamente durante a operação, como:

* Perfis de cada usuário
* Aplicativos instalados no computador e os tipos de documentos que cada um pode criar
*Configurações da folha de propriedades para pastas e ícones de aplicativos
* Qual hardware existe no sistema
* As portas que estão sendo utilizadas

Neste [link](https://learn.microsoft.com/en-us/troubleshoot/windows-server/performance/windows-registry-advanced-users) a Microsoft disponibiliza uma documentação de uso do editor de registro para profissionais de TI.

# Windows Update
O Windows Update é um serviço fornecido pela Microsoft para fornecer atualizações de segurança, melhorias de recursos e patches para o sistema operacional Windows e outros produtos Microsoft, como o Microsoft Defender.

As atualizações geralmente são lançadas na segunda terça-feira de cada mês. Esse dia é chamado de Patch Tuesday. Isso não significa necessariamente que uma atualização/patch crítico precise esperar até o próximo Patch Tuesday para ser lançado. Se a atualização for urgente, a Microsoft a enviará por meio do serviço Windows Update para os dispositivos Windows.

Consulte o link a seguir para ver o Guia de Atualizações de Segurança da Microsoft [aqui](https://msrc.microsoft.com/update-guide).

Dica: Outra maneira de acessar o Windows Update é pela caixa de diálogo Executar, ou CMD, executando o comando control /name Microsoft.WindowsUpdate

Ao longo dos anos, os usuários do Windows se acostumaram a adiar as atualizações do Windows para uma data posterior ou a não instalá-las. Vários motivos levaram a essa ação, um deles sendo o fato de que normalmente é necessário reinicializar o computador após uma atualização do Windows.

A Microsoft resolveu esse problema de forma notável com o Windows 10. As atualizações não podem mais ser ignoradas ou deixadas de lado até serem esquecidas. As atualizações do Windows só podem ser adiadas, mas, eventualmente, a atualização será realizada e seu computador será reiniciado. A Microsoft fornece essas atualizações para manter o dispositivo seguro e protegido.

# Windows Security
Na aba de informações sobre segurança do Windows, há quatro opções, sendo elas:

*Proteção contra vírus e ameaças
* Proteção de firewall e rede
* Controle de aplicativos e navegadores
* Segurança do dispositivo

Há alguns ícones de status que estão presentes nas opções de segurança, sendo elas:.

* Verde significa que seu dispositivo está suficientemente protegido e não há ações recomendadas.
* Amarelo significa que há uma recomendação de segurança para você revisar.
* Vermelho é um aviso de que algo precisa de sua atenção imediata.

## Vírus e ameaças
A proteção contra vírus e ameaças é dividida em duas partes:

* Ameaças atuais
* Configurações de proteção contra vírus e ameaças

### Ameaças atuais

**Opções de verificação**

* Verificação rápida - Verifica as pastas do seu sistema onde as ameaças são comumente encontradas.
* Verificação completa - Verifica todos os arquivos e programas em execução no seu disco rígido. Esta verificação pode levar mais de uma hora.
* Verificação personalizada - Escolha quais arquivos e locais você deseja verificar.

**Histórico de ameaças**

* Última verificação - O Antivírus Windows Defender verifica automaticamente seu dispositivo em busca de vírus e outras ameaças para ajudar a mantê-lo seguro.
* Ameaças em quarentena - As ameaças em quarentena foram isoladas e impedidas de serem executadas no seu dispositivo. Elas serão removidas periodicamente.
* Ameaças permitidas - Ameaças permitidas são itens identificados como ameaças, que você permitiu que fossem executados no seu dispositivo.

### Configurações de proteção contra vírus e ameaças

**Gerenciar configurações**

* Proteção em tempo real - Localiza e impede a instalação ou execução de malware no seu dispositivo.
* Proteção fornecida pela nuvem - Oferece proteção aprimorada e mais rápida com acesso aos dados de proteção mais recentes na nuvem.
* Envio automático de amostras - Envie arquivos de amostra para a Microsoft para ajudar a proteger você e outras pessoas contra possíveis ameaças.
* Acesso controlado a pastas - Proteja arquivos, pastas e áreas de memória do seu dispositivo contra alterações não autorizadas por aplicativos hostis.
* Exclusões - O Antivírus do Windows Defender não verificará itens que você excluiu.
* Notificações - O Antivírus do Windows Defender enviará notificações com informações críticas sobre a integridade e a segurança do seu dispositivo.
* Aviso: Itens excluídos podem conter ameaças que tornam seu dispositivo vulnerável. Use esta opção somente se tiver 100% de certeza do que está fazendo.

**Atualizações de proteção contra vírus e ameaças**

*Verificar atualizações - Verifique manualmente se há atualizações para atualizar as definições do Antivírus do Windows Defender.

**Proteção contra ransomware**

* Acesso controlado a pastas - A proteção contra ransomware requer que este recurso esteja habilitado, o que, por sua vez, requer que a Proteção em Tempo Real esteja habilitada.

## Microsoft Defender SmartScreen.

De acordo com a Microsoft, "o Microsoft Defender SmartScreen protege contra sites e aplicativos de phishing ou malware, além do download de arquivos potencialmente maliciosos".

O documento oficial da Microsoft sobre o [Microsoft Defender SmartScreen](https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview).

### Verificar aplicativos e arquivos

O Windows Defender SmartScreen ajuda a proteger seu dispositivo verificando aplicativos e arquivos não reconhecidos na web.

### Proteção contra exploits

A proteção contra exploits é integrada ao Windows para ajudar a proteger seu dispositivo contra ataques.

# Volume Shadow Copy Service (VSS)
Segundo a Microsoft, o Serviço de Cópias de Sombra de Volume (VSS) coordena as ações necessárias para criar uma cópia de sombra consistente (também conhecida como snapshot ou cópia pontual) dos dados a serem copiados.

As Cópias de Sombra de Volume são armazenadas na pasta Informações de Volume do Sistema em cada unidade com a proteção ativada.
Se o VSS estiver ativado (Proteção do Sistema ativada), você poderá executar as seguintes tarefas nas configurações avançadas do sistema.

* Criar um ponto de restauração
* Executar restauração do sistema
* Definir as configurações de restauração
E* xcluir pontos de restauração

Do ponto de vista da segurança, os criadores de malware conhecem esse recurso do Windows e escrevem códigos em seus malwares para procurar esses arquivos e excluí-los. Isso torna impossível a recuperação de um ataque de ransomware, a menos que você tenha um backup offline/externo.

Você consegue acessar o VSS clicando com o botão direito no disco local C: e clicando em "Configurar Cópia de Sombra".




