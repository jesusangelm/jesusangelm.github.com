---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBDb3VjaGRia2l0IHkgYWxtYWNlbmFuZG8gZGF0b3MgZW4g
  Q291Y2hEQiBkZXNkZSBQeXRob24=
tags:
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  bm9zcWw=
- !binary |-
  Y291Y2hkYg==
- !binary |-
  cHl0aG9u
- !binary |-
  Y291Y2hkYmtpdA==
---
Ayer les comentaba que tenia meses leyendo sobre CouchDB, sus usos y <a href="http://blog.jam.net.ve/2010/12/12/instalando-couchdb-en-ubuntu/">como instalarlo en Ubuntu</a>. Pues hoy les mostrare como instalar Couchdbkit y como crear una sencilla aplicacion de ejemplo que almacena informacion en nuestra base de datos CouchDB.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_011.jpeg"><img class="aligncenter size-full wp-image-523" title="Selección_011" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_011.jpeg" alt="" width="192" height="167" /></a>

Para los que no saben, <a href="http://couchdbkit.org/">Couchdbkit</a> es un Framework que le permite a nuestras aplicaciones Python conectarse a una base de datos CouchDB.

Para instalar Couchdbkit  podemos valernos de <strong>easy_install</strong> por lo que debemos instalarlo primero (en caso que no lo tengas ya) tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">curl -O http://peak.telecommunity.com/dist/ez_setup.py</pre>
luego de esto tecleamos:
<pre lang="bash" line="1" escaped="true">sudo python ez_setup.py -U setuptools</pre>
y por ultimo instalamos Couchdbkit tecleando:
<pre lang="bash" line="1" escaped="true">sudo easy_install -U Couchdbkit</pre>
Ya con esto tendremos instalado Couchdbkit y podremos usarlo para conectar todas nuestras aplicaciones a un sistema de base de datos NoSQL CouchDB.

Bien la aplicacion de ejemplo que e realizado para demostrar como podemos usar Couchdkit junto con Python es una sencilla <strong>Lista de Contactos</strong> que se ejecutara desde la terminal,  esta aplicacion solicitara diferentes datos de un contacto y los almacenara en una base de datos CouchDB. Esta aplicacion esta conformada por dos archivos, uno llamado <strong>contactos.py</strong> y el otro <strong>contactosapp.py</strong>

El contenido de el archivo <strong>contactos.py</strong> es el siguiente:
<pre lang="python" line="1" escaped="true">from couchdbkit.schema import Document
from couchdbkit.schema.properties import *

class contactos(Document):
 nombre = StringProperty()
 apellido = StringProperty()
 correo = StringProperty()
 telefono = StringProperty()
 fecha_agregado = StringProperty()</pre>
y el codigo correspondiente para contactosapp.py es el siguiente:
<pre lang="python" line="1" escaped="true">#Importando los modulos necesarios
from datetime import *
from contactos import contactos
from couchdbkit import *

print "Conectando al Servidor de Base de Datos..."
#Creando el objeto "Servidor" y colocando los datos de conexion
server = Server("http://usuario:contrasena@localhost:5984")

#Creando/Accesando a la base de dato (no tengo muy claro esto
#pero al parecer el metodo se encarga de verificar que la base
#de datos ya exista, si existe crea una session y se conecta
#si no existe crea la base de datos.
db = server.get_or_create_db("listacontactos")
#cambiar listacontactos por el nombre de tu base de datos.

el_nombre = raw_input('Introdusca el Nombre de su nuevo contacto: ')
el_apellido = raw_input('Introdusca el Apellido de su nuevo contacto: ')
el_correo = raw_input('Introdusca el Correo de su nuevo contacto: ')
el_telefono = raw_input('Introdusca el Telefono de su nuevo contacto:')

print "Nombre: " + el_nombre
print "Apellido: " + el_apellido
print "Correo: " +el_correo
print "Telefono: " +el_telefono

#Asocia "Bookmark" a la base de datos (NPI LOL)
contactos.set_db(db)

fecha = date.today()
#Los datos del documento a guardar.
contacs = contactos(
 nombre= el_nombre,
 apellido    = el_apellido,
 correo = el_correo,
 telefono = el_telefono,
 fecha_agregado=fecha.strftime("%d-%m-%y")
)

print('Guardando el documento al Servidor CouchDB...')
#guargando el documento
contacs.save()
print('Documento Guardado con EXITO!')</pre>
<strong>Nota:</strong> no se mucho de programacion en Python (estoy aprendiendo) y tengo fallas en programacion orientada a objetos por lo que el programa puede contener errores o ser muy basico.

estos dos archivos los podemos guardar (con extencion .py ) juntos en una carpeta y desde la terminal lo ejecutamos de este modo:
<pre lang="bash" line="1" escaped="true">python contactosapp.py</pre>
con esto te solicitara los datos del contacto (nombre, apellido, correo y telefono), generara el documento y lo almacenara en la base de datos CouchDB  :-)

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_014.jpeg"><img class="aligncenter size-medium wp-image-537" title="Selección_014" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_014-300x180.jpg" alt="" width="300" height="180" /></a>

Aqui podemos ver la aplicacion ejecutandose... y como pueden observar es sumamente sencilla. Si ahora abrimos Futon en el navegador y observamos nuestra base de datos nos encontraremos con el documento recien almacenado que contienen los datos del contacto que acabamos de añadir:

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_015.jpeg"><img class="aligncenter size-medium wp-image-538" title="Selección_015" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_015-300x96.jpg" alt="" width="300" height="96" /></a>

Si eres de los que no quieren tener una base de datos corriendo en su PC pero quieres probarla y aprender a usarla entonces estas de suerte ya que <a href="http://www.couchone.com/get">CouchOne</a> y <a href="https://cloudant.com/">Coudant</a> ofrecen hosting Cloud de CouchDB Gratis!!! con lo que prodras tener una interfaz Futon online en donde administrar tus bases de datos.

Si quieres descargar la aplicacion de ejemplo haz click <a href="http://blog.jam.net.ve/guias/democontactos.zip">Aqui!</a>

Tambien has estado probando CouchDB ??? ya has realizado una aplicacion??? cuentanos tu experiencia con CouchDB!!! :D

Espero les sirva tanto como a mi...
