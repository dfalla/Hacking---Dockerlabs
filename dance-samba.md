# Máquina dance-samba

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### FTP

nos conectamos al servicio ftp y descargamos el archivo nota.txt y vemos el contenido.

![alt text](image-2.png)

### Samba

Análisis con: 

smbclient

![alt text](image-4.png)

enum4linux

enum4linux 172.17.0.2

![alt text](image-3.png)

Encontramos el usuario macarena

Fuerza bruta con netexec

![alt text](image-5.png)

### Intrusión
1.- creamos claves de ssh:

ssh-keygen -t rsa -b 4096

2.- Creamos el directorio .ssh en el recurso compartido

3.- Creamos una copia de la id_rsa.pub con el nombre de authorized_keys para luego subir ambas (id_rsa.pub y el authorized_keys) al directorio .ssh

4.- Le damos permisos 600 al id_rsa

5.- No conectamos por ssh con el id_rsa

Nos conectamos al recurso compartido:

![alt text](image-6.png)

![alt text](image-7.png)

Nos conectamos por ssh con id_rsa:

![alt text](image-8.png)

### Escalar privilegios

en la ruta: /home/secret encontramos un hash, al verlo era un código en base64 y lo descifré con cyberchef

![alt text](image-10.png)

la contraseña descifrada le pertenece al usuario macarena entonces hice sudo -l y escribi la contraseña, luego tengo el binario file que me permite ver archivos como el de password.txt que se encuentra en opt, el cual es la contraseña root.

![alt text](image-9.png)
