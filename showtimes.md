# Maquina Showtimes

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Entrando en la web

Entramos en http://172.17.0.2/login_page/index.php y me di cuenta que es vulnerable a SQLi

![alt text](image-9.png)

![alt text](image-8.png)

entonces utilicé SQLMAP.


Para ver las bases de datos que tiene:

![alt text](image-2.png)

![alt text](image-3.png)


ver las tablas dentro de la base de datos users:

![alt text](image-4.png)

![alt text](image-5.png)

Ver el contenido de la tabla usuarios:

![alt text](image-6.png)

![alt text](image-7.png)

### Intrusión

Inicié sesión con las credenciales subrayadas.

![alt text](image-10.png)

Me apareció un panel para ingresar código en python, lo que se me ocurrió fue ingresar un código de reverse shell.

el código:

![alt text](image-11.png)

![alt text](image-12.png)

me puse previamente en escucha con netcat en el puerto 443

una vez ya infiltrado hice tratamiento de la TTY.

en /tmp hay un archivo llamado .hidden_txt.txt que al parecer son contraseñas en mayúsculas, lo copié y lo  tranformé a minúsculas.

![alt text](image-13.png)

como tenía el puerto ssh abierto, lo que hice fue un ataque con hydra.

![alt text](image-14.png)

Conexión por ssh:

![alt text](image-15.png)

Entré en /home/luciano y cambié en nombre del script.sh a scripts.sh

luego hice lo siguiente:

![alt text](image-16.png)


Me puse en escucha con nc en el puerto 4444

![alt text](image-17.png)