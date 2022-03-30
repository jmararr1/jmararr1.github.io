---
title: Máquina Crocodile
published: true
---

Jorge Marco Arráez

## [](#header-3) 1)  What nmap scanning switch employs the use of default scripts during a scan? 

-sC

## [](#header-3) 2)   What service version is found to be running on port 21? 

vsftpd 3.0.3


## [](#header-3) 3)  What FTP code is returned to us for the "Anonymous FTP login allowed" message? 

230

## [](#header-3) 4)  What command can we use to download the files we find on the FTP server? 

get

## [](#header-3) 5)  What is one of the higher-privilege sounding usernames in the list we retrieved? 

```
ls
get allowed.userlist
get allowed.userlist.passwd
```

admin

## [](#header-3) 6)  What version of Apache HTTP Server is running on the target host? 

2.4.41

## [](#header-3) 7)  What is the name of a handy web site analysis plug-in we can install in our browser? 

wappalyzer

## [](#header-3) 8)  What switch can we use with gobuster to specify we are looking for specific filetypes? 

-x

## [](#header-3) 9) What file have we found that can provide us a foothold on the target? 

```
gobuster -x php -u $IP -w common.txt
```

login.php

## [](#header-3) 10)

Aquí simplemente pongo las credenciales que he obtenido en el paso 5.

```
flag=c7110277ac44d78b6a9fff2232434d16
```
