# Máquina BadPlugin

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.1.100

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 vvv -Pn 192.168.1.100

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://192.168.1.100/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-2.png)

hacemos fuzzing web a /wordpress

![alt text](image-3.png)


### Wordpress

agregamos el dominio escolares.dl al /etc/hosts

luego aplicamos wpscan para enumerar usuarios

![alt text](image-4.png)

![alt text](image-5.png)

ahora hacemos fuerza bruta:

![alt text](image-6.png)

![alt text](image-7.png)
