# Máquina WalkingCMS

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

hacemos fuzzing web a /wordpress

![alt text](image-3.png)

Como se trata de wordpress utilizamos wpscan para encontrar algún usuario:

![alt text](image-4.png)

![alt text](image-5.png)

Ahora hacemos un ataque de fuerza bruta con wpscan para intentar adivinar la contraseña.

![alt text](image-6.png)

![alt text](image-7.png)

### Intrusión

Iniciamos sesión en wordpress y subimos un plugin.

Contenido del plugin:

![alt text](image-8.png)

lo comprimimos en formato .zip

lo subimos, y lo activamos:

Hacemos tratamiento de la TTY

buscamos binarios SUID:

### Escalar privilegios

![alt text](image-9.png)

![alt text](image-10.png)