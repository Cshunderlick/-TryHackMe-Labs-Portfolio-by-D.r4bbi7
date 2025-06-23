Linux Fundamentals Part 1 (Info) - Full Report 

Objetivo
Dominar comandos essenciais do Linux para navegação, manipulação de arquivos e permissões - base para qualquer profissional de segurança.

🐧 Sistema de Arquivos Linux

Estrutura chave:
/
├── bin   → Comandos básicos (ls, cp)
├── etc   → Arquivos de configuração
├── home  → Diretórios dos usuários
├── root  → Home do superusuário
└── var   → Dados variáveis (logs)


🛠️ Comandos Essenciais
1. Navegação

Comando			Exemplo			Descrição
pwd			pwd			Mostra diretório atual
ls			ls -la /etc		Lista arquivos (-la: detalhes)
cd			cd ~/Documents		Muda de diretório

Dica:
ls -lh  # Mostra tamanhos legíveis (KB/MB)


2. Manipulação de Arquivos

Comando		Exemplo				Descrição
cp		cp arquivo.txt backup/		Copia arquivos
mv		mv antigo.txt novo.txt		Move/renomeia
rm		rm -r pasta/			Remove (-r: recursivo)
touch		touch novo.txt			Cria arquivo vazio


Atenção:
rm -rf /  # ☠️ NUNCA use - destruiria todo o sistema!


3. Permissões
Formato:
-rwxr-xr-- 1 user group 1.2K Jan 1 10:00 arquivo.txt
 ↑ ↑↑↑↑↑↑↑
 │ └── Permissões (usuário/grupo/outros)
 └── Tipo (- = arquivo, d = diretório)


Comandos úteis:
chmod 750 script.sh  # Dono: rwx, Grupo: r-x, Outros: ---
chown root:admin arquivo.conf  # Muda dono/grupo


💻 Exercícios Práticos

1. Criar e Organizar Arquivos
mkdir -p ~/pentest/{scans,reports}  # Cria estrutura de pastas
touch ~/pentest/scans/{alvo1,alvo2}.txt

2. Verificar Permissões Críticas
bash
ls -la /etc/passwd  # Deve ser -rw-r--r--
find / -perm -4000 2>/dev/null  # Lista binários SUID


🔍 Ferramentas para Segurança
1. Filtrar Logs
grep "Failed" /var/log/auth.log  # Tentativas de login falhas

2. Monitorar Processos
top -u root  # Visualiza processos do root

3. Compactar Dados
tar -czvf relatorio.tar.gz /pentest/reports/  # Cria backup


🏆 Checklist de Competências
Habilidade			Comando Dominado?
Navegar no filesystem		cd, ls, pwd
Gerenciar arquivos		cp, mv, rm
Configurar permissões		chmod, chown
Analisar logs			grep, tail


💡 Lições Aprendidas
Linux é o sistema operacional da segurança: 90% das ferramentas rodam nele
Permissões mal configuradas são a causa #1 de violações
Terminal > GUI: Produtividade multiplicada por comandos