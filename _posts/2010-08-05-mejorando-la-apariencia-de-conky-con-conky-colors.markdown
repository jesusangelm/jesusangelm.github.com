---
layout: post
title: !binary |-
  TWVqb3JhbmRvIGxhIGFwYXJpZW5jaWEgZGUgQ29ua3kgY29uIENvbmt5IENv
  bG9ycw==
tags:
- !binary |-
  Z25vbWU=
- !binary |-
  Z3VpYQ==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  Y29ua3k=
- !binary |-
  bW9uaXRvcg==
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  cGFuZWw=
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  Y29tYW5kb3M=
- !binary |-
  dGVybWluYWw=
---
Hace unos dias me dio por intentar mejorar la apariencia de mi panel de <a href="http://blog.jam.net.ve/tag/conky/" target="_self">conky</a> en mi <a href="http://blog.jam.net.ve/tag/ubuntu/" target="_self">Ubuntu </a>y navegando por internet encontre una buena aplicacion llamada Conky Colors que nos permite configurar y personalizar de manera sencilla el script para el panel de conky.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-5.png"><img class="aligncenter size-medium wp-image-357" title="Pantallazo-5" src="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-5-157x300.png" alt="" width="157" height="300" /></a>

Para hacer esto lo primordial es tener conky instalado, si todavia no lo has hecho entonces lee mi guia de: <a href="http://blog.jam.net.ve/2009/12/21/instalando-conky-en-ubuntu-karmic/" target="_blank">como instalar conky en Ubuntu.</a>

Una vez instalado conky necesitamos descargarnos algunas dependencias y utilidades que debemos tener para que funcione correctamente Conky Colors, Para esto tecleamos en la terminal

[bash] sudo apt-get install python-statgrab ttf-droid curl [/bash]

Luego de esto nos <a href="http://gnome-look.org/content/show.php/CONKY-colors?content=92328" target="_self">descargamos Conky Colors</a> desde Gnome-Look. Una ves este descargado lo descomprimes y usando la terminal navegamos hasta la carpeta resultante y en ella teclamos:

[bash] make [/bash]

Bien les explico un poco, el metodo de uso de Conky colors consiste en que este nos muestra mediante un comando una serie de comandos u opciones disponibles, luego estos comandos lo podremos ejecutar en la terminal para que conky colors nos genere el script a usar en el archivo .conkyrc para que este nos configure el panel con las funciones que hemos elegido anteriormente.

Para ver las opciones que nos ofrece Conky Colors tecleamos en la terminal:

[bash] ./conky-colors --help [/bash]

alli podremos ver todas las funciones disponibles que podemos agregar a nuestro panel de conky. Un ejemplo de funciones que podemos usar es este y creamos el script tecleando en la terminal:

[bash] ./conky-colors --lang=spanish --theme=ambiance --cpu=2 --cputemp --swap --updates --hdtemp1=sda --proc=3 --clock=modern --calendar --m --network --ubuntu [/bash]

Bien ahora para aplicar esta configuracion a nuestro panel conky tecleamos en la terminal:

[bash] make install [/bash]

Ya con esto  deberia haberse aplicado el script en el archivo .conkyrc y debe haber configurado conky con las funciones elegidas.

si por casualidad no tienes conky corriendo lo iniciamos tecleando en la terminal

[bash] conky [/bash]

Si todo a ido bien deberia ver un panel conky similar al de la captura arriba.

Como funcion adicional podriamos hacer que nustro panel conky nos muestre por ejemplo la temperatura del CPU y la del disco duro eligiendo las opciones --cputemp  y --hdtemp1=sda tal cual vemos en el comando de configuracion mas arriba, pero para que esto funcione correctamente tu disco duro y procesador debe tener dicha funcion (casi todos la tiene), ser soportado y tener instalado y configurado los siguientes paquetes de monitoreo el cual podemos instalar tecleando en la terminal:

[bash] sudo apt-get install lm-sensors hddtemp [/bash]

luego de instalado los paquetes lm-sensors debemos configurarlo tecleando en la terminal:

[bash] sudo sensors-detect [/bash]

y le damos a "y" todas las veces que nos lo solicite.

Bien ahora para iniciar el sensor tecleamos:

[bash]  sudo /etc/init.d/module-init-tools start [/bash]

Para hacer que hddtemp funcione en nuestro ubuntu 10.04 tecleamos:

[bash] sudo chmod u+s /usr/sbin/hddtemp [/bash]

y reiniciamos.

Saludos y espero les sirva. :-D
