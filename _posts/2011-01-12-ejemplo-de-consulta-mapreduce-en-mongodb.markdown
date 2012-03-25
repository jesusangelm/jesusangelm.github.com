---
layout: post
title: !binary |-
  RWplbXBsbyBkZSBjb25zdWx0YSBNYXAvUmVkdWNlIGVuIE1vbmdvREI=
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
<a href="http://blog.jam.net.ve/category/nosql/">NoSQL</a> hasta en la sopa!!! :)

Hace unos articulos atras les mostre un ejemplo de como podriamos usar <a href="http://blog.jam.net.ve/tag/python/">Python</a> y el driver PyMongo para almacenar informacion en MongoDB, el ejemplo que vimos fue mi aplicacion de <a href="http://blog.jam.net.ve/2011/01/10/almacenando-datos-en-mongodb-desde-python/">RegistroDeTransferencias</a>. Al final de dicho articulo  explico como podriamos ver y consultar los datos almacenados usando la consola interactiva de MongoDB, pero... ¿y si queremos que sea la misma aplicacion que nos muestre algunas consultas?. Pues a eso vamos, en este articulo haremos que RegistroDeTransferencias nos muestre el total de datos de subida y bajada.

Para que nuestra aplicacion nos muestre esta informacion necesitamos crear dos funciones <strong>Map/Reduce</strong> escritas en JavaScript.

La funcion <strong>Map</strong> para los datos de <strong>subida</strong> seria algo como esto:
<pre lang="javascript" line="1" escaped="true">ms = Code("""function() {
 emit("Subida", this.subida);
 }""")</pre>
y su funcion Reduce seria algo como:
<pre lang="javascript" line="1" escaped="true">rs = Code("""function(k, v) {
 var i, sum = 0;
 for (i in v) {
 sum += v[i];
 }
 return sum;
 }""")</pre>
<strong>Nota</strong>: Para que el metodo <strong>Code()</strong> que contiene las funciones <strong>Map/Reduce</strong> funcione es necesario hacer uso del modulo <strong>BSON</strong> e importar <strong>Code</strong>, por lo que al inicio del archivo debemos agregar lo siguiente:
<pre lang="python" line="1" escaped="true">from bson.code import Code</pre>
En la funcion <strong>Map (ms)</strong> lo que hara sera seleccionarnos todos registros del campo <strong>subida</strong> en nuestra coleccion y emitirlos como parametro <strong>VALUE</strong>, mientras que la funcion <strong>Reduce (rs)</strong> recibira como parametro en  la <strong>KEY VALUE (v)</strong> los registros de <strong>subida</strong> que seleccionamos en nuestra funcion <strong>Map</strong> y a continuacio en una secuencia for, sumara todos los valores de subida existentes, lo que nos devolvera el total de subida.

Para ejecutar nuestras funciones Map/Reduce y hacer que nos genere y muestre la informacion que solicitamos debemos agregar en nuestra aplicacion lo siguiente:
<pre lang="python" line="1" escaped="true">print "Sumatoria de SUBIDA"
 resultado = colsubida.map_reduce(ms, rs)

 for subida in resultado.find():
 print subida</pre>
Como podemos ver, se elige la coleccion colsubida que contiene los registros de subida y a continuacion usamos el metodo <strong>map_reduce()</strong> pasandole como parametro nuestras funciones <strong>Map (ms)</strong> y funcion <strong>Reduce (rs)</strong>. Luego de esto la recorremos en un for y mostramos el resultado.

De forma similar podriamos usar otra funcion <strong>Map/Reduce</strong> para mostrar el total de bajada, si modificamos el codigo de la aplicacion RegistroDeTransferencias y añadimos lo que hemos visto, nos quedaria algo como esto:
<pre lang="python" line="1" escaped="true">from pymongo import *
from datetime import *
from time import *
from bson.code import Code

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
 print "Cancelado!!!"

respuesta = raw_input("Deseas ver la sumatoria de subida/bajada? (s/n): ")
if respuesta == "s":
 ms = Code("""function() {
 emit("Subida", this.subida);
 }""")

 rs = Code("""function(k, v) {
 var i, sum = 0;
 for (i in v) {
 sum += v[i];
 }
 return sum;
 }""")

 mb = Code("""function() {
 emit("Bajada", this.bajada);
 }""")

 rb = Code("""function(k, v) {
 var i, sum = 0;
 for (i in v) {
 sum += v[i];
 }
 return sum;
 }""")

 print "Sumatoria de SUBIDA"
 resultado = colsubida.map_reduce(ms, rs)

 for subida in resultado.find():
 print subida

 print "Sumatoria de BAJADA"
 resultado = colbajada.map_reduce(mb, rb)

 for bajada in resultado.find():
 print bajada

else:
 print "Cancelado!!!"</pre>
Al ejecutar la aplicacion y responder afirmativamente a la pregunta "Deseas ver la sumatoria de subida/bajada? (s/n): " veremos algo similar a esto:
<pre lang="text" line="1" escaped="true">Deseas ver la sumatoria de subida/bajada? (s/n): s
Sumatoria de SUBIDA
{u'_id': u'Subida', u'value': 126.10999999999999}
Sumatoria de BAJADA
{u'_id': u'Bajada', u'value': 805.0}</pre>
Como vemos, no es muy dificil realizar consultas <strong>Map/Reduce</strong> en <a href="http://blog.jam.net.ve/tag/mongodb/">MongoDB</a>, aunque comparandola a como lo haciamos en <a href="http://blog.jam.net.ve/tag/couchdb/">CouchDB</a> es un tanto mas largo y posiblemente engorroso.

Lo bueno de esto es que, esta misma consulta podriamos realizarla tal cual, hacer que nos devuelva unicamente solo numeros y no un documento JSON ({u'_id': u'Subida', u'value': 126.10999999999999}) si usamos un ODM :D y lo mejor,  sin usar funciones Map/Reduce lo que hara tambien que nuestra aplicacion tenga menos lineas de codigo... Pero esto se los mostrare proximamente :P

Saludos y espero les sirva!.
