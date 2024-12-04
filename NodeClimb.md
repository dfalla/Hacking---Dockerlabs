# Máquina NodeClimb

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p21,22 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Entramos al servidor FTP

![alt text](image-2.png)

y descargamos secretitopicaron.zip

### Descomprimir archivos que tienen contraseña

Herramienta: fcrackzip

![alt text](image-3.png)

### Intrusión

Me conecté por ssh con las credenciales encontradas.

### Escalar privilegios

luego hice sudo -l

![alt text](image-4.png)

contenido del código de script.js

![alt text](image-5.png)


![alt text](image-6.png)