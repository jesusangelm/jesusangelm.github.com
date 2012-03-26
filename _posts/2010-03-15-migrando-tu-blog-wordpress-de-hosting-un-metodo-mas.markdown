---
layout: post
title: !binary |-
  TWlncmFuZG8gdHUgYmxvZyBXb3JkcHJlc3MgZGUgaG9zdGluZyAtIFVuIG1l
  dG9kbyBtYXM=
tags:
- !binary |-
  YmFt
- !binary |-
  YmxvZw==
- !binary |-
  aG9zdGluZw==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  cmVzcGFsZG8=
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  c29mdHdhcmU=
- !binary |-
  d2luZG93cw==
- !binary |-
  Y3BhbmVs
- !binary |-
  bWJy
- !binary |-
  cGFuZWw=
- !binary |-
  bWlncmFy
- !binary |-
  d29yZHByZXNz
- !binary |-
  bXlzcWw=
- !binary |-
  cGhw
- !binary |-
  cGhwbXlhZG1pbg==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  bWF5bw==
- !binary |-
  YmFzaA==
- !binary |-
  c2VndXJpZGFk
- !binary |-
  ZG5z
- !binary |-
  Y29udHJhc2XDsWE=
- !binary |-
  aW1wb3J0YXI=
- !binary |-
  ZXhwb3J0YXI=
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
- !binary |-
  YXJjaGl2b3M=
- !binary |-
  cmVzdGF1cmFjaW9u
---
Desde que empece este blog e tenido que aprender por mi cuenta y en ocasiones de mala manera la administracion, uso y configuracion de Wordpress. Una de las cosas que tube que aprender a hacer y que en un principio siempre me daban fallos al realizarlas es migrar el blog de hosting. Como ninguno de mis lectores saben y ya han podido leer aqui, hubo un tiempo en el que tenia <a href="http://blog.jam.net.ve/2009/08/17/de-nuevo-problemas-con-el-hosting/">innumerables problemas</a> con mi anterior proveedor de hosting el cual me migraba a cada rato de servidor para intentar solventar la situacion.  En esas migraciones el traslado del contenido del blog y la base de datos se hacia sacando backups con las herramientas del panel de control web cPanel y luego eran restauradas en el nuevo servidor, No se porque pero siempre me quedaba mal el blog luego de estas migraciones y restauraciones mediante cPanel.

Uno de los motivos de estos errores me di cuenta que era que al migrar la base de datos esta quedaba con la vieja ruta de la cuenta de hosting en donde estaba el contenido del blog en el servidor, por lo que en el nuevo servidor si esta ruta no era la misma, se terminaba el mundo :D

Bien luego de esto y en otro proceso de migracion de servidor mas, me propuse hacerlo yo mismo y a mi modo y paso a explicar:

- Primero que nada debemos realizar un respaldo de los archivos del blog, si tu blog esta en una carpeta podemos comprimir esta y descargarla para luego trasladarla al nuevo servidor. Esto lo podemos hacer por medio del cPanel con la herramienta "Administrador de Archivos", seleccionamos la carpeta con el contenido del blog y le damos a "Comprimir"
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/boton-aac.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/migrarwphosting/boton-aac.png" alt="" width="201" height="55" /></a></p>
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/comp.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/migrarwphosting/comp.png" alt="" width="142" height="80" /></a></p>
- Luego de esto debemos sacar un respaldo a la Base de Datos del blog, esto lo podemos hacer usando el PhpMyAdmin que esta en el cPanel, dandole a la pestaña "Exportar" luego seleccionamos la base de datos en el recuadro del lado superior izquierdo y marcamos la opcion "SQL" en la parte inferior izquierda. Si deseamos comprimir la base de datos la comprimimos seleccionando cualquiera de los dos formatos disponibles y le damos a continuar. Esto nos iniciara la descarga de la base de datos de nuetro blog.
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/boton-pmac.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/migrarwphosting/boton-pmac.png" alt="" width="158" height="62" /></a></p>
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/etiq-impexp.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/migrarwphosting/etiq-impexp.png" alt="" width="225" height="62" /></a></p>
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/sql-exp.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/migrarwphosting/sql-exp.png" alt="" width="196" height="181" /></a></p>
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/pma-comp.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/migrarwphosting/pma-comp.png" alt="" width="1212" height="127" /></a></p>
Antes que nada deberiamos verificar que en el nuevo servidor nuestro directorio home se llame igual que en el servidor anterior,  esto en cPanel lo podemos verificar en el panel superior izquierda en donde dice "Directorio Home" si es el mismo podemos pasar a importar la base de datos en el nuevo servidor por medio de phpMyAdmin, de lo contrario debemos editar la base de datos como explico a continuacion.

- Bien una vez descargada la base de datos pasamos a abrir el archivo .sql en tu editor de codigo favorito (si usas Windows y la base de datos es de unos cuantos megas no uses el blog de notas, simplemente no esta hecho para esto) y buscamos la linea en donde este la direccion de nuestro directorio home.  es algo similar a esto:

[bash] /home/usuarioviejoservidor/public_html/blog/ [/bash]

y cambiamos el nombre de usuario para que quede

[bash]/home/usuarionuevoservidor/public_html/blog/[/bash]

una vez editada la base de datos guardamos los cambios y podemos proceder a importarla en el nuevo servidor por medio de phpMyAdmin seleccionando la pestaña "Importar" y luego agregando la ruta de la base de datos en nuestra pc por medio del boton "Browse".  le damos al boton "Continuar".
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/imp-sql.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/migrarwphosting/imp-sql.png" alt="" width="705" height="122" /></a></p>
si todo a ido bien deberiamos tener importada con exito la base de datos de nuetro blog en el nuevo servidor.

- Ahora debemos importar en el nuevo servidor los archivos de nuestro blog, para hacer esto podemos subir el archivo comprimido por medio de nuestro cliente FTP favorito o tambien por medio de la terminal situandonos en la raiz de nuestra carpeta web publica (public_html o httpd o html) usando el comando "wget" de este modo:

[bash] wget http://www.tuviejohosting.com/archivos-blog.zip [/bash]

una ves transferido los archivos al nuevo hosting debemos descomprimirlo, para esto podemos usar de nuevo el "Administrador de archivos" en el cPanel, seleccionamos el archivo compromido y le damos a la opcion "Extraer".
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/comp.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/migrarwphosting/comp.png" alt="" width="142" height="80" /></a></p>
- Bien ahora solo nos falta configurar la nueva conexion entre el blog y la base de datos, para esto debemos crear el usuario de la base de datos en el nuevo servidor y otorgarles sus respectivos privilegios, esto lo podemos hacer en el mismo cPanel en la opcion "MySql Basesde Datos".
<div><a href="http://blog.jam.net.ve/imagenes/migrarwphosting/boton-mc.png"></a></div>
<p style="text-align: center;"><img class="alignnone" src="http://blog.jam.net.ve/imagenes/migrarwphosting/boton-mc.png" alt="" width="198" height="51" /></p>
<p style="text-align: center;"></p>

<div>Como nombre de usuarios puedes usar los mismos que tenias en el anterior hosting, al igual que la contraseña (aunque es aconsejable cambiarla para mayor seguridad).  Tambien en esta misma seccion del cPanel debemos añadir el usuario que acabas de crear a la base de datos que acabamos de importar para que este sea el que tenga privilegios de uso de esa base de datos en especifico.</div>
<div></div>
<div>- Bien por ultimo ya solo debemos  editar el archivo wp-config.php de nuestro blog y agregar los nuevos datos de conexion como el nombre de la base de datos, el usuario y la contraseña.  Una vez listo tan solo debemos subirlo y remplazarlo por el que ya estaba en el nuevo hosting con la informacion del viejo servidor.</div>
<div></div>
<div>Bien para este momento ya deberia estar todo bien y funcionando correctamente, pero si como yo tienes las url de los permalinks (enlaces permanentes) personalizadas, deberas apuntar tu viejo dominio a el nuevo hosting y esperar a que los cambios en los DNS se rieguen por todo internet para poder ver correctamente el contendido del blog y para que puedan funcionar los enlaces. Esto por lo general dura como mucho unas horas o mas, pero tambien puede que este en mucho menos tiempo, asi que tan solo queda esperar y listo.</div>
<div></div>
<div>Saludos y espero que les haya servido tanto como a mi.</div>