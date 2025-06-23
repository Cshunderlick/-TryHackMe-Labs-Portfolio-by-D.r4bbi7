Security Principles - Full Report

Objetivo
Entender os princípios fundamentais de segurança da informação que formam a base para proteção de sistemas e dados.

🔒 Os 5 Pilares da Segurança (CIA + 2)

1. Confidencialidade
"Dados só para quem deve vê-los"

Exemplo Prático:
# Criptografar arquivo com OpenSSL
openssl enc -aes-256-cbc -salt -in secreto.txt -out secreto.enc -k MinhaSenhaForte

Como implementar?
Criptografia (AES, RSA)
Controle de acesso (usuários/senhas)

2. Integridade
"Garantir que dados não são alterados"

Ferramenta:
# Gerar hash SHA-256 de um arquivo
sha256sum documento.txt

Saída:
d4d4d4... documento.txt

3. Disponibilidade
"Sistemas acessíveis quando necessários"
Ameaça comum: Ataques DDoS

Proteção:
# Regra básica de firewall contra flood ICMP
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT


4. Autenticidade (Novo)
"Garantir a origem dos dados"
	Exemplo: Assinaturas digitais com GPG

gpg --verify arquivo.sig arquivo.txt


5. Não-repúdio (Novo)
"Impedir que alguém negue uma ação"
Tecnologia: Blockchain, logs assinados


🛡️ Princípios de Defesa Profunda
1. Defesa em Camadas
"Múltiplas barreiras de proteção"

Exemplo:
[Internet] → [Firewall] → [IDS] → [Autenticação] → [Dados Criptografados]


2. Privilégio Mínimo
"Usuários/acessos só com permissões necessárias"

Comando Linux:
chmod 750 /pasta/confidencial  # Dono: ler/escrever/executar | Grupo: ler/executar | Outros: nada


3. Falha Segura
"Se quebrar, que quebre bloqueando"

Caso real:
Firewalls devem bloquear tráfego se perderem energia


💻 Exercício Prático
Cenário: Proteger um arquivo sensível

Criar hash para monitorar alterações
sha512sum contrato.pdf > hash_contrato.sha512

Verificar posteriormente:
sha512sum -c hash_contrato.sha512

Saída esperada:
contrato.pdf: OK

🏆 Checklist de Boas Práticas
Princípio		Implementação		Ferramenta Exemplo
Confidencialidade	Criptografia de disco	Veracrypt, LUKS
Integridade		Assinaturas digitais	GPG, SHA-256
Disponibilidade		Backup 3-2-1		rsync, Borg Backup
Autenticidade		Certificados SSL/TLS	Let's Encrypt


💡 Lições Aprendidas
CIA+2 é o alicerce de qualquer política de segurança
Defesa em profundidade reduz risco mesmo com falhas pontuais
Regras simples (como mínimo privilégio) previnem 80% dos ataques

