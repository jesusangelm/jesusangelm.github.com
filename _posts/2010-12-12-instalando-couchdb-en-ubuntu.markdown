---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBDb3VjaERCIGVuIFVidW50dQ==
tags:
- !binary |-
  amFtdW5peA==
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  YmFzaA==
- !binary |-
  bm9zcWw=
- !binary |-
  Y291Y2hkYg==
---
{% include JB/setup %}

Desde hace un mes aproximadamente e estado leyendo sobre sistemas de bases de datos del tipo <a href="http://es.wikipedia.org/wiki/NoSQL">NoSQL</a>, estos sistemas de bases de datos se estan poniendo de moda entre las grandes compañias que requieren alta escalabilidad y performance a bajo costo. Los sistemas de bases de datos NoSQL no son para nada similares a los sistemas de bases de datos Relacionales a los que estamos acostumbrado, en los Sistemas de Administracion de Bases de Datos Relacionales (RDBMS) se acostumbra a organizar los datos en forma de tablas las cuales contienen filas, columnas y un campo clave o ID por lo general autoincremental, ademas de que se usan esquemas de relaciones entre otras tablas.

<a href="http://imgur.com/EUNoH"><img src="http://i.imgur.com/EUNoH.jpg" title="Hosted by imgur.com" alt="" /></a>

Bien en los Sistemas NoSQL casi nada de esto existe, CouchDB es un sistema de bases de datos NoSQL que almacena la informacion en forma de documentos, estos documentos reflejan los datos en formato <a href="http://www.json.org/json-es.html">JSON</a>, es decir organiza la los datos en Clave:Valor y no en tablas. Estos documentos JSON contienen una ID unica No-Incremental que puede ser autogenerada o que puede definir uno mismo.

Una de las ventajas de <a href="http://couchdb.apache.org/">CouchDB</a> frente a otros sistemas NoSQL del tipo documento es que incluye una interfaz web (FUTON) de facil manejo desde la que podemos administrar nuestras bases de datos, CouchDB ademas soporta accesibilidad por REST/HTTP por lo que podemos administrar nuestra base de datos mediante una URL. Otra de las ventajas de couchDB es el soporte de replicaciones del tipo Mestro-Esclavo, Maestro-Maestro y Replicacion incremental con deteccion/resolucion de conflictos bidireccional.

Un documento sencillo en CouchDB podria ser algo como esto:

{% highlight bash %}
"_id" : "ksjfhk65464f65g464f68465cx4665",
"_rev" : "1-6d4f654d5fv5fz3214fd45d45",
"Nombre" : "Angel",
"Nick" : "JamUnix",
"Web" : "www.jam.net.ve",
"Lenguajes_conocidos" : ["Vb.Net", "HTML5", "CSS3", "otros mas..."]
{% endhighlight %}

Para instalar CouchDB en Ubuntu y comenzar a "jugar" con el y aprender como funciona una base de datos NoSQL tan solo teclea en la terminal:

{% highlight bash %}
sudo aptitude install couchdb
{% endhighlight %}

Con esto tendremos CouchDB instalado y ejecutandoce en nuestra PC, para comprobarlo podemos ir a la terminal y mediante Curl teclear:

{% highlight bash %}
curl http://localhost:5984
{% endhighlight %}

lo que nos devolvera algo como:

{% highlight bash %}
{"couchdb":"Welcome","version":"1.0.1"}
{% endhighlight %}

CouchDB ofrece una interfaz web llamada Futon en la que podemos administrar las bases de datos, para entrar en Futon tan solo debemos abrir nuestro navegador y colocar la siguiente URL:

{% highlight bash %}
http://localhost:5984/_utils
{% endhighlight %}

Con lo que veras algo como esto:

<a href="http://imgur.com/vbyGB"><img src="http://i.imgur.com/vbyGBs.jpg" title="Hosted by imgur.com" alt="" /></a>

Por ahora no hay mucha documentacion en Español sobre CouchDB, pero si te interesa aprender mas sobre este sistema puedes leer este <a href="http://4tic.com/blog/40-blgo/63-couchdb-una-bd-diferente">primer</a> y <a href="http://4tic.com/en/blog/40-blgo/64-couchdb-una-base-de-datos-diferente-2">segundo</a> articulo publicado en 4tic.com

Tambien puedes visitar la <a href="http://wiki.apache.org/couchdb/">Wiki de CouchDB</a> o leer <a href="http://guide.couchdb.org/">la Guia</a> en Ingles.

Pronto publicare mas articulos acerca de como crear documentos sencillos usando Futon, los usos con curl y un ejemplo de como conectar y almacenar datos usando Python y el Framework <a href="http://couchdbkit.org/">CouchDBKit.</a>
