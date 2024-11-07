### Máquina vacaciones

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image.png)

## Entrando por el puerto 80

Encontré el siguiente comentario

<!-- De : Juan Para: Camilo , te he dejado un correo es importante... -->

lo que me hace pensar que hay un usuario juan y un usuario camilo, y que dentro del email de camilo hay información útil
 
## Ataque conn hydra a ssh

![alt text](image-1.png)


## Intrusión

Nos conectamos por ssh con las credenciales anteriores encontradas de camilo

![alt text](image-2.png)

encontramos información útil en : /var/mail/camilo

![alt text](image-3.png)

## Conexión por ssh con el usuario juan y la contraseña encontrada: 2k84dicb

![alt text](image-4.png)

## Escalar privilegios

![alt text](image-5.png)

