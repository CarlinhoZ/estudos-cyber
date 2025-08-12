# O que é uma Assinatura Digital?
As assinaturas digitais fornecem uma maneira de verificar a autenticidade e a integridade de uma mensagem ou documento digital. Comprovar a autenticidade de arquivos significa que sabemos quem os criou ou modificou. Usando a criptografia assimétrica, você produz uma assinatura com sua chave privada, que pode ser verificada usando sua chave pública. Somente você deve ter acesso à sua chave privada, que comprova que você assinou o arquivo. Em muitos países modernos, as assinaturas digitais e físicas têm o mesmo valor legal.

A forma mais simples de assinatura digital é criptografar o documento com sua chave privada. Se alguém quiser verificar essa assinatura, deverá descriptografá-la com sua chave pública e verificar se os arquivos correspondem.

Alguns artigos usam termos como assinatura eletrônica e assinatura digital de forma intercambiável. Eles se referem à colagem de uma imagem de uma assinatura sobre um documento. Essa abordagem não comprova a integridade do documento, pois qualquer pessoa pode copiar e colar uma imagem.

<img width="508" height="291" alt="image" src="https://github.com/user-attachments/assets/e6e41968-d84f-4507-a786-096ce1287960" />

O termo correto para assinatura digital é assinar um documento usando uma chave privada ou um certificado. Esse processo é semelhante à imagem mostrada acima, onde Bob criptografa um hash de seu documento e o compartilha com Alice, juntamente com o documento original. Alice pode descriptografar o hash criptografado e compará-lo com o hash do arquivo que recebeu. Essa abordagem comprova a integridade do documento, diferentemente de colar uma imagem sofisticada de uma assinatura. 

# O que são certificados?

Certificados são uma aplicação essencial da criptografia de chave pública e também estão vinculados a assinaturas digitais. Um local comum onde eles são usados é para HTTPS. Como seu navegador sabe que o servidor com o qual você está se comunicando é o verdadeiro?

A resposta está nos certificados. O servidor web possui um certificado que afirma ser o verdadeiro website. Os certificados têm uma cadeia de confiança, começando com uma **CA raiz (Autoridade Certificadora)**. Desde o momento da instalação, seu dispositivo, sistema operacional e navegador confiam automaticamente em várias CAs raiz. Os certificados são confiáveis somente quando as CAs raiz afirmam confiar na organização que os assinou. De certa forma, é uma cadeia; por exemplo, o certificado é assinado por uma organização, a organização é confiável para uma CA e a CA é confiável para seu navegador. Portanto, seu navegador confia no certificado. Em geral, existem longas cadeias de confiança. Você pode conferir as autoridades certificadoras confiáveis do Mozilla Firefox aqui e do Google Chrome aqui.

Digamos que você tenha um site e queira usar HTTPS. Esta etapa requer um certificado TLS. Você pode obtê-lo de diversas autoridades certificadoras por uma taxa anual. Além disso, você pode obter seus próprios certificados TLS para domínios de sua propriedade usando o ```Let's Encrypt``` gratuitamente!! Se você administra um site, vale a pena configurar e migrar para HTTPS, como qualquer site moderno faria.

# PGP e GPG
PGP significa Pretty Good Privacy (Privacidade Muito Boa). É um software que implementa criptografia para criptografar arquivos, realizar assinaturas digitais e muito mais. [GnuPG ou GPG](https://gnupg.org/) é uma implementação de código aberto do padrão OpenPGP.
O GPG é comumente usado em e-mails para proteger a confidencialidade das mensagens. Além disso, pode ser usado para assinar uma mensagem de e-mail e confirmar sua integridade.

Você pode precisar usar o GPG para descriptografar arquivos em CTFs. Com o PGP/GPG, as chaves privadas podem ser protegidas com senhas, de forma semelhante à proteção das chaves privadas SSH. Se a chave for protegida por senha, você pode tentar quebrá-la usando John the Ripper e gpg2john. A chave fornecida nesta tarefa não é protegida por senha.

## Exemplo Prático

Agora que você tem seu par de chaves GPG, pode compartilhar a chave pública com seus contatos. Sempre que seus contatos quiserem se comunicar com segurança, eles criptografarão as mensagens que enviarem a você usando sua chave pública. Para descriptografar a mensagem, você precisará usar sua chave privada. Devido à importância das chaves GPG, é vital que você mantenha uma cópia de segurança em um local seguro.

Digamos que você comprou um computador novo. Tudo o que você precisa fazer é importar sua chave e começar a descriptografar as mensagens recebidas novamente:

Você usaria gpg --import backup.key para importar sua chave de backup.key.
Para descriptografar suas mensagens, você precisa executar gpg --decrypt confidential_message.gpg.

# O que é uma Função Hash?
Funções hash são diferentes de criptografia. Não há chave e é suposto ser impossível (ou computacionalmente impraticável) retornar da saída para a entrada.

Uma função hash recebe dados de entrada de qualquer tamanho e cria um resumo ou resumo desses dados. A saída tem um tamanho fixo. É difícil prever a saída para qualquer entrada e vice-versa. Bons algoritmos de hash serão relativamente rápidos para calcular e proibitivamente lentos para reverter, ou seja, partir da saída e determinar a entrada. Qualquer pequena alteração nos dados de entrada, mesmo que seja um único bit, deve causar uma alteração significativa na saída.

Quando você faz um login, o servidor usa o hashing para verificar sua senha. Na verdade, de acordo com as boas práticas de segurança, um servidor não registra sua senha; ele registra o valor de hash da sua senha. Sempre que você quiser fazer login, ele calculará o valor de hash da senha que você enviou com o valor de hash registrado. Da mesma forma, quando você faz login no seu computador, o hashing desempenha um papel na verificação da sua senha. Você interage com o hashing de forma mais indireta do que imagina, e quase diariamente no contexto de senhas.

# O que é uma Colisão de Hash?
Uma colisão de hash ocorre quando duas entradas diferentes geram a mesma saída. As funções de hash são projetadas para evitar colisões da melhor forma possível. Além disso, as funções de hash são projetadas para impedir que um invasor crie, ou seja, planeje, uma colisão intencionalmente. No entanto, como o número de entradas é praticamente ilimitado e o número de saídas possíveis é limitado, isso leva a um efeito de casa de pombo.

Como exemplo numérico, se uma função de hash produz um valor de hash de 4 bits, temos apenas 16 valores de hash diferentes. O número total de valores de hash possíveis é 2número_de_bits = 24 = 16. A probabilidade de uma colisão é relativamente alta.

O efeito de casa de pombo afirma que o número de itens (pombos) é maior que o número de contêineres (casas de pombo); alguns contêineres devem conter mais de um item. Em outras palavras, neste contexto, há um número fixo de valores de saída diferentes para a função hash, mas você pode fornecer qualquer tamanho de entrada. Como há mais entradas do que saídas, algumas entradas inevitavelmente fornecem a mesma saída. Se você tiver 21 pombos e 16 compartimentos, alguns dos pombos compartilharão os compartimentos. Consequentemente, colisões são inevitáveis. No entanto, uma boa função hash garante que a probabilidade de uma colisão seja insignificante.

MD5 e SHA1 foram atacados e agora são considerados inseguros devido à capacidade de projetar colisões de hash. No entanto, nenhum ataque ainda gerou uma colisão em ambos os algoritmos simultaneamente, portanto, se você comparar os hashes MD5 e SHA1, verá que eles são diferentes. Você pode ver o exemplo de colisão MD5 na [página de demonstração de colisão MD5](https://www.mscs.dal.ca/~selinger/md5collision/); além disso, você pode ler os detalhes do ataque de colisão SHA1 no [Shattered](https://shattered.io/). Devido a isso, você não deve confiar em nenhum dos algoritmos para fazer hash de senhas ou dados.

# Práticas inseguras de armazenamento de senhas
A RockYou, uma empresa que desenvolvia aplicativos e widgets para mídias sociais, armazenavam suas senhas em texto simples, e a empresa sofreu uma violação de dados. O arquivo de texto contém mais de 14 milhões de senhas. 

A notável violação de dados da Adobe foi um pouco diferente. Em vez de usar uma função de hash segura para armazenar os valores de hash das senhas, a empresa utilizou um formato de criptografia obsoleto. Além disso, as dicas de senha eram armazenadas em texto simples, às vezes contendo a própria senha. Consequentemente, a senha em texto simples podia ser recuperada com relativa rapidez.

O LinkedIn também sofreu uma violação de dados em 2012. O LinkedIn utilizou um algoritmo de hash inseguro, o SHA-1, para armazenar as senhas dos usuários. Além disso, não foi utilizado o método de "salting" de senha. "salting" de senha refere-se à adição de um "salt", ou seja, um valor aleatório, à senha antes de ela ser hash.

# Usando Hashing para Armazenar Senhas
É aqui que entra o hashing. E se, em vez de armazenar a senha, você apenas armazenasse o valor do hash usando uma função de hash segura? Esse processo significa que você nunca precisará armazenar a senha do usuário e, se o seu banco de dados vazar, um invasor terá que quebrar cada senha para descobrir qual era a senha.

Só há um problema com isso. E se dois usuários tiverem a mesma senha? Como uma função de hash sempre transformará a mesma entrada na mesma saída, você armazenará o mesmo hash de senha para cada usuário. Isso significa que, se alguém quebrar esse hash, terá acesso a mais de uma conta. Isso também significa que alguém pode criar uma Rainbow Tables para quebrar os hashes.

Uma Rainbow Tables é uma tabela de consulta de hashes para textos simples, para que você possa descobrir rapidamente qual senha um usuário tinha a partir do hash. Uma Rainbow Table troca o tempo para quebrar um hash por espaço em disco, mas leva tempo para ser criada.

Sites como [CrackStation](https://crackstation.net/) e [Hashes.com](https://hashes.com/en/decrypt/hash) usam internamente tabelas de arco-íris enormes para fornecer quebra rápida de senhas para hashes sem salts. Fazer uma busca em uma lista ordenada de hashes é mais rápido do que tentar quebrar o hash.

# Proteção contra Rainbow Tables
Para proteção contra rainbow tables, adicionamos um salt às senhas. O salt é um valor gerado aleatoriamente e armazenado no banco de dados, que deve ser exclusivo para cada usuário. Em teoria, você poderia usar o mesmo salt para todos os usuários, mas senhas duplicadas ainda teriam o mesmo hash, e uma rainbow table ainda poderia ser criada para senhas com esse salt.

O salt é adicionado ao início ou ao final da senha antes do hash, o que significa que cada usuário terá um hash de senha diferente, mesmo que tenha a mesma senha. Funções de hash como Bcrypt e Scrypt lidam com isso automaticamente. Os salts não precisam ser mantidos em sigilo.

# Exemplo de Armazenamento Seguro de Senhas
Considere este exemplo de boas práticas de segurança ao armazenar senhas de usuários:

* Selecionamos uma função de hash segura, como Argon2, Scrypt, Bcrypt ou PBKDF2.
* Adicionamos um salt exclusivo à senha, como ```Y4UV*^(=go_!```
* Concatenamos a senha com o salt exclusivo. Por exemplo, se a senha for AL4RMc10k, a string resultante será ```AL4RMc10kY4UV*^(=go_!```
* Calculamos o valor de hash da senha e do salt combinados. Neste exemplo, usando o algoritmo escolhido, calculamos o valor de hash de ```AL4RMc10kY4UV*^(=go_!```.
* Armazenamos o valor de hash e o salt exclusivo utilizado ```(Y4UV*^(=go_!)```.

# Reconhecimento de hash de senha
Se começarmos com um hash, como podemos reconhecer seu tipo, eventualmente quebrá-lo e recuperar a senha original?

Ferramentas automatizadas de reconhecimento de hash, como o [hashID](https://pypi.org/project/hashID/), existem, mas não são confiáveis para muitos formatos. Para hashes com prefixo, as ferramentas são confiáveis. **Usamos uma combinação adequada de contexto e ferramentas**. **Se você encontrar o hash em um banco de dados de aplicativo web, é mais provável que seja MD5 do que NTLM (NT LAN Manager)**. Ferramentas automatizadas de reconhecimento de hash frequentemente confundem esses tipos de hash, destacando a importância de aprender por conta própria.

# Senhas do Linux
No Linux, os hashes de senha são armazenados em /etc/shadow, que normalmente só pode ser lido pelo root. Anteriormente, eles eram armazenados em /etc/passwd, que era legível por todos.

O arquivo shadow contém as informações da senha. Cada linha contém nove campos, separados por dois pontos (:). Os dois primeiros campos são o nome de login e a senha criptografada. Mais informações sobre os outros campos podem ser encontradas executando man 5 shadow em um sistema Linux.

O campo de senha criptografada contém a senha com hash com quatro componentes: prefixo (id do algoritmo), opções (parâmetros), salt e hash. Ela é salva no formato $prefixo$opções$salt$hash. O prefixo facilita o reconhecimento de senhas no estilo Unix e Linux; ele especifica o algoritmo de hash usado para gerar o hash.
Você pode ler mais sobre eles consultando a página do manual com man 5 crypt.

# Senhas no Windows

No Windows, os hashes de senha são armazenados no SAM (Gerenciador de Contas de Segurança). O Windows tenta impedir que usuários comuns os descartem, mas ferramentas como o ```mimikatz``` existem para burlar a segurança do Windows. Notavelmente, os hashes encontrados lá são divididos em hashes NT e hashes LM.

Um ótimo lugar para encontrar mais formatos de hash e prefixos de senha é a página de [Hashcat Example Hashes](https://hashcat.net/wiki/doku.php?id=example_hashes). Para outros tipos de hash, normalmente você precisará verificar o comprimento ou a codificação, ou até mesmo pesquisar o aplicativo que os gerou.

# Quebra de Senhas
As tabelas rainbow são um método para quebrar hashes que não usam um salt, mas e se houver um salt envolvido?

Você não pode "decifrar" hashes de senha. Eles não são criptografados. Você precisa quebrar os hashes fazendo o hash de várias entradas diferentes (como rockyou.txt, pois ele abrange muitas senhas possíveis), potencialmente adicionando o salt, se houver, e comparando-o com o hash de destino. Assim que houver correspondência, você saberá qual era a senha. Ferramentas como [Hashcat](https://hashcat.net/wiki/doku.php?id=example_hashes) e [John the Ripper](https://www.openwall.com/john/) são comumente usadas para esses fins.






















