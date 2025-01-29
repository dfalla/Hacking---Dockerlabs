# Máquina sjd

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -b 403,404 2>/dev/null


![alt text](image-2.png)

Entramos en /pass.txt

![alt text](image-3.png)

desencriptamos las claves con cyberchef

sjd -> sjd

admin -> admin

root -> 1971

nos conectamos por ssh con el usuario root:

### Intrusión y Escalar privilegios

![alt text](image-4.png)