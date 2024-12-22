# Máquina Hackpenguin

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![clear](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

### Intrusión

entrando en la web:

![alt text](image-3.png)

descargué la imagen:

![alt text](image-4.png)

![alt text](image-5.png)

extrayendo archivos ocultos:

![alt text](image-6.png)

al abrir el archivo penguin.kdbx con la herramienta keepassxc me pide contraseña entonces procedí a crackearla, primero extrayendo el hash con keepass2john y luego con john la crackeo.

![alt text](image-7.png)

procedo abrir el archivo con keepassxc

keepassxc penguin.kdbx

![alt text](image-8.png)

también se puede abrir online con https://app.keeweb.info/

![alt text](image-9.png)

luego nos conectamos mediante ssh con el usuario penguin y la contraseña encontrada:

![alt text](image-10.png)

### Escalar privilegios

utilicé pspy64 para ver si se ejecutan archivos y me di con la sorpresa que se ejecuta un script.sh en /home/hackpenguin/script.sh

![alt text](image-11.png)

vi los permisos y tenía permiso de escritura:

![alt text](image-12.png)

modifiqué el archivo:

![alt text](image-13.png)

me puse en escucha con netcat:

![alt text](image-14.png)