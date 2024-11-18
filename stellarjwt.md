### Maquina Stellarjwt

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

## Entramos en la web:

y nos sale la pregunta que astronomo descubrio neptuno:


Ataque con hydra a ssh:

Johann Gottfried Galle

gottfried

## Fuzzing web

gobuster dir -t 200 -u http://172.17.0.1:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

entramos a /universe y hacemos ctrl + u

![alt text](image-2.png)

vemos un jwt

entramos en la web de jwt.io

y desciframos un usurio llamado neptuno:

## Intrusión

entramos por ssh con el usuario neptuno y la contraseña Gottfried

![alt text](image-3.png)

hacemos:

cat /etc/passwd | grep bash

![alt text](image-4.png)

al hacer ls -la en /home/neptuno encontramos un archivo oculto llamado .carta_a_la_NASA.txt, lo abrimos y encontramos la contraseña del usuario nasa.

![alt text](image-5.png)

cambiamos al usuario nasa con las credenciales:

nasa y Eisenhower

con el usuario nasa, hacemos sudo -l

![alt text](image-7.png)

cambiamos al usuario elite

## Escalar privilegios

![alt text](image-8.png)


![alt text](image-9.png)


![alt text](image-10.png)


![alt text](image-11.png)