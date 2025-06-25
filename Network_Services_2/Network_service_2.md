🛡️ Network Services 2 - Full Report (TryHackMe)

Objetivo:
Explorar serviços de rede com foco em FTP, SMB e NFS, entendendo como vulnerabilidades de configuração podem permitir acesso indevido e escalada de privilégios.

🛠️ Ferramentas Utilizadas:

Nmap: Mapeamento de portas e detecção de serviços.
enum4linux: Enumeração de informações SMB.
smbclient: Acesso a compartilhamentos SMB.
showmount: Enumeração de volumes NFS.
mount: Montagem de volumes remotos no sistema.
John The Ripper: Quebra de senhas.
LinPEAS: Enumeração de privilégios locais.


📌 Passo a Passo Detalhado

🔍 1. Enumeração Inicial (Nmap)

Comando:
nmap -sV -p- 10.10.10.10 -oN scan.txt

Explicação:
-sV: Detecta versões dos serviços.
-p-: Escaneia todas as portas.
-oN: Salva o resultado.

Saídas Relevantes:
21/tcp open ftp
139/tcp open netbios-ssn
445/tcp open microsoft-ds
2049/tcp open nfs

Por que importa?
Indica presença de FTP (anônimo?), SMB (compartilhamentos acessíveis?) e NFS (volumes exportados?).


📁 2. FTP (Porta 21)
Comando:
ftp 10.10.10.10

Resultado:
Acesso anônimo permitido.

Ação:
Baixei arquivos da raiz do FTP — havia um arquivo com possíveis credenciais para uso posterior.


📂 3. SMB (Portas 139 e 445)
Enumeração:
enum4linux -a 10.10.10.10

Resultado:
Enumerou usuários e compartilhamentos visíveis.

Acesso a compartilhamento:
smbclient //10.10.10.10/share -N

Descoberta:
Acesso ao diretório público contendo arquivos de configuração e credenciais de usuário.

📦 4. NFS (Porta 2049)
Comando:
showmount -e 10.10.10.10

Resultado:
/export *(rw,no_root_squash)

Montagem:
mkdir /mnt/nfs
mount -t nfs 10.10.10.10:/export /mnt/nfs

Oportunidade:
Como no_root_squash está habilitado, usuários remotos com UID 0 (root) têm acesso total.

Exploração:
Criei um shell reverso como root e movi para o diretório exportado.
A partir daí, obtive execução como root.

⬆️ 5. Escalação de Privilégios (Local)
Comando:
./linpeas.sh

Resultado:
Identificou binários inseguros e permissões SUID.

Exemplo de exploração (caso aplicável):
/usr/bin/somebinary . -exec /bin/bash \; -quit


✅ Lições Aprendidas
🔐 Serviços mal configurados representam riscos críticos:
FTP com acesso anônimo = vazamento de informações.
SMB sem autenticação = exposição de dados internos.
NFS com no_root_squash = acesso root remoto.


🛡️ Boas práticas:
Desativar acessos anônimos.
Restringir compartilhamentos por IP e autenticação.
Evitar exportações NFS inseguras.