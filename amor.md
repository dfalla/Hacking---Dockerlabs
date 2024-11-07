### Maquina amor

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64


## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-3.png)

## Entrando en la web

Encontramos 2 posibles usuarios, juan y carlota

## Ataque con hydra

![alt text](image.png)

## Intrusion

Nos conectamos por ssh con las credenciales calota, babygirl

![alt text](image-1.png)

Encontramos una imagen en: 
scp carlota@172.17.0.2:/home/carlota/Desktop/fotos/vacaciones

la descargamos la imagen a nuestro kali

desde kali ejecutamos el comando:

scp carlota@172.17.0.2:/home/carlota/Desktop/fotos/vacaciones/imagen.jpg ~/Downloads/

analice la imagen con:

steghide extract -sf imagen.jpg

me arrojo un secret.txt que luego lo descripte y me arrojo esta clave: eslacasadepinypon

## Cambiar al usuario oscar

su oscar y escribi la clave eslacasadepinypon


## Escalar privilegios

![alt text](image-2.png)


