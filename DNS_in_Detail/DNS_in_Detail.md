✅ DNS in Detail - Full Report

Objetivo:
Compreender o funcionamento e as vulnerabilidades do sistema de nomes de domínio (DNS), utilizando técnicas de enumeração e análise de requisições DNS para identificar ativos e possíveis pontos de entrada.

🔧 Ferramentas Utilizadas:
nslookup – Consulta DNS básica.
dig – Ferramenta avançada de análise DNS.
host – Alternativa simples para resolver nomes e descobrir subdomínios.
dnsenum / dnsrecon – Enumeração de registros DNS.
whois – Coleta de informações sobre domínios.
Gobuster (modo DNS) – Descoberta de subdomínios por força bruta.


🧭 1. Descoberta de Registros DNS Básicos (nslookup / dig)

Comando:
nslookup tryhackme.com
dig tryhackme.com any

Explicação:
Consultas básicas para descobrir os registros A, NS, CNAME e MX, fundamentais para entender como o domínio é configurado.

🧠 O que aprendi?
A estrutura do domínio, incluindo quais servidores respondem por ele e possíveis aliases (CNAME).


🌐 2. Enumeração Avançada com dnsenum / dnsrecon

Comando:
dnsrecon -d tryhackme.com

Explicação:
Enumera registros como TXT, SPF, DMARC, além de buscar zonetransfer (quando habilitado acidentalmente).

🔍 Resultado relevante:
Found NS record: ns1.thm.local
Attempting zone transfer...
SUCCESS! Transferred zone: tryhackme.com

✅ Exploração:
A zona foi transferida com sucesso, revelando todos os subdomínios e registros internos. Isso é uma falha grave de configuração.


🔎 3. Descobrindo Subdomínios (Gobuster DNS)

Comando:
gobuster dns -d tryhackme.com -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt

Explicação:
Realiza força bruta de nomes DNS com wordlist, útil quando zone transfer está desabilitado.

📌 Saídas importantes:
Found: admin.tryhackme.com
Found: dev.tryhackme.com
Found: vpn.tryhackme.com

💡 Lições:
Cada subdomínio pode corresponder a um sistema isolado — com serviços e vulnerabilidades próprias.


🧾 4. Consulta de Informações WHOIS

Comando:
whois tryhackme.com

Explicação:
Consulta sobre o registro do domínio: datas, organização, servidores DNS e e-mails de contato.

📬 Uso em OSINT:
Possibilidade de descobrir e-mails de administradores ou prestadores de serviço terceirizados.

🧠 Lições Aprendidas:
🔐 Zone Transfer mal configurado pode vazar a estrutura interna completa de um domínio.
🌍 DNS é uma porta de entrada valiosa para ataque e OSINT — saber onde e como consultar é vital.
🧩 Subdomínios podem conter aplicações esquecidas ou vulneráveis (“Shadow IT”).
📤 Técnicas de força bruta via DNS ajudam a mapear ativos mesmo sem informações iniciais.
