Python Basics - Full Report

Objetivo
Aprender os fundamentos de Python aplicados à segurança cibernética, desde sintaxe básica até scripts para automação de tarefas.

🐍 Conceitos Essenciais
1. Variáveis e Tipos de Dados

# Strings (texto)
alvo = "192.168.1.1"

# Números
porta = 22

# Booleanos
servidor_online = True



2. Estruturas de Controle
Condicionais (if/else):

if porta == 22:
    print("Porta SSH aberta!")
elif porta == 80:
    print("Servidor web detectado")
else:
    print("Porta desconhecida")



Loops (for/while):

# Varre portas comuns
for porta in [21, 22, 80, 443]:
    print(f"Testando porta {porta}...")
🔧 Scripts Úteis para Cybersecurity


1. Scanner de Portas Simples

import socket

alvo = "192.168.1.1"

for porta in range(1, 1025):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(1)
    resultado = sock.connect_ex((alvo, porta))
    if resultado == 0:
        print(f"Porta {porta}: ABERTA")
    sock.close()


2. Quebrador de Senhas Básico

import hashlib

senha_alvo = "5f4dcc3b5aa765d61d8327deb882cf99"  # MD5 de "password"

with open("wordlist.txt") as arquivo:
    for linha in arquivo:
        palavra = linha.strip()
        hash_teste = hashlib.md5(palavra.encode()).hexdigest()
        if hash_teste == senha_alvo:
            print(f"Senha encontrada: {palavra}")
            break


3. Parser de Logs

with open("/var/log/auth.log") as log:
    for linha in log:
        if "Failed password" in linha:
            print(linha.strip())


🎯 Exercícios Práticos
1. Crie um script para pingar IPs

import os

rede = "192.168.1."

for host in range(1, 11):
    ip = rede + str(host)
    resposta = os.system(f"ping -c 1 {ip} > /dev/null")
    if resposta == 0:
        print(f"{ip} está online")


2. Extrair URLs de um arquivo

import re

with open("dados.txt") as arquivo:
    texto = arquivo.read()
    urls = re.findall(r'http[s]?://(?:[a-zA-Z]|[0-9]|[$-_@.&+]|[!*\\(\\),]|(?:%[0-9a-fA-F][0-9a-fA-F]))+', texto)
    print("URLs encontradas:", urls)


🏆 Projeto Final: Scanner de Vulnerabilidades

import requests

def testar_sql_injection(url):
    payloads = ["'", "\"", "1=1--"]
    for payload in payloads:
        teste = requests.get(f"{url}?id={payload}")
        if "error in your SQL syntax" in teste.text:
            print(f"[!] Vulnerável a SQLi com payload: {payload}")
            return True
    return False

testar_sql_injection("http://site.com/login")



💡 Lições Aprendidas
Python é essencial para automação em segurança
Bibliotecas como socket, hashlib e requests são poderosas
Scripts simples podem economizar horas de trabalho manual

