# Máquina Mybb

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Entramos a la web

![alt text](image-2.png)

![alt text](image-3.png)

agregamos al /etc/hosts

panel.mybb.dl

![alt text](image-4.png)

### Fuzzing web a panel.mybb.dl

gobuster dir -t 200 -u http://panel.mybb.dl/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -b 403,404 2>/dev/null


![alt text](image-5.png)

entramos en backups

![alt text](image-6.png)

luego en data vemos un usuario admin y una contraseña de un usuario alice

![alt text](image-7.png)

### Hydra

hydra -l admin -P /usr/share/wordlists/rockyou.txt panel.mybb.dl http-post-form "/admin/index.php:username=^USER^&password=^PASS^:F=The username and password combination you entered is invalid." 

![alt text](image-8.png)

Inicié sesión en el sistema:

![alt text](image-9.png)

al iniciar sesión vi la versión del sistema, MyBB 1.8.35

![alt text](image-10.png)

busqué un exploit para esa versión y encontré: https://github.com/SorceryIE/CVE-2023-41362_MyBB_ACP_RCE

![alt text](image-11.png)

### Intrusión

me envié una reverse shell

![alt text](image-12.png)

visualice el direcotorio home y visualicé que hay un usuario alice, previamente habia accedido a esta ruta en la url y se encontraba la contraseña encriptada de alice, entonces la cracke con johntheripper

![alt text](image-13.png)

cambio al usuario alice:

![alt text](image-14.png)

hice sudo -l

![alt text](image-15.png)

Esto quiere decir que cualquier usuario puede ejecutar cualquier script en rugby (rb) dentro de /home/alice/scripts

creé un archivo elevation.rb que me permita elevar a root

![alt text](image-16.png)

ejecuté el archivo

![alt text](image-17.png)



