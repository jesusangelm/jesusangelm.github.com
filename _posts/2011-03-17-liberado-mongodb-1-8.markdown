---
layout: post
title: !binary |-
  TGliZXJhZG8gTW9uZ29EQiAxLjg=
tags:
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  bGludXg=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  dWJ1bnR1
- !binary |-
  dW5peA==
- !binary |-
  YWN0dWFsaXphY2lvbg==
- !binary |-
  bWF2ZXJpY2s=
- !binary |-
  bm9zcWw=
- !binary |-
  bW9uZ29kYg==
---
Hace unas horas fue liberada una nueva versión estable de MongoDB, exactamente la versión 1.8 la cual trae una buena cantidad de mejoras muy importantes que muchos las estaban pidiendo a gritos.

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_024.jpeg"><img class="aligncenter size-medium wp-image-577" title="Selección_024" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_024-300x89.jpg" alt="" width="300" height="89" /></a>

Entre las novedades y mejoras están:

- Journaling. (hasta la versión 1.8RC3 se conocía con la opción --dur)

MongoDB ahora soporta escrituras Jounrnaling anticipadas para facilitar una rápida recuperación ante una caída y durabilidad en el motor de almacenamiento. Con journaling activado, una instancia MongoDB podría ser rápidamente reiniciada luego de un accidente sin la necesidad de reparar las colecciones.

- Soporte Map/Reduce Incremental.

Map/Reduce ahora soporta las nuevas opciones que permiten la actualización de las colecciones de forma incremental.

- Mejoras en el rendimiento de Sharding.

- Mejoras en Replica Set, incluyendo soporte para la autenticación.

- Búsquedas geográficas esféricas (¡La tierra no es plana!).

- Auto completado en la shell.

- Opción --discover en mongodbstat.

Entre otras mejoras.

Si ya tenias una <a title="MongoDB" href="http://blog.jam.net.ve/2011/01/03/instalando-mongodb-en-ubuntu/" target="_blank">versión anterior de MongoDB</a> (por ejemplo 1.6 en mi caso) debes saber que los repositorios de 10Gen fueron ligeramente cambiados, por lo que tal vez no aparezca la nueva versión en tu gestor de paquete. por lo tanto debemos eliminar los repositorios anteriores y añadir los nuevos, para esto tan solo debemos:

- abrir nuestro archivo <strong>/etc/apt/sources.list</strong> con tu editor favorito con permisos de <strong>root</strong> y luego de eliminar el repo anterior, añadir el nuevo repositorio de 10Gen colocando la siguiente linea:
<pre lang="bash" line="1" escaped="true">deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen</pre>
Luego de esto guardamos el cambio y nos vamos a la terminal para agregar la llave GPG respectiva tecleando:
<pre lang="bash" line="1" escaped="true">sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10</pre>
Luego de esto podemos actualizar el listado de paquetes
<pre lang="bash" line="1" escaped="true">sudo aptitude update</pre>
Bien aquí viene el detalle, si tienes instalado una anterior versión estable de mongodb como por ejemplo 1.6 en mi caso deberás saber que al instalar la version 1.8 aptitude desinstalara la versión 1.6 para instalar la nueva, por lo que para prevenir posibles daños seria bueno que hagas un respaldos de los datos que tienes en tu instancia mongodb. podría ser entrando como <strong>root</strong> en la carpeta <strong>/var/lib/mongodb</strong> y copiando los archivos (menos el <strong>mongod.lock</strong>) en otra carpeta. seria buena idea también respaldar el archivo <strong>/etc/mongodb.conf</strong> en el cual se guardan las configuraciones de mongodb. También es aconsejable que antes de hacer todo esto apagues mongodb por ejemplo con el comando:
<pre lang="bash" line="1" escaped="true">sudo service mongodb stop</pre>
Luego de haber tomado las precauciones, puedes instalar Mongodb 1.8 tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install mongodb-10gen</pre>
Durante el proceso de instalación tal vez te aparezca algo como esto:

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/03/Pantallazo-43.png"><img class="aligncenter size-medium wp-image-682" title="Pantallazo-43" src="http://blog.jam.net.ve/imagenes/uploads/2011/03/Pantallazo-43-300x96.png" alt="captura pantalla instalacion mongodb 1.8" width="300" height="96" /></a>

En este caso yo respondo con una "Y" para añadir el nuevo archivo mongodb.conf si lo deseas puedes responder "N" para mantener tu actual archivo o compara la nueva versión con la anterior ya respaldada y adaptar los cambios.

Cuando haya terminado la instalación ya tendrás instalada la nueva versión de MongoDB lista para usar. ahora tan solo revisa tus bases de datos para asegurarte de que tu información este completa.

Mas info en: la nota de <a title="liberacion de mongodb 1.8" href="http://www.mongodb.org/display/DOCS/1.8+Release+Notes" target="_blank">liberacion de MongoDB</a>
