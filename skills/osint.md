# Operadores de Busca

## operadores de busca suportados pelo Google.

* "frase exata": Aspas duplas indicam que você está procurando páginas com a palavra ou frase exata. Por exemplo, pode-se pesquisar por "reconhecimento passivo" para obter páginas com essa frase exata.

* site:: Este operador permite especificar o nome de domínio ao qual você deseja limitar sua busca. Por exemplo, ```site:tryhackme.com access```

* -: O sinal de menos permite omitir resultados de busca que contenham uma palavra ou frase específica. Por exemplo, você pode estar interessado em aprender sobre as pirâmides, mas não quer visualizar sites de turismo; uma abordagem é pesquisar por pirâmides - turismo ou - pirâmides de turismo.

* filetype:: Este operador de busca é indispensável para encontrar arquivos em vez de páginas da web. Alguns dos tipos de arquivo que você pode pesquisar usando o Google são Portable Document Format (PDF), Microsoft Word, Microsoft Excel e Microsoft PowerPoint. Por exemplo, para encontrar apresentações sobre segurança cibernética, tente pesquisar por filetype:ppt cyber security.

[Lista de operadores de busca avançada do Google](https://github.com/cipher387/Advanced-search-operators-list)

# Mecanismo de Busca Personalizado

## Shodan
O [Shodan](https://www.shodan.io) é um mecanismo de busca para dispositivos conectados à internet. Ele permite que você pesquise por tipos e versões específicos de servidores, equipamentos de rede, sistemas de controle industrial e dispositivos de IoT. Você pode querer ver quantos servidores ainda estão executando o Apache 2.4.1 e a distribuição entre os países. Para encontrar a resposta, podemos pesquisar por apache 2.4.1, que retornará a lista de servidores com a string "apache 2.4.1" em seus cabeçalhos.

## Censys
O Shodan se concentra em dispositivos e sistemas conectados à Internet, como servidores, roteadores, webcams e dispositivos IoT. O [Censys](https://search.censys.io), por outro lado, concentra-se em hosts, sites, certificados e outros ativos da Internet conectados à Internet. Alguns de seus casos de uso incluem enumeração de domínios em uso, auditoria de portas e serviços abertos e descoberta de ativos não autorizados em uma rede.
[Documentação oficial do Censys](https://docs.censys.com/docs/ls-introductory-use-cases#/)

## Virus Total
O [VirusTotal](https://www.virustotal.com/gui/home/upload) é um site online que oferece um serviço de verificação de vírus para arquivos usando vários mecanismos antivírus. Ele permite que os usuários carreguem arquivos ou forneçam URLs para escaneá-los em diversos mecanismos antivírus e scanners de sites em uma única operação. Eles podem até mesmo inserir hashes de arquivo para verificar os resultados de arquivos carregados anteriormente.

## Have I Been Pwned
O [Have I Been Pwned (HIBP)](https://haveibeenpwned.com) faz uma coisa: informa se um endereço de e-mail apareceu em um vazamento de dados. Encontrar o e-mail de alguém em dados vazados indica vazamento de informações privadas e, mais importante, senhas. Muitos usuários usam a mesma senha em várias plataformas; se uma plataforma for violada, suas senhas em outras plataformas também serão expostas. De fato, as senhas geralmente são armazenadas em formato criptografado; no entanto, muitas senhas não são tão complexas e podem ser recuperadas por meio de uma variedade de ataques.

# Exploits e Vulnerabilidades

## CVE
O Common Vulnerabilities and Exposures (CVE) é como um dicionário de vulnerabilidades. Ele fornece um identificador padronizado para vulnerabilidades e problemas de segurança em produtos de software e hardware. Cada vulnerabilidade recebe um ID CVE com um formato padronizado, como [CVE-2024-29988](https://nvd.nist.gov/vuln/detail/CVE-2024-29988). Esse identificador exclusivo (ID CVE) garante que todos, desde pesquisadores de segurança até fornecedores e profissionais de TI, estejam se referindo à mesma vulnerabilidade, [CVE-2024-29988](https://nvd.nist.gov/vuln/detail/CVE-2024-29988) neste caso.

## Exploit Database
O [Exploit Database](https://www.exploit-db.com/) lista códigos de exploração de vários autores; alguns desses códigos de exploração são testados e marcados como verificados.














