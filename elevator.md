# Máquina Elevator

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x php,txt,bak,sh,py,js,html -b 403,404 2>/dev/null

![alt text](image-2.png)


gobuster dir -t 200 -u http://172.17.0.2/themes/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x php,txt,bak,sh,py,js,html -b 403,404 2>/dev/null

![alt text](image-3.png)

### Intrusión


Entramos en /themes/archivo.html y aquí me permite subir archivos .jpg, entonces lo que hice fue hacer una reverse shell (pentestmonkey) en php con la extensión .php.jpg

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)

Me puse en escucha con nc en el puerto 443.

Hice tratamiento de la tty, y luego tuve que entrar a diferentes usuarios para poder ser root.

![alt text](image-7.png)

![alt text](image-8.png)

![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)

![alt text](image-12.png)