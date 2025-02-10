# Máquina forgotten_portal

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-2.png)

### Análisis

Entré en la web http://172.17.0.2 hice ctrl + u y encontré lo siguiente:

![alt text](image-3.png)

por lo tanto entré en: m4ch1n3_upload.html

![alt text](image-4.png)

### Intrusión

entonces como me permite subir archivos con extensión php subí una reverse shell y me puse a la escucha con netcat.


![alt text](image-5.png)

![alt text](image-6.png)

![alt text](image-7.png)


hice tratamiento de la tty:

script /dev/null -c bash

crtl +z

crtl +z

stty raw -echo; fg

reset

xterm

export TERM=xterm

export SHELL=bash


vi los usuarios dentro del sistema:

![alt text](image-8.png)

dentro de /var/www/html encontramos un archivo access_log que contiene lo siguiente:

![alt text](image-9.png)

con cybercheff decodifiqué: YWxpY2U6czNjcjN0cEBzc3cwcmReNDg3

![alt text](image-10.png)

cambié al usuario alice:

![alt text](image-11.png)

dentro de /home/alice/incidents hay un archivo llamado report que contiene lo siguiente:

![alt text](image-12.png)

![alt text](image-13.png)

entonces lo que se me ocurre es copiar el id_rsa de alice y iniciar sesión mediante ssh con el usuario bob y que sabemos el Passphrase.

![alt text](image-14.png)

### Escalar privilegios

siendo el usuario bob:

![alt text](image-15.png)