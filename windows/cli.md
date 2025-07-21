# Troubleshoot de rede
## ping
Uma tarefa comum de solução de problemas é verificar se o servidor consegue acessar um servidor específico na internet. A sintaxe do comando é ```ping destino```. Inspirado no pingue-pongue, enviamos um pacote ICMP específico e aguardamos uma resposta. Se uma resposta for recebida, sabemos que podemos alcançar o alvo e que o alvo pode nos alcançar.

## tracert
Outra ferramenta valiosa para solução de problemas é o tracert, que significa trace route (rota de rastreamento). O comando ```tracert destino``` rastreia a rota de rede percorrida para atingir o destino. Sem entrar em mais detalhes, ele espera que os roteadores no caminho nos notifiquem se descartarem um pacote porque seu tempo de vida (TTL) chegou a zero.

## nslookup
Um comando de rede que vale a pena conhecer é o ```nslookup```. Ele procura um host ou domínio e retorna seu endereço IP. A sintaxe ```nslookup example.com``` pesquisará example.com usando o servidor de nomes padrão; no entanto, o ```nslookup example.com 1.1.1.1``` usará o servidor de nomes one.one.one.one.

## netstat 
Este comando exibe as conexões de rede atuais e as portas de escuta. Um comando netstat básico, sem argumentos, mostrará as conexões estabelecidas.
