# Máquina File

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p21,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null


### Intrusión

Entramos a file_upload.php

Nos permite subir archivo .phar, con reverse shell en el puerto 443

![alt text](image-2.png)


nos ponemos en escucha con netcat, hacemos clic en rev.phar

![alt text](image-3.png)

hacemos tratamiento de la TTY

luego vi todos los usuarios en el sistema

![alt text](image-4.png)

luego utilicé la herramiente multi-su_force -> https://github.com/Maciferna/multi-Su_Force

![alt text](image-5.png)

Entré al usuario fernando, su fernando, contraseña chocolate.

entré a /home/fernando y encontré una imagen.

para descargarla inicié un servidor web en /home/fernando, luego con wget la descargué en mi kali linux

![alt text](image-6.png)

![alt text](image-7.png)

Ahora apliqué esteganografia sobre la imagen.

![alt text](image-8.png)

tiene una contraseña:

![alt text](image-9.png)

utilizando crackstation:

![alt text](image-10.png)

la contraseña encontrada le pertenece a mario:

cambimos al usuario mario, luego al usuario julen y luego al usuario iker.

![alt text](image-11.png)


### Escalar privilegios

Siendo el usuario iker:

cambiamos el nombre del archivo geo_ip.py a geos_ip.py, luego hice:

![alt text](image-12.png)