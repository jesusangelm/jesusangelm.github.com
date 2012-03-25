---
layout: post
title: !binary |-
  TW9uaXRvcmVhbmRvIG51ZXN0cm8gc2lzdGVtYSB2aWdpbGFuZG8gbG9zIGFy
  Y2hpdm9zIGRlIHJlZ2lzdHJvICAoTG9ncyk=
tags:
- !binary |-
  YmxvZw==
- !binary |-
  Y29ycmVv
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  amFtdW5peA==
- !binary |-
  bGludXg=
- !binary |-
  bW9kZW0=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  dW5peA==
- !binary |-
  dXNi
- !binary |-
  bW9uaXRvcg==
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  bXlzcWw=
- !binary |-
  bGlnaHR0cGQ=
- !binary |-
  bWF5bw==
- !binary |-
  b3BlcmE=
- !binary |-
  YmFzaA==
- !binary |-
  d2Vi
- !binary |-
  Y29tYW5kb3M=
- !binary |-
  dGVybWluYWw=
- !binary |-
  bW9uaXRvcmVhcg==
- !binary |-
  bG9ncw==
- !binary |-
  cmVnaXN0cm9z
- !binary |-
  YXJjaGl2b3M=
- !binary |-
  c2lzdGVtYXM=
- !binary |-
  eG9yZw==
---
Los archivos de registros o archivos log como se conocen comummente, son archivos en donde se van almacenando un registro de todos los eventos que ocurren en un sistema durante un periodo de tiempo en particular. Estos archivos son usados tanto por el sistema operativo como por las aplicaciones o demonios (procesos) para registrar datos o informacion sobre un evento en particular.  En un sistema Linux podemos encontrar estos archivos de registro o logs en la carpeta /var/log  En esta carpeta encontraremos casi todos los archivos de registros de un sistema, pero cabe destacar que muchas aplicaciones crean estos archivos en sus propias carpetas fuera de /var/log.

Ahora bien, ¿En que nos sirve los logs para monitorear nuestro sistema? pues muy sencillo, los principales archivos logs que estan en la carpeta /var/log van almacenando informacion de casi todos los eventos que ocurren en tu PC practicamente desde que la enciendes y en ellos podremos ver por ejemplo que pasa internamente en Linux cuando conectas una Memoria USB, un <a href="http://blog.jam.net.ve/tag/modem/">Modem</a> USB o cuando estas conectado a internet puedes ver los intentos de entrada bloqueados por tu firewall.   En otras circunstancias podremos ser capaces de observar algun mensaje de error que se pueda producir cuando estas conectando algun hardware nuevo o si tienes un servicio web instalado podras ver quienes estan conectados a tu equipo.

Aqui en <a href="http://blog.jam.net.ve/">JamUnix Blog</a> veremos algunos archivos Logs y sus usos:
<pre lang="bash" line="1" escaped="true">/var/log/messages</pre>
Este es el archivo principal de registros y almacena la mayoria de los mensajes de interes.
<pre lang="bash" line="1" escaped="true">/var/log/auth.log</pre>
Muestra mensajes sobre autenticacion de usuarios y permisos
<pre lang="bash" line="1" escaped="true">/var/log/daemon.log</pre>
Muestra mensajes sobre demonios (permisos) o servicios corriendo en el sistema.
<pre lang="bash" line="1" escaped="true">/var/log/dmesg</pre>
Muestra mensajes del nucleo Linux.
<pre lang="bash" line="1" escaped="true">/var/log/dpkg.log</pre>
Muestra un registro de los paquetes binarios instalado.
<pre lang="bash" line="1" escaped="true">/var/log/kern.log</pre>
Muestra mensajes del Kernel
<pre lang="bash" line="1" escaped="true">/var/log/boot.log</pre>
Muestra mensajes referentes al arranque del sistema.
<pre lang="bash" line="1" escaped="true">/var/log/debug</pre>
Muestra mensajes de depuracion.
<pre lang="bash" line="1" escaped="true">/var/log/lpr.log</pre>
Muestra mensajes sobre la impresora
<pre lang="bash" line="1" escaped="true">/var/log/mail.err

/var/log/mail.info

/var/log/mail.warn

/var/log/mail.log</pre>
Archivos varios que muestran mensajes sobre error, informacion, alertas y registro (respectivamente) para los correos (requiere tener un servicio de correos funcionando).
<pre lang="bash" line="1" escaped="true">/var/log/mysql.*</pre>
Archivos varios de registro para el servicio mysql (requiere tener un servicio mysql).
<pre lang="bash" line="1" escaped="true">/var/log/user.log</pre>
Muestra informacion acerca de los procesos usados por el usuario
<pre lang="bash" line="1" escaped="true">/var/log/Xorg.0.log</pre>
Muestra registros de Xorg
<pre lang="bash" line="1" escaped="true">/var/log/apache2/*</pre>
Archivos de registro varios que muestra informacion sobre el servicio web Apache (requiere tener apache instalado).
<pre lang="bash" line="1" escaped="true">/var/log/lighttpd/*</pre>
Archivos de registro varios que muestran informacion sobre el servicio web <a href="http://blog.jam.net.ve/tag/lighttpd/">Lighttpd</a> (requiere tener instalado Lighttpd)

...   Entre otros.

Por supuesto existen mucho mas archivos de logs, ya que muchos de los programas y aplicaciones que instales de seguro colocara su propio archivo de registro en /var/log o en su propia carpeta.  Por ejemplo, si instalamos el gestor de paquetes Aptitude, podremos ver un buen logs de los paquetes que instalamos con el en el archivos /var/log/aptitude

Estos archivos tambien pueden variar dependiendo de la distribucion <a href="http://blog.jam.net.ve/category/linux/">Linux</a> que se use.

Un tips importante es que podemos ver estos archivos desde la terminal usando comandos como tail, cat, less o grep. un ejemplo podria ser tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">tail -f  /var/log/message</pre>
Con esto podriamos dejar abierta la terminal y detectar en tiempo real cualquier nuevo registro en el archivo log

Saludos y espero les sirva.
