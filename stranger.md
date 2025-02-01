# Máquina Stranger

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p21,22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing web

![alt text](image-2.png)

fuzzing web a http://172.17.0.2/strange/

![alt text](image-3.png)

al entrar por url en /private.txt se descargó el archivo

y al entrar a /secret.html

![alt text](image-6.png)

entonces hice un ataque con hydra al puerto FTP

![alt text](image-4.png)

inicié sesión con el usuario admin y con la contraseña banana y descargué lo siguiente

![alt text](image-5.png)

### Intrusión

El archivo private_key.pem sirve para desencriptar el archivo private.txt, utilicé el siguiente comando:

openssl pkeyutl -decrypt -in private.txt -out decrypted.txt -inkey private_key.pem

![alt text](image-7.png)

inicié sesión por ssh con las credenciales :

mwheeler - demogorgon

![alt text](image-8.png)

como ya sabía la clave de FTP de admin que es banana, entonces prové como su contraseña para cambiar al usuario admin.

![alt text](image-9.png)

### Escalar privilegios

![alt text](image-10.png)






