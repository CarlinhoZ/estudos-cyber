# Descoberta de Host
O Nmap utiliza várias maneiras de especificar seus alvos:

* Intervalo de IP usando -: Se você deseja escanear todos os endereços IP de 192.168.0.1 a 192.168.0.10, você pode escrever 192.168.0.1-10
* Sub-rede IP usando /: Se você deseja escanear uma sub-rede, você pode expressá-la como 192.168.0.1/24, o que seria equivalente a 192.168.0.0-255
* Nome do host: Você também pode especificar seu alvo pelo nome do host, por exemplo, example.thm

Digamos que você queira descobrir os hosts online em uma rede. O Nmap oferece a opção -sn, ou seja, ping scan.

Executar o Nmap como um usuário local (não root) limitaria a tipos fundamentais de varredura, como varreduras de eco ICMP e varreduras de conexão TCP.

# Varredura de uma Rede "Local"
Supondo que meu endereço IP é 192.168.66.89, vamos varrer a rede 192.168.66.0/24. O comando é:```nmap -sn 192.168.66.0/24```.













