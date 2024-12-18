# Máquina dockhacklab

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![clear](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

entramos en la ruta /hackademy/

![alt text](image-3.png)

hicimos gobuster en la ruta /hackademy/

gobuster dir -t 200 -u http://172.17.0.2/hackademy/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-4.png)

entramos en la ruta /upload.php

![alt text](image-5.png)

Lo que me da la impresión de subir una reverseshell con extensión .jpg.php

haciendo una prueba al subir una imagen llamada perro.jpeg:

![alt text](image-6.png)

me sale lo siguiente:

![alt text](image-7.png)

al aplicar gobuster a la ruta /hackademy/ no aparece la ruta dónde se guarda las imágenes, entonces intuyo que se guarda en /hackademy/xxx_archivo.jpeg

entonces como me dice que el archivo se guarda con un nombre xxx_ puedo intuir que se trata de letras, numero o numeros y letras:

utilizando la herramienta crunch:

crunch 3 3 z0123456789abcdefghijklmnopqrstuvwyxz -o dicnumletras.txt

![alt text](image-8.png)

utilizando wfuzz:

![alt text](image-11.png)

![alt text](image-9.png)

el archivo rev.jpeg.php tiene un reverse shell, nos ponemos en escucha con netcat y entramos en la web con la url:

![alt text](image-10.png)

hacemos tratamiento de la TTY

![alt text](image-13.png)

![alt text](image-14.png)

### Escalar privilegios

sieno el usuario firsthacking

![alt text](image-12.png)