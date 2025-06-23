Light - Full Report 

Objetivo
Aprender técnicas básicas de busca e filtragem de informações em sistemas Linux, essenciais para investigações forenses e pentests.

🛠️ Ferramentas Utilizadas
Ferramenta	Comando Exemplo			Finalidade
grep		grep "palavra" arquivo.txt	Busca padrões em arquivos
find		find / -name "*.conf"		Localiza arquivos por nome/extensão
awk		awk '{print $1}' dados.txt	Processamento avançado de texto


🔍 Passo a Passo Detalhado
1. Busca Simples com grep

Comando:
grep -i "senha" /var/log/auth.log

Explicação:
-i: Ignora maiúsculas/minúsculas
"senha": Termo buscado
/var/log/auth.log: Arquivo analisado

Saída útil:
May 10 14:23:45 sshd[1234]: Failed password for root from 192.168.1.100

2. Filtragem com awk

Comando:
awk -F: '{print $1}' /etc/passwd

Explicação:
-F:: Define ":" como separador
{print $1}: Imprime a primeira coluna (nomes de usuários)

Resultado:
root  
bin  
daemon  
... 

3. Busca de Arquivos com find

Comando:
find /home -type f -name "*.txt" -mtime -7

Explicação:
/home: Diretório alvo
-type f: Só arquivos (não pastas)
-name "*.txt": Arquivos com extensão .txt
-mtime -7: Modificados nos últimos 7 dias

💻 Exercício Prático
Cenário: Encontrar todos os arquivos .conf modificados recentemente:
find /etc -name "*.conf" -mtime -30 -exec ls -la {} \;

🏆 Artefatos Coletados
Tipo		Comando usado				Informação obtida
Logins SSH	grep "ssh" /var/log/auth.log		IPs de tentativas de acesso
Usuários	awk -F: '{print $1}' /etc/passwd	Lista de contas do sistema

💡 Lições Aprendidas
grep/awk são essenciais para análise rápida de logs.
find pode localizar arquivos suspeitos em investigações.
Combinar comandos (ex: find + grep) potencializa buscas.