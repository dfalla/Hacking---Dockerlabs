# Maquina Winterfell

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,139,445 -vvv -Pn 172.17.0.1

![alt text](image-1.png),

### FUZZING WEB

gobuster dir -t 200 -u http://172.17.0.1:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-4.png)

http://172.17.0.1/dragon

![alt text](image-5.png)

guardamos esas frases en un archivo llamado passwords.txt, lo utilizaré luego.

### Enumeramos el SMB

![alt text](image-2.png)

![alt text](image-3.png)

Utilizando el archivo passwords.txt

![alt text](image-6.png)

![alt text](image-7.png)

usamos cybercheff para crackear la contraseña:

![alt text](image-8.png)

### Intrusión

![alt text](image-9.png)

![alt text](image-10.png)

el contenido de .mensaje.py

![alt text](image-11.png)

siendo el usuario aria:

![alt text](image-12.png)

hacemos su daenerys y escribimos la contraseña drakaris

siendo el usuario daenerys:

![alt text](image-13.png)

El archivo shell.sh tenia ya el reverse shell solo le puse mi ip de atacante.

