---
title: Primeros pasos
published: true
---

# [](#header-1)De qué va esto

Llevo poco tiempo informandome sobre el Pentesting, pero creo que puedo dar una definición acertada de lo que es. Se trata de encontrar vulnerabilidades en una máquina y aprovecharlas para manipularla o extraer información de ella. 

## [](#header-2)Fases de un ataque

He visto que los ataques seguir una estructura similar:

1. Ver que tipo de dispositivo queremos atacar
1. Reconocer su S.O., ver que puertos están abiertos
1. Ver vulnerabilidades
1. Explotar esas vulnerabilidades
1. Pos-explotación, escalar privilegios
1. Reunir toda la información que hayamos encontrado

* * *

## [](#header-2)Software

Para reconocer los dispositivos de la red y ver que sistema operativo usan, he visto que NMAP es bastante útil. Tiene muchas opciones y aún tengo que profundizar en esta herramienta. He visto que incorpora scripts para determinar vulnerabilidades.

Para la fase de explotación, una herramienta muy útil es MetaSploit, aunque automatiza demasiado todos los procesos y tal vez no sea la mejor opción para aprender.

GoBuster o Dirbuster son útiles cuando nos interesa ver directorios de una página web donde tal vez halla más oportunidades para tomar el control de la máquina. 

Una herramienta muy usada también es NetCat, que permite poner en escucha al cliente por un puerto que le indiques. He visto que se suele usar cuando se quiere hacer una reverse shell, ya sea con php o con python. 

Aún no he resuelto ninguna máquina, pero cuando lo haga, subiré su writeup.



