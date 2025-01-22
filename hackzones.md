# Máquina

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,53,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

agregamos el dominio hackzones.hl al /etc/hosts

![alt text](image-2.png)

### Fuzzing Web

gobuster dir -t 200 -u http://hackzones.hl/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -b 403,404 2>/dev/null

![alt text](image-3.png)

### Intrusión

Al acceder a http://hackzones.hl/dashboard.hml

![alt text](image-4.png)

me permite subir archivos php entonces subí una reverse shell que se guarda en uploads

![alt text](image-5.png)

### Escalar privilegios

En /var/www/html/supermegaultrasecretofolder encontramos un archivo secret.sh

![alt text](image-7.png)

![alt text](image-6.png)

cambié al usuario mrrobot con la contraseña encontrada.

![alt text](image-8.png)

con el usuario mrrobot, hice sudo -l

![alt text](image-9.png)

entonces en /opt hay un archivo llamado SistemUpdate

entonces hice sudo /usr/bin/cat SistemUpdate y hallé la contraseña´de root

![alt text](image-10.png)

cambiando a root:

su root y escribí rooteable

![alt text](image-11.png)

