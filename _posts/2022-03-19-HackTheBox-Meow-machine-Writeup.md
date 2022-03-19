---
title: Máquina Meow
published: true
---

Primera máquina en HackTheBox

## [](#header-1)Procedimiento

# IP máquina: 10.129.245.20
# export IP=10.129.245.20

1)  What does the acronym VM stand for? 

'''
Virtual Machine
'''

2) What tool do we use to interact with the operating system in order
to start our VPN connection?

'''
terminal
'''

3)  What service do we use to form our VPN connection? 

'''
openvpn
'''

4) What is the abreviated name for a tunnel interface in the output of your VPN boot-up sequence output? 

'''
tun
'''

5) What tool do we use to test our connection to the target? 

'''
ping
'''

6) What is the name of the tool we use to scan the target's ports? 

'''
nmap
'''

7) What service do we identify on port 23/tcp during our scans? 

'''
telnet
'''

8) What username ultimately works with the remote management login prompt for the target? 

'''
root
'''

9) Submit root flag

telnet $IP
meow login: root
ls
cat flag.txt

'''
b40abdfe23665f766f9c61ecba8a4c19
'''
