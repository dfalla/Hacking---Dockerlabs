### Maquina trust

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.18.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.18.0.2

![alt text](image.png)



## Fuzzing web

gobuster dir -t 200 -u http://172.18.0.2:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

/secret.php -> entramos

http://172.18.0.2/secreto.php

![alt text](image-1.png)

encontramos el usuario mario

## Ataque con hydra para saber la contraseña

![alt text](image-2.png)

## Intrusion

![alt text](image-3.png)

## Escalar privilegios

![alt text](image-4.png)