---
title: Máquina Fawn
published: true
---

Segunda máquina en HackTheBox

## [](#header-4)Procedimiento

```
IP máquina: 10.129.245.20
export IP=10.129.245.20
```

1.  What does the 3-letter acronym FTP stand for? 
```
file transfer protocol
```
 
1.  What communication model does FTP use, architecturally speaking? 
```
client-server model
```

1.  What is the name of one popular GUI FTP program? 
```
filezilla
```

1.  Which port is the FTP service active on usually? 
```
21 tcp
```

1.  What acronym is used for the secure version of FTP? 
```
sftp
```


1.  What is the command we can use to test our connection to the target? 

```
ping
```


1.  From your scans, what version is FTP running on the target? 

nmap -Pn -A  -sV -p 21 -oN nmap/initial $IP

```
vsftpd 3.0.3
```

1.  From your scans, what OS type is running on the target? 

```
unix
```

1.  Obtain the root flag

```
035db21c881520061c53e0536e44f815
```