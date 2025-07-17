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
