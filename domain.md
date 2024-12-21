# Máquina domain

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80,139,445 -vvv -Pn 172.17.0.2

![alt text](image-1.png)


### Analizamos samba

enum4linux 172.17.0.2

![alt text](image-2.png)

fuerza bruta para saber la contraseña de bob:

![alt text](image-3.png)

nos conectamos con smbclient:

![alt text](image-4.png)

me di cuenta que está el index.html de la web, entonces subí una reverse shell para poder conectarme mediante el puerto 443

me puse en escucha en el puerto 443 y accedí a la reverseshell

![alt text](image-5.png)

### Escalar privilegios

![alt text](image-6.png)

una vez conectados hice su bob y escribí la contraseña star, luego busqué permisos SUID y me apareció nano lo que se me ocurrió fue abrir el archivo /etc/passwd con nano y quitar la x del usuario root:

![alt text](image-7.png)




