# Maquina

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,139,445 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

### Listar samba

![alt text](image-2.png)

encontramos un archivo access.txt que contenia un jwt, lo verificamos con jwt.io y nos aparecio un dominio y un usuario:

![alt text](image-3.png)

satriani7 -> eseemeb.dl

![alt text](image-4.png)

### Crackmapexec 

crackmapexec smb 172.17.0.1 -u satriani7 -p /usr/share/wordlists/rockyou.txt --users

![alt text](image-5.png)

![alt text](image-6.png)




nos aseguramos a que tenemos acceso con las credenciales de arriba:



smbmap -H 172.17.0.1 -u satriani7 -p 50cent

![alt text](image-8.png)

smbclient //172.17.0.1/backup24 -U satriani7%50cent

![alt text](image-9.png)

abrimos el archivo credentials.txt y encontramos las credenciales para SSH.

![alt text](image-10.png)

![alt text](image-11.png)

### Escalar privilegios

No encontramos nada, utilizando las diferentes herramientas tales como sudo -l, SUID, crontab, linpeas, pspy64.

Aplicando el artificio:

hice fuzzing web y encontramos un /productos.php entonces con la conexion ssh que tengo entre en /var/www/html y renombre el archivo procutos.php por products.php ya que no podia editarlo y cree un productos.php con una reverse shell.

![alt text](image-12.png)

![alt text](image-14.png)

![alt text](image-13.png)

me puse en escucha por el puerto 443 y luego entre en la web a /productos.php, una vez conectado, hice tratamiento de la TTY:





