# Maquina Psycho

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

### LFI

![alt text](image-2.png)

![alt text](image-3.png)

le sacamos el id_rsa al usuario vaxei:

![alt text](image-4.png)

lo guardamos en un archivo le di el permiso 600 y luego ejecuté:

ssh -i id_rsa vaxei@172.17.0.1

### Escalar privilegios:

![alt text](image-5.png)


![alt text](image-6.png)