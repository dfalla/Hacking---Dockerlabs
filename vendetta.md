### Maquina Vendetta

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,3306 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

## Ataque de hydra

hacemos tac /usr/share/wordlists/rockyou.txt > wordlists

eliminamos los caracteres especiales

hacemos un ataque co hydra al puerto 3306 de mysql

![alt text](image-2.png)

## Intrusión

Entramos mendiante mysql con el comando

mysql -h 172.17.0.1 -u V --password=ie168

ERROR 2026 (HY000): TLS/SSL error: SSL is required, but the server does not support it

mysql -h 172.17.0.1 -u V --password=ie168 --skip-ssl

![alt text](image-3.png)

![alt text](image-4.png)

Nos conectamos mediante ssh:

![alt text](image-5.png)

## Escalar privilegios

hacemos sudo -l

y tenemos privielegios sudo en /usr/bin/nano

entonces editamos el /etc/passwd y le eliminamos la x y luego ejecutamos el su root sin contraseña.

![alt text](image-6.png)