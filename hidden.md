# Máquina Hidden

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)


agregamos al /etc/hosts/ el dominio hidden.lab

### Fuzzing Web para subdominios

gobuster dns -d hidden.lab -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 50 --wildcard

encontramos el subdominio dev.hidden.lab, que también debemos agregarlo al etc/hosts

![alt text](image-4.png)

fuzzing para /dev.hidden.lab

gobuster dir -t 200 -u http:///dev.hidden.lab/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/

![alt text](image-15.png)

### Intrusión

entramos en /dev.hidden.lab

![alt text](image-2.png)

hice las pruebas y me permite subir cualquier cosa pero solo procesa archivos .phar, entonces subí un reverse shell (pentestmonkey) y me puse en escucha por el puerto 443

![alt text](image-3.png)

![alt text](image-5.png)

hice clic en el archivo .phar y obtuve la conexión:

![alt text](image-6.png)

hice tratamiento de la tty

observé el home y ví 3 usuarios:

![alt text](image-7.png)

### Cracking de contraseñas dentro del equipo victima

herramieta multi-su_force.sh, la subimos mediante el subdominio dev.hidden.lab y también subimos las primeras 200 líneas del rockyou para hacer el ataque.

![alt text](image-8.png)

se encontró la contraseña 123123 para el usuario cafetero

![alt text](image-12.png)

### Escalar privilegios

primero escalarmos al usuario john.

siendo el usuario cafetero hacemos sudo -l

![alt text](image-9.png)

![alt text](image-10.png)

siendo el usuario john, hice sudo -l:

![alt text](image-11.png)

![alt text](image-13.png)

![alt text](image-14.png)

siendo el usuario bobby ejecuté sudo -l:

![alt text](image-17.png)

me apareció:

(root) NOPASSWD: /usr/bin/find

ejecuté:

sudo /usr/bin/find . -exec /bin/sh \; -quit

y me hice root.