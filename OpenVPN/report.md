OpenVPN - Full Report

Objetivo
Aprender a configurar e usar conexões VPN com OpenVPN para acessar redes seguras e máquinas em laboratórios como o TryHackMe.

🛠️ Ferramentas Utilizadas
Ferramenta	Comando Exemplo			Finalidade
OpenVPN		sudo openvpn arquivo.ovpn	Estabelece conexão VPN
ifconfig	ifconfig tun0			Verifica interface VPN
ping		ping 10.10.10.10		Testa conectividade com alvo


🔍 Passo a Passo Detalhado
1. Instalação do OpenVPN

No Linux:
sudo apt update && sudo apt install openvpn -y

No Windows:
Baixe o instalador em https://openvpn.net/

2. Configuração Inicial
Baixe o arquivo .ovpn do TryHackMe (em "Access" no lab)

Inicie a conexão:
sudo openvpn arquivo.ovpn

Saída esperada:
Initialization Sequence Completed

3. Verificação da Conexão

Comando:
ifconfig tun0

Saída importante:
tun0: flags=4305<UP,POINTOPOINT,RUNNING>  
inet 10.8.0.2  netmask 255.255.0.0
	10.8.0.2 é seu IP na VPN

4. Teste de Conectividade
Comando:
ping -c 4 10.10.10.10

Resultado:
64 bytes from 10.10.10.10: icmp_seq=1 ttl=63 time=45.2 ms
→ Se receber respostas, a VPN está funcionando!

💻 Exercício Prático
Cenário: Conectar-se a uma máquina alvo via VPN:

Inicie a VPN:
sudo openvpn THM.ovpn


Escaneie a rede:
nmap -sn 10.10.0.0/24


🏆 Artefatos Coletados
Tipo		Comando usado		Informação obtida
Interface VPN	ifconfig tun0		IP atribuído (10.8.0.2)
Conexão		ping 10.10.10.10	Latência e conectividade


💡 Lições Aprendidas
VPNs são túneis seguros para acessar redes remotas.
Sempre verifique o IP com ifconfig/ip a.
Problemas comuns:
	Arquivo .ovpn corrompido → Baixe novamente
	Sem internet → sudo systemctl restart network-manager