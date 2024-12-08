# Máquina Whoiam

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.18.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.18.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.18.0.1/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

### Entramos en /backups

descargamos el archivo .zip

![alt text](image-3.png)

lo descomprimimos y vemos el contenido:

![alt text](image-4.png)


### Intrusión

Iniciamos sesión con las credenciales encontradas:

![alt text](image-5.png)

luego creamos un rev.php y lo comprimimos con zip


código rev.php:

![alt text](image-6.png)

![alt text](image-7.png)


nos ponemos en escucha con netcat en el puerto 443

![alt text](image-8.png)

subimos el plugin y luego lo instalamos y activamos y listo tenemos acceso:

![alt text](image-9.png)

hacemos tratamiento de la tty

ahora tenemos que cambiar a diferentes usuarios:

rafa, ruben

![alt text](image-10.png)

### Escalar privilegios

Siendo el usuario ruben

![alt text](image-11.png)