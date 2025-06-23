Lookup - Full Report 

Objetivo
Aprender a usar ferramentas de consulta de informações em sistemas Linux, como DNS, WHOIS e buscas locais, essenciais para coleta de inteligência em pentests.

🛠️ Ferramentas Utilizadas
Ferramenta	Comando Exemplo		Finalidade
dig		dig example.com		Consulta registros DNS
whois		whois example.com	Mostra dono de domínio
host		host 192.168.1.1	Converte IP em domínio ou vice-versa

🔍 Passo a Passo Detalhado
1. Consultando DNS com dig

Comando:
dig tryhackme.com ANY +noall +answer

Explicação:
ANY: Mostra todos os registros (A, MX, TXT...)
+noall +answer: Filtra só as respostas

Saída útil:
tryhackme.com.   300  IN  A     172.67.70.119  
tryhackme.com.   300  IN  MX    10 mail.tryhackme.com 
 
2. Informações de Domínio com whois

Comando:
whois tryhackme.com

Dados importantes:
Registrant Name: TryHackMe Ltd  
Registrar: Namecheap Inc  
Creation Date: 2018-07-05  


3. Busca Reversa com host

Comando:
host 172.67.70.119

Resultado:
119.70.67.172.in-addr.arpa domain name pointer tryhackme.com.
  
💻 Exercício Prático
Cenário: Descobrir servidores de e-mail de um domínio:
dig tryhackme.com MX +short

Saída:
10 mail.tryhackme.com.  

🏆 Artefatos Coletados
Tipo		Comando usado		Informação obtida
DNS		dig tryhackme.com A	IP do site
WHOIS		whois tryhackme.com	Dados do registrante
E-mails		dig MX tryhackme.com	Servidores de e-mail


💡 Lições Aprendidas
DNS revela infraestrutura oculta (subdomínios, e-mails).
WHOIS expõe dados sensíveis (nome, telefone do dono).
Ferramentas nativas do Linux (dig, host) são poderosas para reconhecimento.