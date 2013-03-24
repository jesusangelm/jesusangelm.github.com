---
layout: post
title: "Monitoreando nuestro sistema vigilando los archivos de registros logs."
tags: [linux, sysadmin, seguridad]
---
# Monitoreando nuestro sistema vigilando los archivos de registros logs.

{% include post_header.html %}

Los archivos de registros o archivos log como se conocen comummente, son archivos en donde se van almacenando un registro de todos los eventos que ocurren en un sistema durante un periodo de tiempo en particular. Estos archivos son usados tanto por el sistema operativo como por las aplicaciones o demonios (procesos) para registrar datos o informacion sobre un evento en particular.  En un sistema Linux podemos encontrar estos archivos de registro o logs en la carpeta /var/log  En esta carpeta encontraremos casi todos los archivos de registros de un sistema, pero cabe destacar que muchas aplicaciones crean estos archivos en sus propias carpetas fuera de /var/log.

Ahora bien, ¿En que nos sirve los logs para monitorear nuestro sistema? pues muy sencillo, los principales archivos logs que estan en la carpeta /var/log van almacenando informacion de casi todos los eventos que ocurren en tu PC practicamente desde que la enciendes y en ellos podremos ver por ejemplo que pasa internamente en Linux cuando conectas una Memoria USB, un <a href="http://blog.jam.net.ve/tag/modem/">Modem</a> USB o cuando estas conectado a internet puedes ver los intentos de entrada bloqueados por tu firewall.   En otras circunstancias podremos ser capaces de observar algun mensaje de error que se pueda producir cuando estas conectando algun hardware nuevo o si tienes un servicio web instalado podras ver quienes estan conectados a tu equipo.

Aqui en <a href="http://blog.jam.net.ve/">JamUnix Blog</a> veremos algunos archivos Logs y sus usos:

{% highlight bash %}
/var/log/messages
{% endhighlight %}

Este es el archivo principal de registros y almacena la mayoria de los mensajes de interes.


{% highlight bash %}
/var/log/auth.log
{% endhighlight %}

Muestra mensajes sobre autenticacion de usuarios y permisos


{% highlight bash %}
/var/log/daemon.log
{% endhighlight %}

Muestra mensajes sobre demonios (permisos) o servicios corriendo en el sistema.


{% highlight bash %}
/log/dmesg
{% endhighlight %}

Muestra mensajes del nucleo Linux.


{% highlight bash %}
/var/log/dpkg.log
{% endhighlight %}

Muestra un registro de los paquetes binarios instalado.


{% highlight bash %}
/var/log/kern.log
{% endhighlight %}

Muestra mensajes del Kernel


{% highlight bash %}
/var/log/boot.log
{% endhighlight %}

Muestra mensajes referentes al arranque del sistema.


{% highlight bash %}
/var/log/debug
{% endhighlight %}

Muestra mensajes de depuracion.


{% highlight bash %}
/var/log/lpr.log
{% endhighlight %}

Muestra mensajes sobre la impresora


{% highlight bash %}
/var/log/mail.err

/var/log/mail.info

/var/log/mail.warn

/var/log/mail.log
{% endhighlight %}

Archivos varios que muestran mensajes sobre error, informacion, alertas y registro (respectivamente) para los correos (requiere tener un servicio de correos funcionando).


{% highlight bash %}
/var/log/mysql.*
{% endhighlight %}

Archivos varios de registro para el servicio mysql (requiere tener un servicio mysql).


{% highlight bash %}
/var/log/user.log
{% endhighlight %}

Muestra informacion acerca de los procesos usados por el usuario


{% highlight bash %}
/var/log/Xorg.0.log
{% endhighlight %}

Muestra registros de Xorg


{% highlight bash %}
/var/log/apache2/*
{% endhighlight %}

Archivos de registro varios que muestra informacion sobre el servicio web Apache (requiere tener apache instalado).


{% highlight bash %}
/var/log/lighttpd/*
{% endhighlight %}

Archivos de registro varios que muestran informacion sobre el servicio web <a href="http://blog.jam.net.ve/tag/lighttpd/">Lighttpd</a> (requiere tener instalado Lighttpd)

...   Entre otros.

Por supuesto existen mucho mas archivos de logs, ya que muchos de los programas y aplicaciones que instales de seguro colocara su propio archivo de registro en /var/log o en su propia carpeta.  Por ejemplo, si instalamos el gestor de paquetes Aptitude, podremos ver un buen logs de los paquetes que instalamos con el en el archivos /var/log/aptitude

Estos archivos tambien pueden variar dependiendo de la distribucion <a href="http://blog.jam.net.ve/category/linux/">Linux</a> que se use.

Un tips importante es que podemos ver estos archivos desde la terminal usando comandos como tail, cat, less o grep. un ejemplo podria ser tecleando en la terminal:

{% highlight bash %}
tail -f  /var/log/message
{% endhighlight %}

Con esto podriamos dejar abierta la terminal y detectar en tiempo real cualquier nuevo registro en el archivo log

Saludos y espero les sirva.
