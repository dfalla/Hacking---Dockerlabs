# Máquina chocolatefire

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,5222,5223,5262,5263,5269,5270,5275,5276,7070,7777,9090 -vvv -Pn 172.17.0.2



### Entrando en la web

entramos por el puerto 9090

![alt text](image-1.png)


### Intrusión y Escalar privilegios

Usamos metasploit con el exploit:

exploit/multi/http/openfire_auth_bypass_rce_cve_2023_32315

![alt text](image-2.png)

![alt text](image-3.png)

