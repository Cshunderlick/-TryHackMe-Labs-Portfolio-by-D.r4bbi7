Search Skills - Full Report 

Objetivo
Dominar técnicas avançadas de busca para encontrar informações sensíveis em sistemas e na web, essenciais para pentests e investigações.

🔍 Técnicas de Busca em Sistemas
1. Busca por Arquivos Sensíveis

Comandos Linux:
# Buscar arquivos de configuração
find / -name "*.conf" -type f 2>/dev/null

# Procurar senhas em arquivos
grep -rnw '/' -ie 'password' --color=auto 2>/dev/null

# Arquivos com permissões perigosas
find / -perm -o=w -type f 2>/dev/null


2. Busca em Logs

# Tentativas de login falhas
grep "Failed password" /var/log/auth.log

# Acessos HTTP suspeitos
cat /var/log/apache2/access.log | grep "404"


🌐 Busca Avançada na Web
1. Google Dorking

Operador		Exemplo				Finalidade
site:			site:gov.br senha		Busca no domínio específico
filetype:		filetype:pdf "confidencial"	Encontra arquivos específicos
intitle:		intitle:"index of" backup	Localiza diretórios abertos

Exemplo Prático:
site:github.com "API_KEY" language:python


2. Ferramentas Especializadas

Shodan: Busca dispositivos IoT expostos
	country:BR port:3389

Wayback Machine: Ver versões antigas de sites



💻 Exercício Prático

1. Caça a Credenciais
# Buscar arquivos que podem conter senhas
	find /var/www/html -name "*.php" -exec grep -l "mysql_connect" {} \;

2. Google Hacking
Pesquise no Google:
	intitle:"index of" "wp-admin" "user.zip"


🏆 Checklist de Habilidades

Técnica			Comando/Ferramenta	Dominado?
Busca local		find, grep		[ ]
Google Dorking		site:, filetype:	[ ]
Ferramentas externas	Shodan, Wayback Machine	[ ]


💡 Lições Aprendidas
90% dos ataques começam com coleta de informações
Dados sensíveis são frequentemente vazados em arquivos esquecidos
Busca é habilidade fundamental tanto para atacantes quanto defensores

