# Maquina apolos

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

Entramos en la web y me creo una cuenta e inicio sesión, luego me voy al panel de mi carrito y me encuentro con un intup de búsqueda, aplico unos comandos de inyección sql y funcionan.

![alt text](image-3.png)

![alt text](image-4.png)

Entonces intrcepto la petición de búsqueda de un producto con burpsuite, la guardo como archivo llamado search, para luego utilizar sqlmap.

![alt text](image-5.png)

ejecuto:

sqlmap -r search --dbs --batch --dump

![alt text](image-6.png)

me interesa el usuario admin, desencripto la password con crackstation.

![alt text](image-7.png)

ahora iniciamos sesión con las credenciales encontradas.

Iniciada la sesión nos dirigimos a la sección de administración, luego en configuración.

![alt text](image-8.png)

![alt text](image-9.png)

luego hay una secció para subir un archivo, el archivo que podemos subir debe ser extensión phtml

![alt text](image-10.png)

### Intrusión

creamos una reverse shell en php con extensión phtml, nos ponemos en escucha con netcat, la subimos nos dirigimos a uploads le damos clic en el archivo.

Una vez iniciada la sesión hacemos tratamiento de la tty.

Luego me dirijí a home y me doy cuenta que existe un usuario llamado luisillo_o

![alt text](image-11.png)

lo que hice fue usar la herramienta Sudo_BruteForce -> https://github.com/Maalfer/Sudo_BruteForce, la descargué en mi kali y la pasé a la máquina victima creando un servidor web con python y descargandola en la máquina víctima con wget, de igual manera pasé el rockyou.

![alt text](image-12.png)

Ejecución de la herramienta:

![alt text](image-13.png)

![alt text](image-14.png)

### Escalar privilegios

cambiamos al usuario luisillo_o

el usuario luisillo_o tiene permiso de lectura del archivo shadow, entonces hice

![alt text](image-15.png)

luego ejecuté en mi kali:

unshadow passwd shadow > hash

![alt text](image-16.png)

![alt text](image-17.png)