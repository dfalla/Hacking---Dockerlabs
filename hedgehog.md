# Máquina hedgehog

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22 -vvv -Pn 172.17.0.2

### Entramos en la web

Encontramos la palabra tails

### Intrusión

Ataque de hydra a ssh

![alt text](image-1.png)

![alt text](image.png)

entramos por ssh con las credenciales encontradas.

### Escalar privilegios

![alt text](image-2.png)