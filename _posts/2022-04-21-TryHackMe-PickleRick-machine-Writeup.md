---
title: Máquina Picklerick
published: true
---

```json
{
    plataforma: TryHackMe,
    dificultad: easy,
    temas tratados: [http, netcat, comandos linux]
}
```

* * *

### [](#header-3)   1. Reconocimiento

![scan-nmap](../assets/capturas_maquinas/THM/picklerick/3-nmap.png)

Puertos abiertos:

```
- SSH: 22
- HTTP: 80
```

![pagina-web](../assets/capturas_maquinas/THM/picklerick/1-web.png)

![codigo-pagina](../assets/capturas_maquinas/THM/picklerick/2-codigo-web.png)

### [](#header-3)   2. Descubrimiento y escaneo

Vemos que el administrador se dejó ahí la contraseña: R1ckRul3s

Lanzo primero un escaneo rápido con nmap.

```
nmap --script=http-enum
```

Reporta que existe /login.php y /robots.txt

![login-php](../assets/capturas_maquinas/THM/picklerick/4-login.png)

Yendo a /robots.txt, encuentro lo siguiente:

![robots.txt](../assets/capturas_maquinas/THM/picklerick/5-robots.png)

Pruebo a ver si puedo iniciar sesión con Wubbalubbadubdub como contraseña y así es.

![commandpannel](../assets/capturas_maquinas/THM/picklerick/6-commandpanel.png)

Inspeccionando la página del panel de comandos veo que vuelve a haber un comentario, este acaba en ==, lo que me hace pensar que puede estar codificado en base64, ya que así es como se ve el padding. Tras pasarlo varias veces por un decodificador de base64 obtengo el siguiente resultado.

![rabbithole](../assets/capturas_maquinas/THM/picklerick/7-rabbithole.png)

Un rabbit hole, efectivamente.

### [](#header-3)   3. Evaluación de vulnerabilidades

Si en el panel de comandos ejecuto ls obtengo:

![ls](../assets/capturas_maquinas/THM/picklerick/8-ls.png)

Y al dirigirme a http://$IP/Sup3rS3cretPickl3Ingred.txt

Obtengo el primer ingrediente:

```
mr. meeseek hair
```
![1er-ingrediente](../assets/capturas_maquinas/THM/picklerick/9-primeringrediente.png)

Con sudo -l veo que puedo ejecutar cualquier comando, así que trato de obtener una reverse shell.

![sudo-l](../assets/capturas_maquinas/THM/picklerick/10-sudo-l.png)
![reverse](../assets/capturas_maquinas/THM/picklerick/11-reverse.png)

Estamos dentro. 

### [](#header-3)   4. Explotación

Tras estabilizar la shell con:

```py
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Puedo buscar más ingredientes para la poción de Rick. 
Puedo a acceder a /home/rick y allí veo el segundo ingrediente.

![2o-ingrediente](../assets/capturas_maquinas/THM/picklerick/12-second-flag.png)

Veo que hay un directorio /root, pero no puedo acceder si no soy root.

### [](#header-3)   5. Escalada

Como puedo ejecutar todos los comandos, pruebo sudo /bin/bash y da resultado. 
Ahora solo tengo que navegar a la carpeta /root y ya tengo el tercer ingrediente.

![escalada-tercera](../assets/capturas_maquinas/THM/picklerick/13-escalada-tercera-flag.png)


### [](#header-3)   6. Evaluación

Picklerick es una máquina en la que he podido ejecutar todos los comandos de Linux que he necesitado, lo que ha hecho muy fácil conseguir una reverse shell. 
He intentado usar netcat para subir linpeas.sh a la máquina, pero la escalada de privilegios era mucho más sencillo que eso.

![pwn](../assets/capturas_maquinas/THM/picklerick/14-pwn.jpg)




