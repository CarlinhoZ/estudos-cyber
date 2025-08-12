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
PGP significa Pretty Good Privacy (Privacidade Muito Boa). É um software que implementa criptografia para criptografar arquivos, realizar assinaturas digitais e muito mais. [GnuPG ou GPG]() é uma implementação de código aberto do padrão OpenPGP.

O GPG é comumente usado em e-mails para proteger a confidencialidade das mensagens. Além disso, pode ser usado para assinar uma mensagem de e-mail e confirmar sua integridade.

Abaixo, um exemplo de geração de GPG. Você será questionado sobre a finalidade do uso do GPG: se apenas assinatura ou assinatura e criptografia. Além de selecionar o algoritmo criptográfico, precisávamos escolher uma data de validade para a chave gerada. Por fim, fornecemos algumas informações sobre nós: nosso nome, endereço de e-mail e um comentário, geralmente sobre a finalidade dessa chave.
















