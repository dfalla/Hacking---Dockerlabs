# Máquina Upload

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

### Entrando en la web

![alt text](image-3.png)

Me permite subir archivo con extensión phtml, entonces lo que hice fue hacer una reverse shell en php y darle la extensión phtml, colocar nc en escucha en el puerto 443, para luego dirigime a uploads y hacer clic en el archivo .phtml

![alt text](image-4.png)

Una vez dentro hacemos tratamiento de la TTY:

### Escalar privilegios

![alt text](image-6.png)



