# Máquina DevTools

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing web

feroxbuster -u 'http://172.17.0.2' -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -x txt,php,bak,db,py,html,js,jpg,png,git,sh -t 200 --random-agent --no-state -d 10

![alt text](image-2.png)

Entramos en backupp.js y encontramos:

![alt text](image-3.png)

### Fuerza bruta a SSH

utilzamos hydra para hacer fuerza bruta:

![alt text](image-4.png)

### Intrusión

iniciamos sesión por ssh con las credenciales encontradas:

![alt text](image-5.png)

### Escalar privilegios

![alt text](image-6.png)