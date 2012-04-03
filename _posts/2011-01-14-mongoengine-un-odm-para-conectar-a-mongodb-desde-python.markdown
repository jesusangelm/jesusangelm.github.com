---
layout: post
title: !binary |-
  TW9uZ29FbmdpbmUgdW4gT0RNIHBhcmEgY29uZWN0YXIgYSBNb25nb0RCIGRl
  c2RlIFB5dGhvbg==
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
- !binary |-
  bW9uZ29lbmdpbmU=
- !binary |-
  b2Rt
- !binary |-
  cHltb25nbw==
---
{% include JB/setup %}

<a href="http://mongoengine.org/">MongoEngine</a> es un ODM (Object Document Mapper) que nos permite mapear la estructura de nuestra base de datos a objetos en nuestras aplicaciones <a href="http://blog.jam.net.ve/tag/python/">Python</a> que se conectan a instancias <a href="http://blog.jam.net.ve/tag/mongodb/">MongoDB</a>, esto con el fin de poder usar la informacion en nuestra base de datos somo si se tratasen de un objeto. Esto nos ofrece la ventaja de que podemos escribir de una manera mas comoda nuestra aplicacion, definir un esquema para la base de datos y mejorar nuestro codigo, entre otras ventajas mas.

Para instar MongoEngine en Linux tan solo debemos escribir en la terminal:

{% highlight bash %}
sudo easy_install mongoengine
{% endhighlight %}

**Nota:** debido a que MongoEngine usa el driver PyMongo para conectar nuestras aplicaciones Python a bases de datos NoSQL MongoDB, es capaz de detectar si tenemos o no instalado el driver PyMongo, por lo que si no lo tenemos instalado MongoEngine lo instalara automaticamente. De todos modos puedes instalar PyMongo de forma separada tecleando:

{% highlight bash %}
sudo easy_install pymongo
{% endhighlight %}

Si leyeron mi articulo anterior sobre <a href="http://blog.jam.net.ve/2011/01/12/ejemplo-de-consulta-mapreduce-en-mongodb/">Ejemplos de Consultas Map/Reduce en MongoDB</a> de seguro habran leido que al final del articulo mencionaba que en especifico esa consulta map/reduce podriamos mejorarla y hacerlas de una forma mas sencilla y sin funciones JavaScript si usaramos un ODM, pues bien MongoEngine es uno de los ODM con los que podemos mejorar el codigo de la aplicacion RegistroDeTransferencias.

Usando el ODM MongoEngine nuestra aplicacion quedaria similar a esto:

{% highlight python%}
#! /usr/bin/env python
from mongoengine import *
from datetime import *
from time import *

class Rsubida(Document):
 subida = FloatField()
 fecha_agregado = StringField()
 hora_agregado = StringField()

class Rbajada(Document):
 bajada = FloatField()
 fecha_agregado = StringField()
 hora_agregado = StringField()

print "Conectando a la Base de datos en la instancia Local"
#Conectando a la instancia MongoDB local en la base de datos "bdregistrotransgerenciamdb"
connect("bdregistrotransgerenciamdb")

la_subida = float(raw_input('Introdusca la cantidad de datos Enviados: '))
la_bajada = float(raw_input('Introdusca la cantidad de datos Recibidos: '))

fecha = date.today()
fechaagregado = fecha.strftime("%d-%m-%y")
horaagregado = strftime("%I:%M %p")

print "Los datos ingresados son:"
print "Subida: " + str(la_subida)
print "Bajada: " + str(la_bajada)
print "Fecha Agregado " + fechaagregado
print "Hora Agregado " + horaagregado

respuesta = raw_input("Estos datos son correctos? introdusca solo (s/n): ")

if respuesta == "s":
 regsubida = Rsubida(subida = la_subida, fecha_agregado = fechaagregado, hora_agregado = horaagregado)
 regbajada = Rbajada(bajada = la_bajada, fecha_agregado = fechaagregado, hora_agregado = horaagregado)

 regsubida.save()
 regbajada.save()
 print "Registros de Subida y Bajada ALMACENADOS con Exito!"

else:
 print "Cancelado!!!"

#Algunas consultas
respuesta = raw_input("Deseas ver algunas consultas? introdusca solo (s/n): ")

if respuesta == "s":
 #Mostrando todos los registros de bajada en la coleccion
 for rbajada in Rbajada.objects:
 print "Bajada: " + str(rbajada.bajada)

 #Sumatoria de todos los registros de bajada :)
 print "Total datos Bajada: " + str(Rbajada.objects.sum("bajada")) + " MB"
 print "Total datos Subida: " + str(Rsubida.objects.sum("subida")) + " MB"
 tbajada = Rbajada.objects.sum("bajada")
 tsubida = Rsubida.objects.sum("subida")
 total = tbajada + tsubida
 print "Total Consumido: " + str(total) + " MB"

else:
 print "Cancelado!"
{% endhighlight %}

Como podemos ver en las primeras lineas del codigo, creamos dos clases llamadas <strong>Rsubida</strong> y <strong>Rbajada</strong>, estas clases contienen lo que es la estructura y tipo de datos de lo que contendran nuestros documentos. De esta forma podemos establecer un esquema predeterminado para la informacion que se almacenara en nuestra base de datos. Cabe destacar tambien que por cada clase que se crea, MongoEngine generara una coleccion correspondiente en la base de datos, por lo que en en este ejemplo nuestra base de datos contendra dos colecciones <strong>rsubida</strong> que contendra los registros de subida y <strong>rbajada </strong>que contendra los registros de bajada.

**Consultas:** Aqui esta la parte que mas nos interesa, si nos fijamos en todo el codigo, no vemos por ningun lado las funciones JavaScript Map/Reduce, esto es porque simplemente no las necesitamos para realizar especificamente las consultas que ya teniamos:


{% highlight python %}
#Mostrando todos los registros de bajada en la coleccion
for rbajada in Rbajada.objects:
  print "Bajada: " + str(rbajada.bajada)
{% endhighlight %}

el ejemplo de salida de esta seccion del codigo seria algo como esto:

{% highlight bash %}
Bajada: 36.3
Bajada: 123.0
Bajada: 66.4
{% endhighlight %}

Esta seccion del codigo nos mostrara los registros de bajadas que estan contenido en el campo bajada, notese que en esta ocacion no nos devuelve un documento JSON con los datos solicitados (incluyendo su corchetes y comillas), sino que simplemente nos devuelve el valor en especifico.

La seccion del codigo con la que sustituimos las consultas map/reduce y su codigo en javascript es la siguiente:

{% highlight python %}
print "Total datos Bajada: " + str(Rbajada.objects.sum("bajada")) + " MB"
 print "Total datos Subida: " + str(Rsubida.objects.sum("subida")) + " MB"
{% endhighlight %}

lo que nos devolvera algo como:

{% highlight bash %}
Total datos Bajada: 225.7 MB
Total datos Subida: 142.3 MB
{% endhighlight %}

Coo vez aqui estamos aprovechando una de los beneficios de usar un ODM, y usar el contenido de nuestra base de datos como si de simples objetos se tratasen ya que con simplemente elegir la clase Rbajada y seleccionando su atributo (variable) "bajada" y haciendo uso del metodo sum() podremos realizar la sumatoria de todo los registros de bajada en en la coleccion Rbajada. Todo esto sin usar map/reduce ni funciones javascript :P

Con esto podemos completar la aplicacion y mostrar el total consumido, es decir, la suma de los datos de subida con los datos de bajada.

{% highlight python %}
tbajada = Rbajada.objects.sum("bajada")
tsubida = Rsubida.objects.sum("subida")
total = tbajada + tsubida
print "Total Consumido: " + str(total) + " MB"
{% endhighlight %}

los que nos muestra:

{% highlight bash %}
Total Consumido: 368.0 MB
{% endhighlight %}

Como vemos, un ODM nos puede facilitar mucho la vida y mejorar nuestras aplicaciones, ademas de acortar un poco el codigo ya que si se fijan. hay muchas menos lineas y mas funciones que la version anterior de la aplicacion que no usa MongoEngine.

Esta aplicacion planeo mejorarla cada vez mas mientras continue aprendiendo sobre Python y MongoDB por loq eu e puesto a disposicion su codigo en <a href="http://github.com/jesuangelm/RegistroDeTransferencias_Mdb_Meng">GitHub</a> para los que quieran descargarlo o solo si les parece util. :)

Saludos y espero les sirva!
