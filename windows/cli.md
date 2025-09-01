# Troubleshoot de rede
## ping
Uma tarefa comum de solução de problemas é verificar se o servidor consegue acessar um servidor específico na internet. A sintaxe do comando é ```ping destino```. Inspirado no pingue-pongue, enviamos um pacote ICMP específico e aguardamos uma resposta. Se uma resposta for recebida, sabemos que podemos alcançar o alvo e que o alvo pode nos alcançar.

## tracert
Outra ferramenta valiosa para solução de problemas é o tracert, que significa trace route (rota de rastreamento). O comando ```tracert destino``` rastreia a rota de rede percorrida para atingir o destino. Sem entrar em mais detalhes, ele espera que os roteadores no caminho nos notifiquem se descartarem um pacote porque seu tempo de vida (TTL) chegou a zero.

## nslookup
Um comando de rede que vale a pena conhecer é o ```nslookup```. Ele procura um host ou domínio e retorna seu endereço IP. A sintaxe ```nslookup example.com``` pesquisará example.com usando o servidor de nomes padrão; no entanto, o ```nslookup example.com 1.1.1.1``` usará o servidor de nomes one.one.one.one.

## icacls
```icacls "C:\System Volume Information" /grant "Administrators:F"```
Exemplod de comando para ajustar permissão na pasta, garantindo acesso.

## netstat 
Este comando exibe as conexões de rede atuais e as portas de escuta. Um comando netstat básico, sem argumentos, mostrará as conexões estabelecidas.

# Navegando por pastas
## cd & dir
O comando ```cd``` é clássico, serve para mudar de diretório. Junto a ele, pode-se usar o ```dir``` nos mostra onde estamos atualmente.
* dir /a - Exibe também arquivos ocultos e de sistema.
* dir /s - Exibe arquivos no diretório atual e em todos os subdiretórios.

Pode-se digitar ```tree``` para representar visualmente os diretórios e subdiretórios filhos.

## rmdir & mkdir
* Para criar um diretório, use ```mkdir nome_do_diretório```; mkdir significa criar diretório.
* Para excluir um diretório, use ```rmdir nome_do_diretório```; rmdir significa remover diretório.

# Trabalhando com arquivos
Você pode visualizar arquivos de texto facilmente com o comando ```type```. Este comando exibirá o conteúdo do arquivo de texto na tela; isso é conveniente para arquivos que cabem na janela do seu terminal. Você pode considerar usar ```more``` para arquivos de texto mais longos. Este comando exibirá conteúdo de arquivo de texto suficiente para preencher a janela do seu terminal. Em outras palavras, para arquivos de texto longos, ```more``` exibirá uma única página e aguardará que você pressione a barra de espaço para mover uma página (virar a página) ou Enter para mover uma linha.

O comando ```copy``` permite copiar arquivos de um local para outro.
Você pode mover arquivos usando o comando ```move```.

Para excluir um arquivo usamos ```del``` ou ```erase```.

Podemos usar o caractere curinga ```*``` para se referir a vários arquivos. Por exemplo, copy *.md C:\Markdown copiará todos os arquivos com a extensão md para o diretório C:\Markdown.

# Processos e Tarefas
Digamos que queremos procurar tarefas relacionadas a ```sshd.exe```. Podemos fazer isso com o comando ```tasklist /FI "imagename eq sshd.exe"```. O parâmtro ```/FI``` é usado para definir o nome da imagem do filtro como sshd.exe.
Com o ID do processo (PID) conhecido, podemos encerrar qualquer tarefa usando ```taskkill /PID target_pid```. Por exemplo, se quisermos encerrar o processo com PID 4567, emitiríamos o comando ```taskkill /PID 4567```.









