---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBNb25nb0RCIGVuIFVidW50dQ==
tags:
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  bm9zcWw=
- !binary |-
  bW9uZ29kYg==
---
Despues de unos cuantos articulos dedicados a la Base de Datos <a href="http://blog.jam.net.ve/category/nosql/">NoSQL</a> <a href="http://blog.jam.net.ve/tag/couchdb/">CouchDB</a> pasare a comentarles algunas pruebas que e realizado usando MongoDB

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_024.jpeg"><img class="aligncenter size-medium wp-image-577" title="Selección_024" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_024-300x89.jpg" alt="" width="300" height="89" /></a>

<a href="http://www.mongodb.org">MongoDB</a> es otro de los sistemas de bases de datos NoSQL, similar a CouchDB que a tenido mayor popularidad, este sistema de base de datos algunos los llaman "La MySQL de las NoSQL" y esto es porque a parte de tener la aceptacion y popularidad que tubo MySQL en sus inicios, MongoDB comparte muchas caracteristicas que son similares a las ya vistas en MySQL pero orientada a el movimiento NoSQL.  Una de estas caracteristicas por ejemplo es que en MongoDB no existen Tablas (claro es una NoQSL) pero si existen Colecciones las cuales podrian ser algo asi como las tablas, solo que estas no se rigen por ningun esquema predefinido  y cualquier coleccion puede contener muchos documentos  con distintos campos. Esto es algo que en lo personal me a gustado mucho en MongoDb ya que ayudan a organizar y clasificar mejor la informacion almacenada ademas de facilitar las consultas y agilizar las mismas.

MongoDB es tambien una base de datos NoSQL orientada a documentos, por lo que estos documentos son muy similares a los ya vistos en CouchDB en formato JSON, pero añadiendo algunos tipos de datos adicionales como date, object id, binary data, code, etc. Se dice (nolo e comprobado todavia) que MongoDB ofrece un rendimiento en inserciones mucho mayor que CouchDB y un poco mejor que MySQL a cosa de sacrificar caracteristicas como las transacciones. MongoDB a diferencia de CouchDB no incluye una interfaz web para administrar nuestros documentos e informacion, en su lugar nos ofrece una Shell para manejar desde ella la instancia de manera muy similar a la shell en MySQL.  Pero al igual que como hacemos con MySQL podemos instalar alguna interfaz de administracion web para administrar. Lo que si podemos encontrar en MongoDB  es una interfaz de administracion para monitorear la instancia y en la que podemos observar informaciones basicas del servidor MongoDB, esta interfaz la podemos encontrar en:
<pre lang="text" line="1" escaped="true">http://localhost:28017</pre>
Un ejemplo de documento en MongoDB seria algo como esto:
<pre lang="bash" line="1" escaped="true">{ "_id" : ObjectId("4d2219e103a143a4cd4b1205"), "nombre" : "Angel", "nick" : "JamUnix", "web" : "www.jam.net.ve" }</pre>
Para instalar MongoDB en <a href="http://blog.jam.net.ve/tag/ubuntu/">Ubuntu</a> 10.10 debemos agregar su respectivo repositorio en nuestro sources.list, para ello usaremos nuestro editor favorito y agregaremos el repo respectivo a la distribucion que usemos:
<pre lang="bash" line="1" escaped="true">sudo nano /etc/apt/sources.list</pre>
y agregamos el repo correspondiente a Ubuntu 10.10 el cual es:
<pre lang="bash" line="1" escaped="true">deb http://downloads.mongodb.org/distros/ubuntu 10.10 10gen</pre>
Nota: Si usas otra version de Ubuntu revisa el <a href="http://www.mongodb.org/display/DOCS/Ubuntu+and+Debian+packages">listado de repos disponibles.</a>

Luego de esto debemos agregar la llave GPG del repo:
<pre lang="bash" line="1" escaped="true">sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10</pre>
ahora tan solo actualizamos el listado de paquetes con:
<pre lang="bash" line="1" escaped="true">sudo aptitude update</pre>
e instalamos MongoDB con:
<pre lang="bash" line="1" escaped="true">sudo aptitude install mongodb-stable</pre>
Con esto tendremos MongoDB instalado y ejecutandose en nuestra PC :D

Si deseas aprender mas acerca de MongoDB puedes visitar:

- <a href="http://www.mongodb.org/display/DOCSES/Inicio">Documentacion Oficial en Español</a>.

- Articulo: <a href="http://4tic.com/es/blog/40-blgo/69-mongodb-la-mysql-del-nosql">MongoDB La MySQL de las NoSQL</a> en 4tic.com

Proximamente publicare mas articulos en los que explicare algunos usos basicos de la Shell de MongoDB, como podemos instalarnos alguna interfaz de administracion web y como podriamos crear una aplicacion en Python que almacene datos en MongoDB :P
