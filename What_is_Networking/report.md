What is Networking? - Full Report

Objetivo
Entender os conceitos fundamentais de redes de computadores que todo profissional de segurança precisa dominar.

🌐 Conceitos-Chave
1. Modelo OSI vs TCP/IP

Comparação visual:
┌─────────────────┐        ┌─────────────────┐
    	 OSI       	   	     TCP/IP       
├─────────────────┤     	 ├─────────────────┤
 7. Aplicação    	│──────▶  Aplicação      
 6. Apresentação 		     	                 
 5. Sessão       		                         
├─────────────────┤      	 ├─────────────────┤
 4. Transporte   	│──────▶  Transporte     
├─────────────────┤     	 ├─────────────────┤
 3. Rede         	│──────▶  Internet       
├─────────────────┤        ├─────────────────┤
 2. Enlace       	│──────▶  Acesso à Rede  
 1. Física       		    	                 
└─────────────────┘        └─────────────────┘


2. Protocolos Essenciais

Protocolo	Porta	Uso			Comando de Teste
HTTP		80	Navegação web		curl http://exemplo.com
HTTPS		443	Web seguro		openssl s_client -connect exemplo.com:443
SSH		22	Acesso remoto seguro	ssh user@10.10.10.10
DNS		53	Tradução de nomes	dig exemplo.com


🔧 Ferramentas Básicas de Diagnóstico

1. Verificar Conexão (ping)
ping -c 4 google.com

Saída típica:
64 bytes from 172.217.29.46: icmp_seq=1 ttl=116 time=12.3 ms

2. Rastreamento de Rota (traceroute)
traceroute example.com

Mostra:
Todos os "saltos" até o destino
Tempo entre cada roteador


3. Analisar Tráfego (tcpdump)
sudo tcpdump -i eth0 port 80 -v

Filtros úteis:
port 443: Só HTTPS
src 192.168.1.100: Tráfego de uma origem



🎯 Exercício Prático
Cenário: Identificar serviços em execução

1.Verificar portas abertas no localhost:
netstat -tuln

2.Testar conectividade DNS:
nslookup tryhackme.com


💡 Lições Aprendidas

Endereçamento IP:
	IPv4: 192.168.1.1 (32 bits)
	IPv6: 2001:0db8:85a3::8a2e:0370:7334 (128 bits)

NAT: Traduz IPs privados para públicos
[PC: 192.168.1.100] → [Roteador: 201.45.222.1] → Internet

Firewalls: Filtram tráfego por portas/IPs