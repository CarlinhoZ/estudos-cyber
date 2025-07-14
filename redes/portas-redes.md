## Portas de rede
Quando uma conexão é estabelecida, quaisquer dados enviados ou recebidos por um dispositivo serão enviados por essas portas. Em computação, portas são um valor numérico entre 0 e 65535.
Como as portas podem variar de 0 a 65535, rapidamente corre-se o risco de perder o controle de qual aplicativo está usando qual porta, por isso associamos aplicativos, softwares e comportamentos a um conjunto padrão de regras.
Por exemplo, ao impor que todos os dados do navegador web sejam enviados pela porta 80, os desenvolvedores de software podem projetar um navegador web como o Google Chrome ou o Firefox para interpretar os dados da mesma forma.

Isso significa que todos os navegadores agora compartilham uma regra comum: os dados são enviados pela porta 80. A aparência, a experiência e a facilidade de uso dos navegadores dependem do designer ou da decisão do usuário.
Embora a regra padrão para dados web seja a porta 80, alguns outros protocolos receberam uma regra padrão. **Qualquer porta entre 0 e 1024 (1.024) é conhecida como porta comum.**

### Portas comuns

**FTP 21**[^1]
**SSH 22**[^2]
**HTTP 80**[^3]
**HTTPS 443**[^4]
**SMB 445**[^5]
**RDP 3389**[^6]

Vale ressaltar que esses protocolos seguem apenas os padrões. Ou seja, você pode administrar aplicativos que interagem com esses protocolos em uma porta diferente da padrão (executando um servidor web na porta 8080 em vez da porta padrão 80). Observe, no entanto, que os aplicativos presumirão que o padrão está sendo seguido, portanto, você precisará inserir dois pontos (:) junto com o número da porta.

[^1]: O File Transfer Protocol (FTP) é um protocolo desenvolvido para auxiliar na transferência eficiente de arquivos entre sistemas diferentes e até mesmo incompatíveis. Ele suporta dois modos de transferência de arquivos: binário e ASCII (texto). É usado por um aplicativo de compartilhamento de arquivos criado em um modelo cliente-servidor, o que significa que você pode baixar arquivos de um local central.
[^2]: Secure Shell (SSH) refere-se a um protocolo de rede criptográfico usado na comunicação segura entre dispositivos. O SSH criptografa dados usando algoritmos criptográficos, como o Advanced Encryption System (AES), e é frequentemente usado para fazer login remotamente em um computador ou servidor. É usado para efetuar login com segurança em sistemas por meio de uma interface baseada em texto para gerenciamento.
[^3]: O HyperText Transfer Protocol (HTTP) é o protocolo que especifica como um navegador e um servidor se comunicam. Seu navegador solicita conteúdo de um servidor usando o protocolo HTTP conforme você navega.
[^4]: O HyperText Transfer Protocol Secure (HTTPS) faz a mesma coisa que o protocolo HTTP, porém utilizando encripitação segura.
[^5]: Este protocolo é semelhante ao FTP; no entanto, além de arquivos, o SMB permite que você compartilhe dispositivos como impressoras.
[^6]: O Remote Desktop Protocol (RDP) é um meio seguro de efetuar login em um sistema usando uma interface de desktop visual. 

