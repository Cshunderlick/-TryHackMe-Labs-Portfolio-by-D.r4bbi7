Governance & Regulation - Full Report

Objetivo
Entender como leis e políticas de segurança (como GDPR e LGPD) impactam empresas e profissionais de cybersecurity.

📜 Principais Regulamentações

1. GDPR (Europa)

O que é?
Lei de proteção de dados que afeta qualquer empresa que lide com dados de cidadãos europeus.

Princípios-chave:
Consentimento explícito: Usuários devem autorizar uso de seus dados
Direito ao esquecimento: Pode solicitar exclusão de dados pessoais
Multas: Até 4% do faturamento global por violações

Exemplo Prático:
# Simulando registro de consentimento em banco de dados
INSERT INTO users (name, email, consent) VALUES ('João', 'joao@email.com', TRUE);

2. LGPD (Brasil)

Diferença para GDPR:
Multas menores (até 2% do faturamento no Brasil)
Exige Encarregado de Dados (DPO) nas empresas

Como implementar?
Criar política de privacidade clara
Mapear onde os dados são armazenados:
# Comando para listar bancos de dados (exemplo Linux)
ls /var/lib/mysql/


3. ISO 27001

Padrão internacional para segurança da informação:

Requisitos:
Avaliação de riscos
Controles de acesso (ex: chmod 600 arquivo.conf)
Backup criptografado

Exemplo de Documentação:
Política de Senhas:  
- Mínimo 12 caracteres  
- Troca a cada 90 dias  
- Bloqueio após 5 tentativas falhas 
 
🔍 Exercício Prático

Cenário: Você é o DPO de uma empresa. Como responder a um vazamento de dados?

Identifique o vazamento:
grep "vazamento" /var/log/sistema.log
Conteção: Isolar servidor afetado
Notificar autoridades: Prazo máximo de 72h (GDPR)

💡 Lições Aprendidas
Regulamentações não são opcionais – multas podem quebrar empresas
Documentação é tão importante quanto firewalls
Cybersecurity e Direito estão cada vez mais conectados