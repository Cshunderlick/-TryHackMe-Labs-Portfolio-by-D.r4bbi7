Industrial Intrusion (Medium) - Full Report (Versão Didática)

Objetivo
Aprender sobre os riscos de segurança em ambientes industriais (ICS/SCADA) e como sistemas críticos podem ser comprometidos.

🏭 Conceitos Fundamentais

1. O que são Sistemas Industriais?
ICS (Industrial Control Systems): Controlam processos industriais (ex: usinas, fábricas)
SCADA (Supervisory Control And Data Acquisition): Software de supervisão industrial

Exemplo de arquitetura vulnerável:
PLC (Programmable Logic Controller) ←→ HMI (Human-Machine Interface) ←→ Rede Corporativa

🔧 Ferramentas e Técnicas de Ataque

1. Enumeração de Dispositivos

Comando com Nmap:
nmap -sU -p 161,102 192.168.1.1/24  # Varredura UDP em portas industriais

	Porta 161: SNMP (geralmente mal configurado)
	Porta 102: Protocolo industrial IEC 61850

2. Exploração de PLCs

Ferraramenta: modbus-cli
modbus read 192.168.1.100 1 0 10  # Lê 10 registros do PLC


3. Ataque a Protocolos Industriais

Exemplo com Metasploit:
use auxiliary/scanner/scada/modbusdetect
set RHOSTS 192.168.1.100
run


💀 Casos Reais de Ataques
Stuxnet (2010): Malware que danificou centrifugadoras nucleares iranianas
Triton (2017): Ataque a sistema de segurança de usina química

🛡️ Técnicas de Defesa

Segmentação de Rede:
iptables -A FORWARD -p tcp --dport 102 -j DROP  # Bloqueia tráfego industrial na rede corporativa

Monitoramento Especializado
Ferramentas: Siemens SINEC IDS, Nozomi Networks

🧪 Exercício Prático
Simular proteção de PLC

Criar regra para restringir acesso:
iptables -A INPUT -s 192.168.1.50 -p tcp --dport 502 -j ACCEPT  # Permite apenas HMI específico

Testar conexão:
nc -zv 192.168.1.100 502

📌 Lições Aprendidas
Sistemas industriais são alvos valiosos (impacto físico real)
Muitos usam protocolos inseguros por padrão (Modbus, DNP3)
Defesa requer equipe especializada (TI industrial ≠ TI corporativo)