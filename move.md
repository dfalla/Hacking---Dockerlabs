# Máquina Move

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,3000 -vvv -Pn 172.17.0.2

![alt text](image-1.png)


### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

Entramos en /maintenance.html

![alt text](image-3.png)

### Entramos en la web por el puerto 3000

![alt text](image-4.png)

buscamos un exploit para la version 8.3.0 de Grafana

![alt text](image-5.png)

Ejecución del exploit

![alt text](image-6.png)

como anteriormente en la ruta /manteinance.html me dijo algo sobre /tmp/pass.txt, lo vi y era una contraseña entonces se me vino a la mente de que como está el puerto ssh abierto y corriendo puede que sea una contraseña y es por eso que también ví el archivo /etc/passwd

### Inrusión

Entré con el usuario freddy y la contraseña t9sH76gpQ82UFeZ3GXZS

![alt text](image-7.png)

### Escalar privilegios

![alt text](image-8.png)

hice sudo -l y vi que podía ejecutar sin contraseña /usr/bin/python3 /opt/maintenance.py

entonces vi los permisos de /opt/maintenance.py y vi que podía modificarlo, entonces le agregué el siguiente código:

![alt text](image-9.png)
