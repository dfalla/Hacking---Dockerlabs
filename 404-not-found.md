# Máquina 404-not-found

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

agregamos al /etc/hosts

404-not-found.hl

![alt text](image-2.png)


### Encontrando subdominios

wfuzz -H "Host: FUZZ.404-not-found.hl" -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://404-not-found.hl --hw=28 

![alt text](image-3.png)

lo agregamos al /etc/hosts

![alt text](image-4.png)

al ingresar a info.404-not-found.hl, me di con la sorpresa de que se trata de un login.

![alt text](image-5.png)

al hacer ctrl + u

![alt text](image-6.png)

entonces probé LDAP Injection:

![alt text](image-7.png)

![alt text](image-8.png)

logré entrar y también visualizar las credenciales de ssh:

![alt text](image-9.png)

### Intrusión

Me conecté por ssh con las credenciales encontradas.

![alt text](image-10.png)

visualicé todos los usuarios del sistema:

![alt text](image-11.png)

ejecuté sudo -l

![alt text](image-12.png)

migrar al usuario 200-ok:

![alt text](image-13.png)


### Escalar privilegios

siendo el usuario 200-ok entramos a /home/200-ok

visualicé el archivo boss.txt que decia rooteable, y asumí que era la contraseña de root

entonces:

![alt text](image-14.png)