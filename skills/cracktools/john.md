# Básico do John the Ripper

```john [opções] [caminho do arquivo]```

john: faz um request do programa
[opções]: Especifica as opções que você deseja usar
[caminho do arquivo]: O arquivo que contém o hash que você está tentando quebrar; se estiver no mesmo diretório, você não precisará nomear um caminho, apenas o arquivo.

## Quebra Automática
O John possui recursos integrados para detectar o tipo de hash que está sendo fornecido e selecionar regras e formatos apropriados para quebrá-lo para você; isso nem sempre é a melhor ideia, pois pode não ser confiável, mas se você não consegue identificar com qual tipo de hash está trabalhando e quer tentar quebrá-lo, pode ser uma boa opção! Para fazer isso, usamos a seguinte sintaxe:

```john --wordlist=[caminho para a lista de palavras] [caminho para o arquivo]```

* --wordlist=: Especifica o uso do modo de lista de palavras, lendo o arquivo que você fornece no caminho fornecido
* [caminho para a lista de palavras]: O caminho para a lista de palavras que você está usando
Exemplo de uso:

```john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt```

## Identificando Hashes
Há várias maneiras de fazer isso, como usar um identificador de hash online. Outra opção é o [hash-identifier](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master).
Para usar o [hash-identifier](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master), você pode usar ```wget``` ou ```curl``` para baixar o arquivo Python ```hash-id.py``` da página no GitHub. Em seguida, execute-o com ```python3 hash-id.py``` e insira o hash que você está tentando identificar. Ele fornecerá uma lista dos formatos mais prováveis. 

```wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py```

# Cracking de Formato Específico
Depois de identificar o hash, podemos usar o John para crackear o hash fornecido usando a seguinte sintaxe:

```john --format=raw-[formato] --wordlist=[caminho para a lista de palavras] [caminho para o arquivo]```

* --format=: Este é o sinalizador para informar a John que você está atribuindo um hash de um formato específico e para usar o seguinte formato para crackeá-lo
* [formato]: O formato do hash

Exemplo de Uso:

```john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt```

```
Uma Observação sobre Formatos:

Ao instruir John a usar formatos, se estiver lidando com um tipo de hash padrão, por exemplo, md5 como no exemplo acima, você precisa prefixá-lo com raw- para informar a John que está lidando apenas com um tipo de hash padrão, embora isso nem sempre se aplique. Para verificar se você precisa adicionar o prefixo ou não, você pode listar todos os formatos de John usando john --list=formats e verificar manualmente ou usar grep para seu tipo de hash usando algo como john --list=formats | grep -iF "md5".
```

## NTHash / NTLM
NThash é o formato de hash que as máquinas modernas com o sistema operacional Windows usam para armazenar senhas de usuários e serviços. Também é comumente chamado de NTLM, que faz referência à versão anterior do formato do Windows para hash de senhas, conhecido como LM, portanto, NT/LM.

No Windows, o SAM (Gerenciador de Contas de Segurança) é usado para armazenar informações de contas de usuários, incluindo nomes de usuários e senhas com hash. Você pode obter hashes NTHash/NTLM instalando o banco de dados SAM em uma máquina Windows, usando uma ferramenta como o ```Mimikatz``` ou usando o banco de dados do Active Directory: NTDS.dit. Talvez você não precise quebrar o hash para continuar a escalada de privilégios, pois muitas vezes é possível realizar um ataque de "passar o hash", mas, às vezes, quebrar o hash é uma opção viável se houver uma política de senhas fraca.

# ect/shadow
O arquivo /etc/shadow é o arquivo em máquinas Linux onde os hashes de senha são armazenados. Ele também armazena outras informações, como a data da última alteração de senha e informações de expiração de senha. Ele contém uma entrada por linha para cada usuário ou conta de usuário do sistema. Este arquivo geralmente é acessível apenas pelo usuário root, portanto, você deve ter privilégios suficientes para acessar os hashes. No entanto, se você tiver, há uma chance de conseguir quebrar alguns dos hashes.

```unshadow [caminho para a senha] [caminho para a sombra]```

```
unshadow: Invoca a ferramenta unshadow
[caminho para a senha]: O arquivo que contém a cópia do arquivo /etc/passwd que você obteve da máquina de destino
[caminho para a sombra]: O arquivo que contém a cópia do arquivo /etc/shadow que você obteve da máquina de destino
```

# Usando o Single Crack Mode
Para usar o modo Single Crack Mode, usamos praticamente a mesma sintaxe que usamos até agora; por exemplo, se quiséssemos quebrar a senha do usuário "Mike", usando o modo de quebra única, usaríamos:

```john --single --format=[formato] [caminho para o arquivo]```

* --single: Este sinalizador informa a John que você deseja usar o modo de quebra de hash única
* --format=[formato]: Como sempre, é vital identificar o formato correto.

Exemplo de Uso:

```john --single --format=raw-sha256 hashes.txt```

```
Uma Observação sobre Formatos de Arquivo no Modo de Quebra Única:

Se você estiver quebrando hashes no modo de quebra única, precisará alterar o formato do arquivo que está alimentando John para que ele entenda a partir de quais dados criar uma lista de palavras.
Para fazer isso, adicione ao hash o nome de usuário ao qual ele pertence. Assim, de acordo com o exemplo acima, alteraríamos o arquivo hashes.txt.

De 1efee03cdcb96d90ad48ccc7b8666033

Para mike:1efee03cdcb96d90ad48ccc7b8666033
```


















