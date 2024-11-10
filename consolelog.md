### Maquina Consolelog

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

80/tcp   open  http    syn-ack ttl 64
3000/tcp open  ppp     syn-ack ttl 64
5000/tcp open  upnp    syn-ack ttl 64


## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80,3000,5000 -vvv -Pn 172.17.0.2

![alt text](image.png)

## Entrando en la web

http://172.17.0.2/authentication.js :

function autenticate() {
    console.log("Para opciones de depuracion, el token de /recurso/ es tokentraviesito");
}

## Fuzzing web

gobuster dir -t 200 -u http://172.17.0.2 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null 

/index.html          
/backend              
/authentication.js 

Entramos en la web /backend/server.js y encontramos:

![alt text](image-1.png)

## Intrusion

Ataque con hydra para saber el usuario -> /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt

![alt text](image-2.png)

Entramos por ssh con las credenciales encontradas

![alt text](image-3.png)

Todos los usuarios:

cat /etc/passwd | grep bash

root:x:0:0:root:/root:/bin/bash
tester:x:1000:1000::/home/tester:/bin/bash
lovely:x:1001:1001:lovely,,,:/home/lovely:/bin/bash

## Escalar privilegios

![alt text](image-4.png)






