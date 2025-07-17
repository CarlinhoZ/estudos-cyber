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







