# Máquina chmod-4755

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,139,445 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### SMB

enumeración de compartidos:

![alt text](image-2.png)

enumeración de usuarios:

enum4linux 172.17.0.2

![alt text](image-3.png)

Fuerza bruta:

![alt text](image-4.png)

Iniciamos sesión al recurso compartido con smbclient, y observamos el note.txt

![alt text](image-5.png)

### Intrusión

Me conecté mediante ssh con las credenciales rabol : share_secret_only

![alt text](image-6.png)

como tenemos rbash 

ejecutamos:

python3 -c "import subprocess; subprocess.run('/bin/bash', shell=True)"

y luego

export PATH=/bin

### Escalar privilegios

find / -perm -4000 2>/dev/null

![alt text](image-7.png)


como tenemos curl disponible, voy a copiar el contenido de /etc/passwd
y en mi maquina atacante me creo un archivo passwd donde pego el contenido
de /etc/passwd de la maquina comprometida, modificando la primera linea
dejandola asi:

antes de modificar:	root:x:0:0:root:/root:/bin/bash
despues de modificar:	root::0:0:root:/root:/bin/bash

ahora desde mi maquina atacante levanto un servidor con python 

python3 -m http.server

luego, desde la maquina comprometida, como podemos ejecutar /usr/bin/curl como root
vamos a descargar el archivo que modificamos en la maquina atancante y guardarlo
en /etc/passwd, asi conseguimos modificar el contenido del archivo original

![alt text](image-9.png)

![alt text](image-8.png)

despues de validar los cambios, vemos que en efecto sobreescribimos el original
asi que ahora podemos escalar a root.

![alt text](image-10.png)
