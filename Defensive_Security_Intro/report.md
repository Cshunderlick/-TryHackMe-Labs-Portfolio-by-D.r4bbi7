Defensive Security Intro - Full Report

Objetivo
Entender os conceitos básicos de segurança defensiva e como proteger sistemas contra ataques cibernéticos.

Principais Conceitos Estudados

🔒 1. Os 3 Pilares da Segurança (CIA Triad)

Confidencialidade: Garantir que apenas pessoas autorizadas acessem informações
Exemplo: Criptografia de arquivos sensíveis
Ferramenta: gpg -c arquivo.txt (criptografa com senha)

Integridade: Manter os dados precisos e completos
Exemplo: Verificação de hash de arquivos
Comando:
sha256sum arquivo.iso  # Gera hash do arquivo

Disponibilidade: Garantir que sistemas estejam acessíveis quando necessário
Exemplo: Proteção contra ataques DDoS

🛡️ 2. Técnicas de Defesa Básicas

Firewalls
# Exemplo de regras básicas com iptables (Linux)
iptables -A INPUT -p tcp --dport 22 -j DROP  # Bloqueia SSH
iptables -A INPUT -p tcp --dport 80 -j ACCEPT  # Permite HTTP

Por que importa?:
Filtra tráfego indesejado
Bloqueia portas desnecessárias

IDS/IPS (Sistemas de Detecção/Prevenção de Intrusão)
Snort (IDS open-source):
snort -A console -q -c /etc/snort/snort.conf

Backups
Comando útil:
tar -czvf backup.tar.gz /dados_importantes  # Compacta arquivos

🕵️ 3. Monitoramento e Análise
Logs do Sistema
# Visualizar logs de autenticação (Linux)
tail -f /var/log/auth.log
# Windows: Event Viewer -> Security logs

SIEM (Security Information and Event Management)
Ferramentas populares: Splunk, Wazuh, Graylog
Exemplo de regra:
Alerta se >5 falhas de login SSH em 2 minutos

🚨 4. Resposta a Incidentes
Passos básicos:
Identificação: Detectar a anomalia
Contenção: Isolar sistemas afetados
	Exemplo: ifconfig eth0 down (desliga interface de rede)
Eradicação: Remover malware/ameaças
Recuperação: Restaurar sistemas
Lições aprendidas: Documentar o incidente

Exercício Prático

Simular análise de logs:
Gerar log suspeito:
echo "Failed password for root from 192.168.1.100" >> /var/log/auth.log

Analisar tentativas falhas:
grep "Failed password" /var/log/auth.log


Lições Aprendidas
Segurança não é só ferramentas - é sobre processos e pessoas
Defesa requer monitoramento constante
Backup é sua última linha de defesa contra ransomware