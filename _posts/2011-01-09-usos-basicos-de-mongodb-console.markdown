---
layout: post
title: !binary |-
  VXNvcyBiYXNpY29zIGRlIE1vbmdvREIgQ29uc29sZQ==
tags:
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  dGVybWluYWw=
- !binary |-
  bm9zcWw=
- !binary |-
  bW9uZ29kYg==
---
Y seguimos con mas pruebas de <a href="http://blog.jam.net.ve/category/nosql/">NoSQL</a> :D ... Hace unos dias comentaba como <a href="http://blog.jam.net.ve/2011/01/03/instalando-mongodb-en-ubuntu/">instalar MongoDB en Ubuntu 10.10</a>, ahora veremos algunos usos basicos de la consola de administracion que incluye MongoDB para almacenar informacion, hacer algunas consultas entre otras tareas administrativas.

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_024.jpeg"><img class="aligncenter size-medium wp-image-577" title="Selección_024" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_024-300x89.jpg" alt="" width="300" height="89" /></a>

Para acceder a la consola administrativa de MongoDB tan solo debemos escribir en la teminal:
<pre lang="bash" line="1" escaped="true">mongo</pre>
esto nos devolvera:
<pre lang="text" line="1" escaped="true">MongoDB shell version: 1.6.5
connecting to: test</pre>
Al hacer esto ejecutaremos la consola de MongoDB la cual por defecto intenta conectarse a la instancia MongoDB local (en tu PC) por lo que conviene tener MongoDB ejecutandoce con anterioridad. Cuando arrancamos la consola de esta manera y sin parametros, la misma se conecta a una base de datos llamada "<strong>test</strong>" en la que podemos hacer nustras primeras pruebas, esto lo podemos comprobar ejecutando el siguiente comando:
<pre lang="bash" line="1" escaped="true">db</pre>
lo cual nos devolvera el nombre de la base de datos en la qeu estamos la cual es <strong>test</strong>.

<strong>Creando/Usando una base de datos</strong>:

Para crear la nueva base de datos llamada "pruebas" tan solo debemos escribir el siguiente comando:
<pre lang="bash" line="1" escaped="true">use pruebas</pre>
esto nos devolvera algo como:
<pre lang="text" line="1" escaped="true">&gt; use pruebas
switched to db pruebas</pre>
Este comando creara la base de datos "pruebas" y nos movera hacia ella, una detalle en este comando es que si por ejemplo la base de datos ya existe, tan solo nos mueve hacia ella para poder usarla, en caso de no existir la base de dato, el sistema la crea.

<strong>Creando Colecciones e insertando documentos:</strong>

Como les comentaba en el articulo "<a href="http://blog.jam.net.ve/2011/01/03/instalando-mongodb-en-ubuntu/">instalando MongoDB en Ubuntu</a>"  MongoDB es una base de datos del tipo documentos en la que almacena dichos  documentos en una especie de agrupaciones conocidas como colecciones, estas colecciones vendrian siendo algo asi como las tablas en MySQL.

Para crear una coleccion llamada "<strong>prueba01</strong>" y y almacenar documentos en ella podemos usar el siguiente comando de ejemplo:
<pre lang="bash" line="1" escaped="true">db.prueba01.insert({titulo: "Primera prueba", contenido: "Mi primera prueba de insercion de un documento"})</pre>
en donde:

- <strong>prueba01</strong> es el nombre de la coleccion donde se encuentra el documento.

- <strong>{titulo: "Primera prueba", contenido: "Mi primera prueba de insercion de un documento"} </strong>es el documento que estamos insertando en la coleccion.

Podemos añadir mas documentos en formato JSON con campos iguales o diferentes al que  acabamos de añadir y estos seran almacenados sin ningun problema, justamente esta es una de las ventajas de las bases de datos NoSQL.
<pre lang="bash" line="1" escaped="true">db.prueba01.insert({titulo: "Segunda prueba", contenido: "Mi segunda prueba de insercion de un documento", hora: "03:20 PM", fecha: "9/01/2011"})</pre>
<strong>Mostrar los documentos almacenados en una coleccion:</strong>

Para ver todos los documentos almacenados en nuestra coleccion <strong>prueba01</strong> podemos usar el siguiente comando:
<pre lang="bash" line="1" escaped="true">db.prueba01.find()</pre>
lo cual nos devolvera algo como esto:
<pre lang="bash" line="1" escaped="true">{ "_id" : ObjectId("4d2a1f5f9d3ceffc299d0fad"), "titulo" : "Primera prueba", "contenido" : "Mi primera prueba de insercion de un documento" }
{ "_id" : ObjectId("4d2a223b9d3ceffc299d0fae"), "titulo" : "Segunda prueba", "contenido" : "Mi segunda prueba de insercion de un documento", "hora" : "03:20 PM", "fecha" : "9/01/2011" }</pre>
en nuestro caso solo hemos almacenado dos documento y esto es lo unico que nos muestra. pero si por ejemplo queremos ver solo un resultado podemos ejecutar el siguiente comando:
<pre lang="bash" line="1" escaped="true">db.prueba01.findOne()</pre>
el cual nos devolvera algo como:
<pre lang="bash" line="1" escaped="true">{
 "_id" : ObjectId("4d2a1f5f9d3ceffc299d0fad"),
 "titulo" : "Primera prueba",
 "contenido" : "Mi primera prueba de insercion de un documento"
}</pre>
<strong>Listando las bases de datos:</strong>

Si queremos obtener un listado de las bases de datos que estan en nuestra instancia MongoDB tan solo tecleamos:
<pre lang="bash" line="1" escaped="true">show dbs</pre>
y esto nos mostrara las bases de datos que tenemos... en nuestro caso puede devolvernos:
<pre lang="text" line="1" escaped="true">&gt; show dbs
admin
local
pruebas
test</pre>
<strong>Listando las colecciones en una base de datos</strong>:

Para obtener un listado de las colecciones almacenadas en la base de datos en la que nos encontramos podemos teclear:
<pre lang="bash" line="1" escaped="true">show collections</pre>
el cual nos devolvera
<pre lang="text" line="1" escaped="true">&gt; show collections
 perros
 prueba01</pre>
<strong>Consultas "super basicas"</strong>:

usando el comando <strong>db.prueba01.find()</strong> podemos realizar una consulta sencilla pasandole al metodo <strong>find()</strong> un parametro el cual sera un documento, este documento sera una especie de ejemplo de lo que queremos que sea buscado. Por ejemplo si queremos que se nos muestre el documento en donde esta contenida la Key/Value <strong>"hora" : "03:20 PM"</strong> podemos pasarle eso mismo como documento:
<pre lang="bash" line="1" escaped="true">db.prueba01.find({"hora" : "03:20 PM"})</pre>
esto nos devolvera el segundo documento que añadimos hace un rato y en el cual contiene el campo hora : 03:20 PM:
<pre lang="bash" line="1" escaped="true"> &gt; db.prueba01.find({"hora" : "03:20 PM"})
{ "_id" : ObjectId("4d2a223b9d3ceffc299d0fae"), "titulo" : "Segunda prueba", "contenido" : "Mi segunda prueba de insercion de un documento", "hora" : "03:20 PM", "fecha" : "9/01/2011" }</pre>
Por supuesto, esta es una consulta super basica, MongoDB incluye muchas maneras de realizar consultas de este tipo (pasando un documento JSON como parametro), pero uno de los metodos mas potentes es usando funciones <strong>Map/Reduce</strong> un tanto parecido a como se hace en CouchDB.

<strong>Eliminando documentos:</strong>

Para eliminar un documento podemos realizarlo de manera similar a como hicimos la consulta anterior, es decir pasar un documento JSON como parametro a una funcion, solo que en este caso la funcion se llama <strong>remove()</strong>:
<pre lang="bash" line="1" escaped="true">db.prueba01.remove({"hora" : "03:20 PM"})</pre>
Este comando nos elimino el documento que contenia el campo "hora" : "03:20 PM" de la coleccion. prueba a realizar la consulta anterior y veras que ya no aparece dicho documento en la coleccion.

Por supuesto MongoDB y su consola interactiva tiene muchas otras caracteristicas y funciones que requeririan un libro entero para ser explicada en detalle.

como complemento podemos usar el comando:
<pre lang="text" line="1" escaped="true">help</pre>
para visualizar un listado de comandos que podemos usar en la consola MongoDB.

Si deseas aprender mas sobre MongoDB visita:

- <a href="http://www.mongodb.org/display/DOCSES/Vistazo+a+la+consola+interactiva+MongoDB">Vistaso a la consola interactiva MongoDB</a>.

- <a href="http://www.mongodb.org/display/DOCSES/Operaciones+DBA+desde+la+consola">Operaciones DBA desde la consola</a>.

- <a href="http://www.mongodb.org/display/DOCSES/Referencia+de+la+consola+%28dbshell%29">Referencias de la consola.</a>

- <a href="http://www.mongodb.org/display/DOCSES/Consultar">Consultas.</a>