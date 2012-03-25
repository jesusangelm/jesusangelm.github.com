---
layout: post
title: !binary |-
  Q3JlYW5kbyB1bmEgQXBsaWNhY2lvbiBSdWJ5IE9uIFJhaWxzIHNlbmNpbGxh
  IGVuIGVsIENwYW5lbC4gW0Jhc2ljb10=
tags:
- !binary |-
  YmFt
- !binary |-
  aG9zdGluZw==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  dHV0b3JpYWw=
- !binary |-
  dmVuZXp1ZWxh
- !binary |-
  cG9ydGF0aWw=
- !binary |-
  cmFpbHM=
- !binary |-
  Y3BhbmVs
- !binary |-
  bWJy
- !binary |-
  cGFuZWw=
- !binary |-
  bWlncmFy
- !binary |-
  bXlzcWw=
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  cmVwcm9kdWN0b3I=
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  Y29udHJhc2XDsWE=
- !binary |-
  d2Vi
- !binary |-
  Y29tYW5kb3M=
- !binary |-
  YXJjaGl2b3M=
---
Desde hace casi un año vengo conociendo el lenguaje de programacion <a href="http://www.ruby-lang.org/es/" target="_blank">Ruby</a> y de su <a href="http://www.rubyonrails.org/" target="_blank">framework Rails</a> para la creacion de aplicaciones y paginas web respectivamente.  Hace solo unos meses pude aprender un poco mas sobre el framework Rails en la universidad y pude hacer unas paginas webs un tanto sencillas como practica. Estas paginas fueron hechas en una PC (modo local o localhost) con una aplicacion portatil llamada <a href="http://instantrails.rubyforge.org/wiki/wiki.pl" target="_blank">InstantRails</a> que contiene dentro de una misma carpeta todo lo necesario para comenzar a programar en Rails.

Despues de haber hecho unas cuantas paginas sencillas en local, quise dar el salto a un servidor e implementar dichas aplicaciones rails en lweb de modo que se tenga por internet.  Uno de los principales problemas que tube al intentar esto fue que no encontraba un proveedor de hosting que ofreciera soporte para Ruby On Rails y acceso a mi cuenta por medio de SSH. Luego de tanto buscar y toparme con unos cuantos resellers poco profesionales y sinceros, por fin encontre a dos proveedores que me ofrecen lo que se necesita para poder crear y/o montar una pagina web hecha en Ruby On Rails.

Como en internet no encontre mucha documentacion con los pasos a seguir para crear una aplicacion Ruby on Rails en el Cpanel, tube que pnerme a escudriñar por todo el Cpanel y SSH para lograr hacer lo que queria, asi que aqui les coloco los pasos a seguir para crear una aplicacion Ruby On Rails super sencilla:

Nota 1: Aqui se esta dando por entender que ya tienes acceso a una cuenta de  hosting que soporte Ruby On Rails y tengas acceso SSH ACTIVADO!!!   Si este no es tu caso (y eres de Venezuela), te puedo recomendar cualquiera de los dos que uso actualmente (Servidores en USA y Francia - Dueños en Venezuela y argentina - Pago en $ o Bs.F)

Nota 2: De aqui en adelante usaremos la abreviacion RoR para referirnos a Ruby On rails.

Nota 3: Damos por entendido de que se tiene conocimientos de conexion a un hosting por medio de cuentas Shell y sabes los comandos basicos.

Nota 4: Damos por entendido que el lector tiene conocimientos y experiencia del protocolo FTP y de su uso con los principales clientes FTP para realizar la conexion con su cuenta de hosting.

Nota 5: Damos por entendido que el lector  posee los conocimientos necesarios para crear bases de datos y usuarios de base de datos en el Cpanel de su hosting.

1- Lo primero es entrar al Cpanel, luego hacer click en la opcion "Ruby On Rails", acontinuacion colocas  en "Nombre de la Aplicacion" el nombre como quieres que se llame tu aplicacion RoR.  Seleccciona la casilla  que dice "Cargar en Boot" para que la aplicacion se autoarranque. elige en Enviroment "Development"  asi le dices a Rails que tu aplicacion esta en desarrollo y no es la version final en implementacion. ahora click en Crear.

<a href="http://blog.jam.net.ve/imagenes/r1/crearappsrailcpanel1.png"><img class="alignnone" title="Crear Apps Rails en Cpanel" src="http://blog.jam.net.ve/imagenes/r1/crearappsrailcpanel1.png" alt="" width="428" height="128" /></a>

Una vez creada la aplicacion podras ver mas abajo tu aplicacion ya creada, fijate que en el campo "Servidor de Vias" hay un link con una URL del tipo http://tudominio.com:12001/ o similar, esto es la direccion que se usa para accesar a tu aplicacion RoR.

Al lado en la misma pagina del Cpanel sale unos botones de PLAY y STOP similares a los de un  reproductor, esto es para ejecutar y poner en funcionamiento la aplicacion RoR o detenerla para que no este ejecutandose en el servidor y no sea accesible por internet.

<a href="http://blog.jam.net.ve/imagenes/r1/appsrailcreadascpanel2.png"><img class="alignnone" title="Apps Rails creada" src="http://blog.jam.net.ve/imagenes/r1/appsrailcreadascpanel2.png" alt="" width="432" height="84" /></a>

2- Bien ahora que tenemos lo necesario para nuestra aplicacion nos conectamos a nuestro hosting por medio de SSH con el nombre de usuario y contraseña que nos otorga el proveedor de hosting.

una vez conectados, nos situamos a la carpeta donde se creo la aplicacion ( normalmente se ubica en el directorio /etc/rails_app, asi que

[bash] cd etc/rails_apps/nombreaplicacion [/bash]

<a href="http://blog.jam.net.ve/imagenes/r1/shellappsrail3.png"><img class="alignnone" title="Shell" src="http://blog.jam.net.ve/imagenes/r1/shellappsrail3.png" alt="" width="403" height="39" /></a>

Una vez ubicados en la carpeta de nuestra aplicacion tecleamos el siguiente comando:

[rails] rails nombreaplicacion [/rails]

Esto nos creara la estructura de la aplicacion.

3- Luego de esto debemos crear el controlador de la pagina principal y sus respectivos campos de base de datos. en este caso, y debido a que este es un  tutorial super sencillo e optado por crear un formulario basico y sin mucho maquillaje en donde se solicite los datos de un alumno como nombre, apellido, cedula y se almacenen en la base de dato.   para crear esta estructura tecleamos

[rails] ruby script/generate scaffold alumno nombre:string apellido:string cedula:string [/rails]

esto nos creara los archivos html, ruby y estructura de la base de dato necesarios para que en la pagina se visualice el formulario solicitando esos datos.

-alumno es el nombre del controlador que contiene los campos apellido, nombre y cedula,  mas adelante este nombre lo usaremos pero en plural (alumnos) para accesar a nuestra pagina.

4- Ahora solo nos falta migrar la estructura de la base de datos al manejador de base de datos.  antes que nada debemos crear una base de datos y su respectivo usuario en el Cpanel de nuestra cuenta de hosting.

En mi caso use MySQL, asi que para conectar mi aplicacion RoR al servidor de bases de datos MySQL de mi hosting tube que editar el archivo database.yml para que pueda realizar dicha conexion. Este archivo se encuentra en directorio de tu aplicacion dentro de una carpeta llamada "config"  .../nombreaplicacion/config/database.yml

Para editarlo tan solo debemos descargarlo y abrirlo con nuestro editor de codigo favorito y lo editamos de modo que quede similar a este:

<a href="http://blog.jam.net.ve/imagenes/r1/databaseyml4.png"><img class="alignnone" title="Editando database.yml" src="http://blog.jam.net.ve/imagenes/r1/databaseyml4.png" alt="" width="435" height="197" /></a>

Una vez editado tan solo nos falta migrar la estructura antes mencionada a la base de datos creada en el Cpanel, para hacerlo tecleamos en la consola SSH:

[rails] rake db:migrate [/rails]

Esto nos debe haber creado las respectivas tablas en la base de datos MySQL.

5- Ahora tan solo debemos correr la aplicacion, para ello debemos dirigirnos de nuevo al Cpanel donde creamos la aplicacion, es decir en "Ruby On Rails"

<a href="http://blog.jam.net.ve/imagenes/r1/rorcpanel5.png"><img class="alignnone" title="Ruby On Rails en Cpanel" src="http://blog.jam.net.ve/imagenes/r1/rorcpanel5.png" alt="" width="415" height="191" /></a>

Recuerdas los botones verde que dice "Correr" debajo de la comlumna acciones ?, pues bueno le damos click alli para iniciar nuestra aplicacion RoR, una vez iniciada tan solo nos falta abrir el navegador  y visualizar nuestra pagina recien creada.  podemos ir a nuestra pagina dando click en el enlace que dice "URL" ubicado debajo del campo SERVIDOR DE VIAS.

si todo salio como esperabamos entonces deberias estar observando una pagina similar a esta.

<a href="http://blog.jam.net.ve/imagenes/r1/apprailcorriendo6.png"><img class="alignnone" title="pagina principal RoR" src="http://blog.jam.net.ve/imagenes/r1/apprailcorriendo6.png" alt="" width="500" height="354" /></a>

un momento aqui no sale los campos que habiamos creado,  esto se debe a que esta es la pagina perdeterminada que coloca Rails al crear una aplicacion, para ver la pagina que nosotros creamos tan solo debemos escribir en el navegador la url de nuestra aplicacion rails junto con el nombre de la tabla en plural de la base de datos que creamos.  nos deberia aparecer algo asi:

<a href="http://blog.jam.net.ve/imagenes/r1/appsrailcorriendo7.png"><img class="alignnone" title="Apps RoR Corriendo en Hosting" src="http://blog.jam.net.ve/imagenes/r1/appsrailcorriendo7.png" alt="" width="525" height="250" /></a>

Bueno eso es todo por los momentos, espero que les sirva tanto como a mi.

Saludos.
