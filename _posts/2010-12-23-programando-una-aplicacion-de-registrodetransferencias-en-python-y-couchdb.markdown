---
layout: post
title: !binary |-
  UHJvZ3JhbWFuZG8gdW5hIGFwbGljYWNpb24gZGUgUmVnaXN0cm9EZVRyYW5z
  ZmVyZW5jaWFzIGVuIFB5dGhvbiB5IENvdWNoREI=
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
{% include JB/setup %}

Una de las ventajas de ser programador es que puedes escribir uno mismo sus aplicaciones para resolver un problema determinado que se tenga, y pues yo tenia un problema :D . Resulta que mi unica conexion a internet es mediante un Modem USB, estos modem vienen con un software que solo funciona bajo Windows (algunos funcionan en MacOS) que te permite llevar un registro de las transferencias de datos consumidas y asi saber cuando estas a punto de consumirte tu cuota mensual de datos. Pues como solo uso <a href="http://blog.jam.net.ve/category/linux/">Linux</a> estos registros los llevava era en notas (tomboy) escribiendo los datos de subida y bajada que consumia despues de desconectarme.

<img class="aligncenter" title="Selección_011" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_011.jpeg" alt="" width="192" height="167" />

Este metodo que usaba me era un tanto engorroso y no era muy fiable ya que mas de una vez perdi algunas notas o las borraba accidentalmente. Luego de aprender las funciones mas basicas de CouchDB, Python y Couchdbkit se me ocurrio escribir una aplicacion de consola que me facilite el registro de mis transferencias y que los almacene en un entorno confiable.

Ya les e comentado [como instalar CouchDB en Ubuntu](http://blog.jam.net.ve/2010/12/12/instalando-couchdb-en-ubuntu/) y tambien como [instalar Couchdbkit y programar la primera aplicacion basica](http://blog.jam.net.ve/2010/12/13/instalando-couchdbkit-y-almacenando-datos-en-couchdb-desde-python), por lo que  si todavia no has instalado Couchdb y/o no tienes instalado Couchdbkit deberas pasar por estos articulos antes de continuar.

Como les decia, esta aplicacion de **RegistroDeTransferencias** es super basica y no es nada del otro mundo programarla. Al igual que la aplicacion anterior de Lista de Contactos  esta estara escrita en Python y usara el framework Couchdbkit para gestionar la conexion con la base de datos CouchDB.

Esta aplicacion que se ejecuta desde la terminal solicitara los datos de subida y bajada transferidos (en Mb), luego los mostrara para verificar que sean correctos y luego tras confirmar se almacenaran en CouchDB.  Al verificar en Futon (la interfaz de Administracion web de couchdb) los documentos creados ademas de ver los datos de subida y bajada previamente introducidos, veremos la fecha y hora en la que se almaceno ese documento. Estos dos ultimos datos se obtienen automaticamente desde la PC usando los modulos time y datetime de Python.  Esta aplicacion esta conformada por dos archivos: **registrodetransferencias.py** y **registrodetransferenciasapp.py**

El contenido de **registrodetransferencias.py** es:

{% highlight python %}
from couchdbkit.schema import Document
from couchdbkit.schema.properties import *
class registrodetransferencias(Document):
subida = FloatProperty()
bajada = FloatProperty()
fecha_agregado = StringProperty()
hora_agregado = StringProperty()
{% endhighlight %}

Y el Contenido de **registrodetransferenciasapp.py** es:

{% highlight python %}
#Importando los modulos necesarios
from datetime import *
from registrodetransferencias import registrodetransferencias
from couchdbkit import *
from time import *
print "Conectando al Servidor de Base de Datos..."
#Creando el objeto "Servidor" y colocando los datos de conexion
server = Server("http://usuario:contrasena@localhost:5984")
#Creando/Accesando a la base de dato (no tengo muy claro esto
#pero al parecer el metodo se encarga de verificar que la base
#de datos ya exista, si existe crea una session y se conecta
#si no existe crea la base de datos.
db = server.get_or_create_db("bdregistrodetransferencias")
la_subida = float(raw_input('Introdusca la cantidad de datos Enviados: '))
la_descarga = float(raw_input('Introdusca la cantidad de datos Recibidos: '))
print "Los datos ingresados son:"
print "Subida: " + str(la_subida)
print "Bajada: " + str(la_descarga)
respuesta = raw_input("Estos datos son correctos? introdusca solo (s/n): ")
if respuesta == "s":
#Asocia "Bookmark" a la base de datos (NPI LOL)
registrodetransferencias.set_db(db)
fecha = date.today()
#Los datos del documento a guardar.
registro = registrodetransferencias(
subida = la_subida,
bajada = la_descarga,
fecha_agregado = fecha.strftime("%d-%m-%y"),
hora_agregado = strftime("%I:%M %p")
)
print('Guardando el documento al Servidor CouchDB...')
#guargando el documento
registro.save()
print('Documento Guardado con EXITO!')
else:
print "Cancelado!!!"
{% endhighlight %}

**Nota:** no se mucho de programacion en Python (estoy aprendiendo) y tengo fallas en programacion orientada a objetos por lo que el programa puede contener errores o ser muy basico.

Como ven, es una aplicacion sumamente sencilla y facil de hacer muy similar a lista de contactos que se hizo en articulos anteriores. esta aplicacion podria ser mejorado por ejemplo si hacemos que el mismo programa tome los valores de subida y bajada de la PC y los almacene sin necesidad de que uno mismo los introdusca (similar a como se hace con la fecha y hora), pero todavia no encuentro la manera de hacer eso :-( .

Para ejecutarlo en la terminal tan solo escribimos en la misma:

{% highlight bash %}
python registrodetransferenciasapp.py
{% endhighlight %}

y veremos algo como esto:

<img class="aligncenter" title="Selección_018" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_018-300x233.jpg" alt="" width="300" height="233" />

Al ingresar en Futon para verificar los documentos creados veremos algo como esto:

<img class="aligncenter" title="Selección_019" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_019-300x88.jpg" alt="" width="300" height="88" />

Para visualizar de una forma sencilla en Futon los datos almacenados y/o calcular el total consumido podriamos usar las funciones Map/Reduce escritas en JavaScript, pero esto se los mostrare en otro articulo proximamente. :P

Si eres de los que no quieren tener una base de datos corriendo en su PC pero quieres probarla y aprender a usarla entonces estas de suerte ya que [CouchOne](http://www.couchone.com/get) y [Cloudant](https://cloudant.com/) ofrecen hosting Cloud de CouchDB Gratis!!! con lo que prodras tener una interfaz Futon online en donde administrar tus bases de datos.

Tambien has estado probando CouchDB ??? ya has realizado una aplicacion??? cuentanos tu experiencia con CouchDB!!!

Espero les sirva!!!
