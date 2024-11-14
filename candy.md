### Maquina

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)


## FUZZING WEB

gobuster dir -t 200 -u http://172.17.0.2:80-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

/media                (Status: 200) [Size: 31]
/templates            (Status: 200) [Size: 31]
/modules              (Status: 200) [Size: 31]
/index.php            (Status: 200) [Size: 7515]
/plugins              (Status: 200) [Size: 31]
/includes             (Status: 200) [Size: 31]
/images               (Status: 200) [Size: 31]
/language             (Status: 200) [Size: 31]
/README.txt           (Status: 200) [Size: 4942]
/components           (Status: 200) [Size: 31]
/cache                (Status: 200) [Size: 31]
/robots.txt           (Status: 200) [Size: 812]
/tmp                  (Status: 200) [Size: 31]
/LICENSE.txt          (Status: 200) [Size: 18092]
/layouts              (Status: 200) [Size: 31]
/administrator        (Status: 200) [Size: 9896]
/configuration.php    (Status: 200) [Size: 0]
/htaccess.txt         (Status: 200) [Size: 6456]
/cli                  (Status: 200) [Size: 31]

Entramos a robots.txt

http://172.17.0.2/robots.txt

entramos en /un_caramelo y vimos el siguiente comentario:

![alt text](image-4.png)

con cyberchef desciframos la contraseña

![alt text](image-3.png)

ejecutando whatweb me di cuenta que es un CMS Joomla

entonces ejcute el comando:

joomscan -u http://172.17.0.2/


entramos en administrator e iniciamos sesion con las credenciales anteriormente encontradas en /administrator

![alt text](image-5.png)

## Intrusion

Una vez iniciada la sesion como administrador, entramos en System > Templates > Administrator Templates > Atun Details and Files y editamos el archivo index.php y le agregamos la siguiente linea

nos ponemos en escucha con nc

encontramos un archivo otro_caramelo.txt en /var/backups/hidden

# $db_host = 'localhost';
# $db_user = 'luisillo';
# $db_pass = 'luisillosuperpassword';
# $db_name = 'joomla_db';

## Escalar Privilegios

Entre al usuario luisillo, con la contraseña encontrada.


![alt text](image-2.png)



