# Máquina cachopo

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Entrando a la web

Encontré un formulario

![alt text](image-2.png)

Lo que se me ocurrió fue interceptarlo con burpsuite al formulario.

![alt text](image-3.png)

al interceptarlo lo mandé al repeater y me aparece el mensaje de error de la derecha, lo que significa que interpreta texto en base64.

![alt text](image-4.png)

le mandé el código de arriba:

![alt text](image-5.png)

y efectivamente lee base64, entonces hice:

para ver los usuarios:

![alt text](image-6.png)

![alt text](image-7.png)

### Intrusión
Como ya tenía el usuario cachopin, lo que hice fue hacer fuerza bruta con hydra al servicio ssh:

hydra -l cachopin -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -t 64 -I

![alt text](image-8.png)

Ingresamos por ssh con las credenciales encontradas:

![alt text](image-9.png)

### Escalar privilegios:

En /home/cachopin/app/com/personal encontré hashes de SHA1, entonces utilicé la herramienta:

https://github.com/PatxaSec/SHA_Decrypt

![alt text](image-10.png)

![alt text](image-11.png)

hice su root y ingresé la contraseña cecina:

![alt text](image-12.png)

