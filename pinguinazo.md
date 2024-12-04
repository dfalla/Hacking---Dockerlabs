# Maquina Pinguinazo

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p5000 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Entrando a la web

![alt text](image-2.png)

es vulnerable a STTI, me puse en escucha por el puerto 443

### Escalar privilegios

Una vez ya conectado en la máquina hice sudo -l:

![alt text](image-3.png)

contenido del exploit.java

![alt text](image-4.png)
