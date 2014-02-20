---
layout: post
title: "Implementando una aplicacion Rails 3 en Cloudfoundry"
tags: [rails, ruby, deploy, cloudfoundry]
---

<a href="http://cloudfoundry.com/">CloudFoundry</a> es la plataforma abierta como proyecto de servicios iniciada por VMware la cual puede soportar múltiples frameworks, varios servicios cloud de algunos proveedores , y múltiples aplicaciones de servicios. todo esto en una plataforma escalable en la nube.

<center><a href="http://imgur.com/NLWkg"><img src="http://i.imgur.com/NLWkg.png" title="Hosted by imgur.com" alt="" /></a></center>

Estos servicios están actualmente en version Beta, por lo que de momento son gratuitos pero se requiere de una invitación que puedes solicitar en la pagina de CloudFoundry. casualmente hoy me llego mi invitación (apenas la había pedido ayer) por lo me pude darle un vistazo rápido a la plataforma y hacer unas primeras pruebas.

<!-- more -->

**Instalación de VMC CLI y configuración:**

Lo primero en que me di cuenta es que el servicio se administra mediante una CLI (Command Line Interface) o interfaz de linea de comandos (si todavía no tienes ni P!##@ idea, lo administras desde la terminal!!! ). que se <strong>instala</strong> mediante una gema ruby llamada VMC (de VMware Cloud... creo!!!) por lo que tenemos que teclear en la terminal:

{% highlight bash %}
gem install vmc
{% endhighlight %}

luego de esto debemos ejecutar:

{% highlight bash %}
vmc target api.cloudfoundry.com
{% endhighlight %}

Ahora podemos iniciar sesion en el servicio tecleando:

{% highlight bash %}
vmc login
{% endhighlight %}

colocamos nuestro dirección de correos, la contraseña <strong>temporal</strong> que se nos envió con la invitación y tal cual dice la invitación, aprovechamos de cambiar la contraseña temporal por una fija tecleando:

{% highlight bash %}
vmc passwd
{% endhighlight %}

**Implementacion de una aplicación Rails 3:**

En mi caso yo use un sencillo blog con registro de usuarios usando la gema Devise. la aplicación no es gran cosa y usa Sqlite 3 como Base de datos.

para esto me muevo en la terminal y entrar a la carpeta donde esta la aplicación, una vez alli tecleo en la terminal:

{% highlight bash %}
vmc push
{% endhighlight %}

Esto nos hará una serie de preguntas:

- Would you like to deploy from the current directory?:

respondemos  <strong>Y</strong> - si

- Application Name: colocamos aqui el nombre de la apliacion

- Application Deployed URL: 'blogdevisejam.cloudfoundry.com'?

nos muestra la URL a la cual podremos acceder y ver nuestra aplicacion.

<strong>Nota:</strong> si no me equivoco las url son únicas, por lo que si ya existe una aplicación con la url que queremos usar, deberemos pensar en otra.

- Detected a Rails Application, is this correct? [Yn]:

nos descubrieron!!! pillaron que queremos subir una aplicacion rails, por lo que no le mentimos y contestamos <strong>Y.</strong>

- Memory Reservation [Default:256M] (64M, 128M, 256M, 512M or 1G)

respondemos 256M - podemos darle simplemente enter y tomara el valor por defecto el cual es 256M.

Deja de preguntarnos vainas y comienza a instalar y configurar la aplicacion:


<img class="aligncenter" title="Selección_065" src="http://blog.jam.net.ve/imagenes/uploads/2011/08/Selección_065-300x102.jpg" alt="" width="300" height="102" />


Y listo!!!

podemos ir a la url indicada en el "cuestionario" y ver nuestra aplicación en ejecución.

así de fácil :D

<a href="http://imgur.com/zm5RV"><img src="http://i.imgur.com/zm5RVs.jpg" title="Hosted by imgur.com" alt="" /></a>

Claro esta, esto es solo el principio, aplicaciones mas complejas requieren configuraciones y pasos mas complejos.

Cloudfoundry ademas de Rails (ruby) soporta aplicaciones Node.js (javascript del lado servidor), Spring (Java), Sinatra (Ruby) y Grails. se pueden usar bases de datos como MongoDB, Redis y MySQL.

a simple vista tiene buena pinta el servicio, uno mas a la lista de hosting "de momento gratuito" que podemos  usar para probar aplicaciones en Internet. habría que esperar a que salga de la etapa beta, ver que otras características se agregan y demás.
