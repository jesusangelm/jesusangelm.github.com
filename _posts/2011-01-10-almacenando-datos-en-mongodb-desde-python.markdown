---
layout: post
title: !binary |-
  QWxtYWNlbmFuZG8gZGF0b3MgZW4gTW9uZ29EQiBkZXNkZSBQeXRob24=
tags:
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  bm9zcWw=
- !binary |-
  cHl0aG9u
- !binary |-
  bW9uZ29kYg==
---
Mas <a href="http://blog.jam.net.ve/category/nosql/">NoSQL</a> :D ... luego de ver como <a href="http://blog.jam.net.ve/2010/12/13/instalando-couchdbkit-y-almacenando-datos-en-couchdb-desde-python/">almacenabamos informacion en CouchDB desde una aplicacion en Python</a>, veremos como hacer lo mismo pero esta vez enviando los datos a una base de datos MongoDB.

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_024.jpeg"><img class="aligncenter size-medium wp-image-577" title="Selección_024" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_024-300x89.jpg" alt="" width="300" height="89" /></a>

Para este caso usaremos la misma aplicacion de <a href="http://blog.jam.net.ve/2010/12/23/programando-una-aplicacion-de-registrodetransferencias-en-python-y-couchdb/">RegistroDeTransferencias</a> que programe anteriormente y que almacena los datos en CouchDB, solo que esta vez modificare el codigo para que almacene la informacion en MongoDB. :P

Para poder conectar nuestras aplicaciones Python a MongoDB y que estas utilicen dicha base de datos NoSQL para almacenar la informacion necesitamos del driver correspondiente el cual se llama <a href="http://api.mongodb.org/python">PyMongo</a>. Para instalar el driver para python en Ubuntu lo haremos de forma similar a como lo hicimos con CouchDB usando  Easy_Install, para esto abrimos una terminal y escribimos:
<pre lang="bash" line="1" escaped="true">sudo easy_install pymongo</pre>
Ya con esto tendremos instalado Pymongo y podremos comenzar a usarlo para que nuestras aplicaciones en python se conecten a MongoDB.

Como les decia, la aplicacion que usaremos en este ejemplo es mi aplicacion de <strong>RegistroDeTransferencias</strong> que programe anteriormente y que almacena los datos en CouchDB, pero luego de hacerle unos pequeños cambios pasara a almacenar la informacion en MongoDB. La aplicacion se compone de un simple archivo llamado <strong>rdtmongo.py</strong> y el codigo es el siguiente:
<pre lang="python" line="1" escaped="true">from pymongo import *
from datetime import *
from time import *

print "Conectando al Servidor de Base de Datos Local..."
conexion = Connection() # Conexion local por defecto

#conexion = Connection("usuario:contraseña@servidor.com:27075/basededato") #Conexion a un servidor remoto

#creando/obteniendo un objeto que referencie a la base de datos.
db = conexion['bdregistrodetransferencias'] #base de datos a usar

#creando/obteniendo un objeto que referencie a la coleccion.
colbajada = db['bajada'] #coleccion con registros de bajada
colsubida = db['subida'] #coleccion con registros de subida

#solicitando los datos de subida y bajada
la_subida = float(raw_input('Introdusca la cantidad de datos Enviados: '))
la_descarga = float(raw_input('Introdusca la cantidad de datos Recibidos: '))

# obteniendo la fecha, hora y almacenandolas en variables.
fecha = date.today()
fecha_agregado = fecha.strftime("%d-%m-%y")
hora_agregado = strftime("%I:%M %p")

print "Los datos ingresados son:"
print "Subida: " + str(la_subida)
print "Bajada: " + str(la_descarga)
print "Fecha Agregado " + fecha_agregado
print "Hora Agregado " + hora_agregado
respuesta = raw_input("Estos datos son correctos? introdusca solo (s/n): ")

if respuesta == "s":
#creando el diccionario con los documentos de subida y bajada
 registrobajada = {"bajada": la_descarga, "fecha_agregado": fecha_agregado, "hora_agregado": hora_agregado}
 registrosubida = {"subida": la_subida, "fecha_agregado": fecha_agregado, "hora_agregado": hora_agregado}

#insertando los datos en la BD
 colbajada.insert(registrobajada)
 colsubida.insert(registrosubida)
 print('Documento Guardado con EXITO!')

else:
 print "Cancelado!!!"</pre>
Como ven es una aplicacion super sencilla y basica, en este ejemplo yo separe los registros de subida y bajada en en dos colecciones <strong>subida</strong> y <strong>bajada</strong> almacenadas en la base de datos <strong>bdregistrodetransferencias</strong> de esta forma los registros en la base de datos quedan mejor organizados y nos ayuda a la hora de buscar o consultar un documento.

Para ejecutar esta aplicacion en la terminal tan solo tecleamos:
<pre lang="bash" line="1" escaped="true">python rdtmongo.py</pre>
y veremos algo como esto

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_027.jpeg"><img class="aligncenter size-medium wp-image-593" title="Selección_027" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_027-300x248.jpg" alt="" width="300" height="248" /></a>

Si nos vamos a la consola interactiva de MongoDB y nos movemos a la base de datos bdregistrodetransferencias:
<pre lang="bash" line="1" escaped="true">use bdregistrodetransferencias</pre>
podremos ver las colecciones tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">show collections</pre>
tambien podremos ver todos los documentos de la coleccion <strong>subida</strong> y <strong>bajada</strong> teclando:
<pre lang="bash" line="1" escaped="true">db.subida.find()</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">db.bajada.find()</pre>
respectivamente, lo cual nos devolvera algo como esto:
<pre lang="text" line="1" escaped="true">{ "_id" : ObjectId("4d2150de5ff0885b8b000001"), "subida" : 2.9, "fecha_agregado" : "03-01-11", "hora_agregado" : "12:00 AM" }
{ "_id" : ObjectId("4d2164dd5ff0887868000001"), "subida" : 7.02, "fecha_agregado" : "03-01-11", "hora_agregado" : "01:25 AM" }
{ "_id" : ObjectId("4d2221855ff0884395000001"), "subida" : 5.57, "fecha_agregado" : "03-01-11", "hora_agregado" : "02:50 PM" }
{ "_id" : ObjectId("4d22b1505ff08829ab000001"), "subida" : 11.4, "fecha_agregado" : "04-01-11", "hora_agregado" : "01:04 AM" }</pre>
Por supuesto podriamos ejecutar consultas simples para visualizar los datos de subida y bajada o consultas Map/Reduce para calcular un total de datos de subida o bajada consumidos, pero eso se los mostrare proximamente :D

Tambien has estado probando MongoDB ??? ya has realizado una aplicacion??? cuentanos tu experiencia con MongoDB!!!
