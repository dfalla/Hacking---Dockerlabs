# Máquina Fileception

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image-2.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p21,22,80 -vvv -Pn 172.17.0.2
![alt text](image-1.png)

Entramos en ftp y descargamos la imagen hello_peter.jpg

![alt text](image.png)

Al entrar en la web me topé con una código que es de base85, lo descifré y era la contraseña para aplicar esteganografia:


![alt text](image-3.png)

herramienta para descifrar base85: https://www.dcode.fr/ascii-85-encoding

![alt text](image-4.png)

aplicando esteganografía:

el passphrase era: base_85_decoded_password

![alt text](image-5.png)

se extrajo el archivo you_find_me.txt y al abrirlo me mostró un codigo Ook! procedí a descifrarlo.

herramienta: https://www.dcode.fr/ook-language

![alt text](image-7.png)

### Intrusión

me conecté mediante ssh con el usuario peter y la contraseña anteriormente descifrada, luego hice ls y vi un archivo con el siguiente mensaje:

![alt text](image-6.png)

me fui a la carpte tmp y encontré lo siguiente:

![alt text](image-8.png)

y un archivo .odt, lo descargué con scp, luego le cambie la extensión por .zip y lo descomprimí

![alt text](image-9.png)

visualicé el archivo leerme.xml

![alt text](image-10.png)

y estaban las credenciales del usuario octopus, la contraseña era cifrada por base65, la descifré con cyberchef

![alt text](image-11.png)

### Escalar privilegios

me conecté por ssh e hice sudo -l

![alt text](image-12.png)



