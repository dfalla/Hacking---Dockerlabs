# Máquina Extraviado

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 172.17.0.2

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22 -vvv -Pn 172.17.0.2

![alt text](image-1.png)

### Fuzzing web

No encontré nada

### Entramos en la web

![alt text](image-2.png)

al hacer ctrl + u

![alt text](image-3.png)

desencriptando con cyberchef => daniela : focaroja

### Intrusión

Mediante ssh con las credenciales daniela : focaroja

![alt text](image-4.png)

al hacer ls -la encontré una carpeta oculta llamada secreto que contenia un archivo llamado passdiego lo desencripté con cyberchef

![alt text](image-5.png)

siendo el usuario diego en la ruta: /home/diego/.local/share/.- encontré la password para root

![alt text](image-6.png)

respuesta del acertijo osoazul

![alt text](image-7.png)
