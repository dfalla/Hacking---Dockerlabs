# Máquina Bashpariencias

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.18.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80,8899 -vvv -Pn 172.18.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.18.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

entramos a /form.html y encontramos las credenciales de rosa por ssh:

![alt text](image-3.png)

### Intrusión

Me conecté por ssh con las credenciales de rosa:

![alt text](image-4.png)

dentro de /home/rosa encontramos 2 archivos, uno llamado irresponsable.txt y otro llamado backup_rosa.zip

irresponsable.txt contenía lo siguiente:

![alt text](image-5.png)

el archivo backup_rosa.zip lo pasé a mi máquina kali, mediante scp y apliqué ataque de contraseña ya que tenía contraseña el archivo .zip, al descomprimirlo me arrojó un archivo password.txt que era la contraseña de juan

![alt text](image-6.png)


### Cambiando al usuario juan

siendo el usuario juan, hice sudo -l, luego pasé al usuario carlos y luego escalé a root.

![alt text](image-7.png)

### Escalar privilegios

siendo el usuario carlos, hice sudo -l

![alt text](image-8.png)
