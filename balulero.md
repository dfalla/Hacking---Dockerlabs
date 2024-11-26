# Maquina Balulero

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

### Ingresando a la web y Escalar privilegios

![alt text](image-2.png)

![alt text](image-7.png)

En scripts.js encontramos una ruta oculta llamada .env_de_baluchingon, ingresamos por la web y encontramos las credenciales de ssh, luego ingresamos por ssh, hacemos: 

![alt text](image-3.png)

sudo -l

![alt text](image-4.png)

![alt text](image-5.png)

cambiamos al usuario chocolate, ejecutamos pspy y vemos que se ejecuta un archivo script.php continuamente entonces vimos que se puede sobreescribir y le coloque el siguiente codigo, espere un rato y ejecute:

![alt text](image-6.png)

bash -p y listo soy root !!!

