---
layout: post
title: !binary |-
  RWplbXBsb3MgZGUgdmlzdGFzL2NvbnN1bHRhcyBlbiBDb3VjaERC
tags:
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  dmlzdGE=
- !binary |-
  bm9zcWw=
- !binary |-
  Y291Y2hkYg==
- !binary |-
  Y29uc3VsdGFz
---
Continuando con mis practicas y articulos sobre CouchDB traigo ahora algunos ejemplos de vistas/consultas para mostrar nuestros datos almacenados, recordemos que en CouchDB las vistas se crean usando funciones escritas en el lenguaje JavaScript, aunque se puede usar otros lenguajes como Ruby, Python, etc mediante plugins.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_011.jpeg"><img class="aligncenter size-full wp-image-523" title="Selección_011" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_011.jpeg" alt="" width="192" height="167" /></a>

Las vistas que crearemos a continuacion sera para consultar y organizar los datos almacenados por la <a href="http://blog.jam.net.ve/2010/12/23/programando-una-aplicacion-de-registrodetransferencias-en-python-y-couchdb/">aplicacion RegistroDeTransferencias</a> la cual explique hace unos dias, por lo que recomiendo que primero sigas dicho articulo antes de continuar para que asi no estes tan perdido.

Como comentaba anteriormente cuando programaba la <a href="http://blog.jam.net.ve/2010/12/23/programando-una-aplicacion-de-registrodetransferencias-en-python-y-couchdb/">aplicacion de RegistroDeTransferencias</a>, la misma almacenaba en CouchDB los datos de <strong>subida</strong> y <strong>bajada</strong> transferidos durante una sesion, ademas de almacenar tambien la <strong>fecha</strong> y<strong> hora</strong>.

Para crear vistas en CouchDB primero debemos ingresar en Futon, seleccionar nuestra base de datos y luego en el listbox "<strong>View</strong>" de la parte superior derecha seleccionar "<strong>Temporary view...</strong>"  Una vez alli veremos una seccion llamada "<strong>View Code</strong>" la cual contiene dos cajas de textos, una llamada "<strong>Map Function</strong>" en donde escribiremos la mayoria de nuestras funciones Map para crear vistas, y otra caja de texto llamada "<strong>Reduce Function</strong>" en donde podremos escribir funciones Reduce que filtren, realicen operaciones u organicen mejor los datos seleccionados por las funciones Map, Estas funciones Reduce son opcionales y no son estrictamente necesarias a menos que algun caso especial las requiera. si te fijas bien ya esta escrito una funcion en la caja de texto Map, esta es uan funcion de ejemplo muy basica que luego de presionar el boton "<strong>Run</strong>" nos mostrara en el campo "<strong>Value</strong>" todos los documentos en la base de datos

Una vista sencilla que podriamos programar podria ser por ejemplo aquella en la que me muestre todos los registros de <strong>bajada</strong> organizado por <strong>fecha</strong> y <strong>hora</strong>. Esta vista la podriamos hacer escribiendo lo siguiente en el textbox de las funciones Map:
<pre lang="javascript" line="1" escaped="true">function(doc) {
emit([doc.fecha_agregado, doc.hora_agregado], doc.bajada);
}</pre>
Esta funcion nos devolvera algo como esto:

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_020.jpeg"><img class="aligncenter size-medium wp-image-566" title="Selección_020" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_020-300x156.jpg" alt="" width="300" height="156" /></a>

Como podemos ver, en el campo Key (llave) nos muestra la fecha y hora en la que se tomo el documento y en el campo Value (valor) nos muestra los datos de <strong>bajada</strong> para cada documento en la base de datos. de forma similar podemos crear una vista para mostrar los valores de <strong>subida</strong>. Esta funcion nos sirve por ejemplo para ver cuantos datos nos descargamos en X dia.

Una de las bellezas de CouchDB es que estas vistas podemos almacenarlas en la misma base de datos para asi consultarla cuando lo queramos sin necesidad de volver a escribir la misma funcion :D esto lo hacemos haciendo click en el boton "<strong>Save As...</strong>" y en "<strong>Desing document:</strong>" colocamos un nombre cualquiera que nos identifique el uso de esas consultas (algo asi como una categoria de consultas), por ejemplo: "<strong>vista_subida-bajada</strong>" y en "<strong>View Name:</strong>" colocamos el nombre de la vista que acabamos de escribir, por ejemplo: "<strong>bajada</strong>".

Otro ejemplo de vistas que podemos crear es una en la que por ejemplo muestre unicamente los datos de subida (en el campo Key) y bajada (en el campo Value), esta vista la podriamos ver escribiendo lo siguiente en el campo Map Function:
<pre lang="javascript" line="1" escaped="true">function(doc) {
emit({Subida: doc.subida}, {Bajada: doc.bajada});
}</pre>
Esto nos devolvera algo como:

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_021.jpeg"><img class="aligncenter size-medium wp-image-567" title="Selección_021" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_021-300x155.jpg" alt="" width="300" height="155" /></a>

Como podemos ver se le a agregado la leyenda Subida y Bajada junto a los datos de subida y bajada para asi identificarlos mejor.

Bien hasta ahora hemos usado dos sencillas funciones Map pero ninguna combinada con una funcione Reduce, bien es hora de ver como son estas fuciones y un ejemplo de uso de las mismas. :D

Una vista que podriamos escribir usando funciones Map y Reduce podria ser aquella en la que nos muestre el valor total de datos de bajada, esto se haria por ejemplo selecionando todos los documentos con la llave bajada y luego haciendo una sumatoria de sus valores, la funcion <strong>Map</strong> seria algo como esto:
<pre lang="javascript" line="1" escaped="true">function(doc) {
emit("bajada", doc.bajada);
}</pre>
y la funcion Reduce seria algo como esto:
<pre lang="javascript" line="1" escaped="true">function (key, values, rereduce) {
return sum(values);
}</pre>
Esto nos mostrara algo como esto:

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_022.jpeg"><img class="aligncenter size-medium wp-image-568" title="Selección_022" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_022-300x76.jpg" alt="" width="300" height="76" /></a>

Como vemos solo nos devuelve una sola fila con la leyenda Bajada en el campo Key y en el campo Value nos muestra la suma total de los datos de <strong>bajada</strong>; 2.498Mb :O y mi plan es de 3000Mb estoy casi qeu sin internet :( LOL.

Este mismo ejemplo podemos usarlo para calcular el consumo total de <strong>subida</strong>.

Por ultimo podriamos hacer una modificacion a la ultima funcion para mostrar y calcular de una sola vez y en una misma vista los datos tanto de subida como de bajada :P

la funcion Map seria algo como esto:
<pre lang="javascript" line="1" escaped="true">function(doc) {
emit("subida", doc.subida);
emit("bajada", doc.bajada);
}</pre>
Y la funcion Reduce seria algo como:
<pre lang="javascript" line="1" escaped="true">function (key, values, rereduce) {
return sum(values);
}</pre>
Esto nos mostrara algo como:

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_023.jpeg"><img class="aligncenter size-medium wp-image-569" title="Selección_023" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_023-300x85.jpg" alt="" width="300" height="85" /></a>

Como podemos observar esto nos mostrara dos filas en la que vemos el total de datos de <strong>subida</strong> como el total de datos de <strong>bajada </strong>en el campo Value ademas de su respectiva leyenda en el campo Key.

Bien esto es todo por el momento pero no es para nada complejo ya que estas mismas vistas las podemos usar desde la aplicacion RegistroDeTransferencia para que sea desde ella misma donde hagamos las consultas previamente creadas y asi no tener que estar visitando Futon cada vez que queramos ver y consultar nuestra informacion en la base de datos, pero eso es algo en lo que estoy practicando y aprendiendo asi que por lo tanto se los muestrare en otra ocasion :D

Tambien has estado probando CouchDB ??? ya has realizado una aplicacion??? cuentanos tu experiencia con CouchDB!!!

Saludos y espero les sirva!!!
