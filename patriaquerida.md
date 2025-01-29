# Máquina Patriaquerida

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)


### Fuzzing web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -b 403,404 2>/dev/null

![alt text](image-3.png)


visitamos el index.php

![alt text](image-4.png)

vi el archivo .hidden_pass

![alt text](image-5.png)


### LFI

![alt text](image-2.png)

### Hydra

![alt text](image-6.png)

el archivo users contiene a los usuarios pinguino y mario que encontramos en el LFI

### Intrusión

Accedí con las credenciales encontradas

![alt text](image-7.png)

![alt text](image-8.png)

cambie al usuario mario

### Escalar privilegios

![alt text](image-9.png)
