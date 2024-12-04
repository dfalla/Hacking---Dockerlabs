# Máquina Los40ladrones

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

entré a /qdefense.txt

![alt text](image-3.png)

hasta este punto veo 2 cosas, que existe un usuario toctoc y que podemos enviar señales para descubrir puertos.

### Técnica de Port Knocking

![alt text](image-4.png)

### Fuzzing web para ver si se abrió otro puerto

![alt text](image-5.png)

como ya teníamos el usuario toctoc, hice un ataque con hydra:

![alt text](image-6.png)

### Intrusión

Nos conectamos por ssh con las credenciales encontradas.

### Escalar privilegios

hice sudo -l, escribí la contraseña de toctoc y luego ejecuté sudo /opt/bash

![alt text](image-7.png)