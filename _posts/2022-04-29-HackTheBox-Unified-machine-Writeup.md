---
title: Unified [HTB]
image: https://www.hackthebox.com/storage/avatars/525ba0e35574d9240e878bb8c716661e.png
tags: [HTB,Starting point]
published: false
---

Jorge Marco Arráez

## [](#header-3) 1)  What ports are open? 

```
Puerto 22: SSH
Puerto 6789: IBM-DB2
Puerto 8080: HTTP-PROXY
Puerto 8443: SSL/NAGIOS-NSCA
```

## [](#header-3) 2)  Name of the software that is running on the highest port? 

UniFi Network

## [](#header-3) 3)  What is the version of the software that is running? 

6.4.54

## [](#header-3) 4)  What is the CVE for the identified vulnerability? 

CVE-2021-44228

## [](#header-3) 5)  What is the version of Maven that we installed? 

```
3.6.3
```

## [](#header-3) 6)  What protocol does JNDI leverage in the injection? 

LDAP

## [](#header-3) 7)  What tool do we use to intercept the traffic, indicating the attack was successful? 

TCPDUMP

## [](#header-3) 8)  What port do we need to inspect intercepted traffic for? 

389

## [](#header-3) 9)  What port is the MongoDB service running on? 

27117

## [](#header-3) 10)  What is the default database name for UniFi applications? 

ace

## [](#header-3) 11)  What is the function we use to enumerate users within the database in MongoDB? 

db.admin.find()

## [](#header-3) 12)  What is the function to add data to the database in MongoDB? 

db.admin.insert()

## [](#header-3) 13)  What is the function we use to update users within the database in MongoDB? 

db.admin.update()

## [](#header-3) 14)  What is the password for the root user? 

NotACrackablePassword4U2022

## [](#header-3) 15)  Submit user flag 

```
user=6ced1a6a89e666c0620cdb10262ba127
```
## [](#header-3) 16)  Submit root flag 

```
root=e50bc93c75b634e4b272d2f771c33681
```

