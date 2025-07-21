# Domínios de Windows
Um domínio Windows é um grupo de usuários e computadores sob a administração de uma determinada empresa. A ideia principal por trás de um domínio é centralizar a administração de componentes comuns de uma rede de computadores Windows em um único repositório chamado Active Directory (AD). O servidor que executa os serviços do Active Directory é conhecido como Domain Controller (DC).

As principais vantagens de ter um domínio Windows configurado são:

* Gerenciamento centralizado de identidades: Todos os usuários da rede podem ser configurados a partir do Active Directory com o mínimo de esforço.
* Gerenciamento de políticas de segurança: Você pode configurar políticas de segurança diretamente do Active Directory e aplicá-las a usuários e computadores da rede, conforme necessário.

Em redes com domínio, você frequentemente receberá um nome de usuário e uma senha que poderá usar em qualquer um dos computadores disponíveis. Suas credenciais são válidas para todas as máquinas, pois sempre que você as inserir em uma máquina, o processo de autenticação será encaminhado de volta para o Active Directory, onde suas credenciais serão verificadas. Graças ao Active Directory, suas credenciais não precisam existir em todas as máquinas e estão disponíveis em toda a rede.

O Active Directory também é o componente que permite que restrinja seu acesso ao painel de controle nas máquinas. As políticas geralmente serão implantadas em toda a rede para que você não tenha privilégios administrativos sobre esses computadores.

# Active Directory (AD)
O núcleo de qualquer domínio do Windows é o Active Directory Domain Services (AD DS). Este serviço atua como um catálogo que contém as informações de todos os "objetos" existentes na sua rede. Entre os muitos objetos suportados pelo AD, temos usuários, grupos, máquinas, impressoras, compartilhamentos e muitos outros.

## Usuários

Usuários são um dos tipos de objetos mais comuns no Active Directory. Usuários são um dos objetos conhecidos como entidades de segurança, o que significa que podem ser autenticados pelo domínio e receber privilégios sobre recursos como arquivos ou impressoras. Pode-se dizer que uma entidade de segurança é um objeto que pode atuar sobre recursos na rede.

Usuários podem ser usados para representar dois tipos de entidades:

### Pessoas: usuários geralmente representam pessoas em sua organização que precisam acessar a rede, como funcionários.
### Serviços: você também pode definir usuários para serem usados por serviços como IIS ou MSSQL. Cada serviço requer um usuário para ser executado, mas os usuários de serviço são diferentes dos usuários comuns, pois terão apenas os privilégios necessários para executar seu serviço específico.

## Máquinas

Máquinas são outro tipo de objeto dentro do Active Directory; para cada computador que ingressa no domínio do Active Directory, um objeto de máquina será criado. As máquinas também são consideradas "entidades de segurança" e recebem uma conta, assim como qualquer usuário comum. Essa conta tem direitos um tanto limitados dentro do próprio domínio.

As contas de máquina em si são administradores locais no computador atribuído e geralmente não devem ser acessadas por ninguém, exceto o próprio computador, mas, como acontece com qualquer outra conta, se você tiver a senha, poderá usá-la para fazer login.

Identificar contas de máquina é relativamente fácil. Elas seguem um esquema de nomenclatura específico. O nome da conta de máquina é o nome do computador seguido por um cifrão. Por exemplo, uma máquina chamada DC01 terá uma conta de máquina chamada DC01$.

## Grupos de Segurança

Se você conhece o Windows, provavelmente sabe que pode definir grupos de usuários para atribuir direitos de acesso a arquivos ou outros recursos a grupos inteiros, em vez de usuários individuais. Isso permite uma melhor gerenciabilidade, pois você pode adicionar usuários a um grupo existente, e eles herdarão automaticamente todos os privilégios do grupo. Grupos de segurança também são considerados entidades de segurança e, portanto, podem ter privilégios sobre recursos na rede.

Os grupos podem ter usuários e máquinas como membros. Se necessário, os grupos também podem incluir outros grupos.

* Administradores de Domínio: Os usuários deste grupo têm privilégios administrativos sobre todo o domínio. Por padrão, eles podem administrar qualquer computador no domínio, incluindo os controladores de domínio (DCs).
* Operadores de Servidor: Os usuários deste grupo podem administrar Controladores de Domínio. Eles não podem alterar nenhuma associação de grupo administrativo.
* Operadores de Backup: Os usuários deste grupo têm permissão para acessar qualquer arquivo, ignorando suas permissões. Eles são usados para realizar backups de dados em computadores.
* Operadores de Conta: Os usuários deste grupo podem criar ou modificar outras contas no domínio.
* Usuários do Domínio: Inclui todas as contas de usuário existentes no domínio.
* Computadores do Domínio: Inclui todos os computadores existentes no domínio.
* Controladores de Domínio: Inclui todos os DCs existentes no domínio.

[Lista completa de grupos de segurança padrão na documentação da Microsoft](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-security-groups)

# Active Directory Users and Computers (ADUC)
Aqui é aonde fica a hierarquia de usuários, computadores e grupos existentes no domínio. Esses objetos são organizados em Unidades Organizacionais (UOs), que são objetos contêineres que permitem classificar usuários e máquinas. UOs são usadas principalmente para definir conjuntos de usuários com requisitos de policiamento semelhantes. As pessoas do departamento de Vendas da sua organização provavelmente terão um conjunto de políticas aplicado diferente das pessoas da TI, por exemplo. **Um usuário só pode fazer parte de uma UO por vez.**

É muito comum ver as UOs imitarem a estrutura da empresa, pois isso permite a implantação eficiente de políticas de base que se aplicam a departamentos inteiros. Lembre-se de que, embora esse seja o modelo esperado na maioria das vezes, você pode definir UOs arbitrariamente.

Existem outros contêineres padrão. Esses contêineres são criados automaticamente pelo Windows e contêm o seguinte:

* Builtin: Contém grupos padrão disponíveis para qualquer host Windows.
* Computadores: Qualquer máquina que se conectar à rede será colocada aqui por padrão. Você pode movê-los, se necessário.
* Controladores de Domínio: UO padrão que contém os controladores de domínio (DCs) em sua rede.
* Usuários: Usuários e grupos padrão que se aplicam a um contexto de domínio.
* Contas de Serviço Gerenciadas: Contém contas usadas por serviços em seu domínio Windows.

##  Grupos de Segurança vs. UOs

Embora ambos sejam usados para classificar usuários e computadores, suas finalidades são completamente diferentes:

* UOs são úteis para aplicar políticas a usuários e computadores, que incluem configurações específicas que pertencem a conjuntos de usuários, dependendo de sua função específica na empresa.
* Grupos de Segurança, por outro lado, são usados para conceder permissões sobre recursos. Por exemplo, você usará grupos se quiser permitir que alguns usuários acessem uma pasta compartilhada ou uma impressora de rede. Um usuário pode fazer parte de vários grupos, o que é necessário para conceder acesso a vários recursos.

## Delegação

Uma das coisas interessantes que você pode fazer no AD é conceder a usuários específicos algum controle sobre algumas UOs. Esse processo é conhecido como delegação e permite conceder aos usuários privilégios específicos para executar tarefas avançadas em UOs sem a necessidade de um Administrador de Domínio.

Um dos casos de uso mais comuns para isso é conceder ao suporte de TI privilégios para redefinir as senhas de outros usuários com privilégios baixos.

## Gerenciando computadores no AD
Por padrão, todas as máquinas que ingressam em um domínio (exceto os DCs) serão colocadas no contêiner chamado "Computadores".

Ter todos os nossos dispositivos ali não é a melhor ideia, pois é muito provável que você queira políticas diferentes para seus servidores e para as máquinas que os usuários comuns usam diariamente.
Embora não haja uma regra de ouro sobre como organizar suas máquinas, um excelente ponto de partida é segregar os dispositivos de acordo com seu uso.

Em geral, você esperaria ver dispositivos divididos em pelo menos as três categorias a seguir:

1. Estações de Trabalho

Estações de Trabalho são um dos dispositivos mais comuns em um domínio do Active Directory. Cada usuário no domínio provavelmente fará login em uma estação de trabalho. Este é o dispositivo que eles usarão para trabalhar ou navegar normalmente. Esses dispositivos nunca devem ter um usuário privilegiado conectado.

2. Servidores

Servidores são o segundo dispositivo mais comum em um domínio do Active Directory. Servidores geralmente são usados para fornecer serviços a usuários ou outros servidores.

3. Controladores de Domínio

Controladores de Domínio são o terceiro dispositivo mais comum em um domínio do Active Directory. Controladores de Domínio permitem que você gerencie o Domínio do Active Directory. Esses dispositivos são frequentemente considerados os mais sensíveis da rede, pois contêm senhas com hash para todas as contas de usuário no ambiente.

# Group Policy Objects (GPO)
O Windows gerencia essas políticas por meio de Objetos de Política de Grupo (GPOs). GPOs são um conjunto de configurações que podem ser aplicadas às UOs. GPOs podem conter políticas direcionadas a usuários ou computadores, permitindo que você defina uma linha de base para máquinas e identidades específicas.



