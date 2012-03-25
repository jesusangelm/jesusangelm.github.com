---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBMaWdodHRwZCBlbiBDZW50b3MgNS40IC0gT3RybyBsaWdl
  cm8gc2VydmljaW8gd2ViIGEgdGVuZXIgZW4gY3VlbnRh
tags:
- !binary |-
  bGludXg=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  Y2VudG9z
- !binary |-
  bmdpbng=
- !binary |-
  dnBz
- !binary |-
  cGhw
- !binary |-
  cGhwbXlhZG1pbg==
- !binary |-
  bGlnaHR0cGQ=
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFy
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  d2Vi
- !binary |-
  cmVsZWFzZQ==
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
---
Como algunos de mis 0.000 lectores ya saben hace ya casi un mes me donaron un servidor dedicado el cual eh estado usando para aprender y estudiar la administracion de servidores y VPS.  Bien, debido a los bajos recursos que tiene este servidor muchos me han recomendado usar servicios web ligeros que consuman pocos procesos y memoria ram. Pues bien como el unico que conocia hasta entonces es <a href="http://blog.jam.net.ve/2010/02/16/instalando-nginx-en-centos/" target="_blank">Nginx</a> del cual ya les e hablado y e publicado una explicacion de como instalarlo, fue el primero que instale y configure en el servidor dedicado.

Pero luego de unos dias de configuracion me tope con un inconveniente, Nginx no me dejaba accesar a phpMyAdmin usando un alias y entrando en la direccion http://miservidor.net.ve/phpmyadmin/.  Despues de casi un mes de busqueda e intento de posibles soluciones, el alias con Nginx nunca me quiso trabajar por lo que tube que dejar Nginx a un lado e intentar con otro servicio web.

Lighttpd es un servicio web de bajos recursos y muy ligero que me recomendaron varias veces, asi que me decidi a instalarlo y probarlo a  ver que tal tabaja y si hacia lo que queria.

Bien para instalarlo segui tan solo estos pasos:

- Primero que nada y al igual a como lo hice en <a href="http://blog.jam.net.ve/2010/02/16/instalando-nginx-en-centos/" target="_blank">mi publicacion de Nginx</a>, debemos agregar los repositorios EPEL tecleando en la terminal y dependiendo de la arquitectura de tu S.O

* Para Centos 64bit

[bash]sudo rpm  -Uvh http://download.fedora.redhat.com/pub/epel/5Server/x86_64/epel-release-5-3.noarch.rpm [/bash]

* Para Centos 32bit

[bash]sudo rpm -Uvh http://download.fedora.redhat.com/pub/epel/5Server/i386/epel-release-5-3.noarch.rpm [/bash]

- Luego de esto ya podemos continuar e instalar Lighttpd tecleando en la terminal:

[bash] yum install lighttpd [/bash]

Luego de esto ya tendremos instalado Lighttpd.

- Ahora podemos iniciar el servicio tecleando en la terminal:

[bash] service lighttpd start [/bash]

Si nos vamos a el navegador y entramos la ip o dominio de nuestro servidor, podremos ver la pagina predeterminada que coloca Lighttpd. curiosamente la pagina predeterminada te mostrara un error 404 - Not Found, esto se debe a que el directorio raiz de Lighttpd esta vacio y no hay ningun archivo index.html en ella.

Para cambiar esto tan solo debemos agregar alguna pagina html en el directorio raiz el cual es:

[bash] /srv/www/lighttpd [/bash]

Bien para poder tener soporte PHP y poder montar paginas escritas en este lenguaje debemos instalar fastcgi y hacer algunas configuraciones extras.

- Instalamos los paquetes lighttpd-fastcgi y php-cli

[bash] yum install lighttpd-fastcgi php-cli [/bash]

luego de esto configuramos lighttpd para que soporte php, abrimos el archivo /etc/php.ini tecleando en la terminal:

[bash] nano /etc/php.ini [/bash]

y agregamos al final del archivo esta linea:

[bash] cgi.fix_pathinfo = 1 [/bash]

luego de esto abrimos /etc/lighttpd/lighttpd.conf tecleando en la terminal:

[bash] nano /etc/lighttpd/lighttpd.conf [/bash]

y descomentamos la linea que dice mod_fastcgi y mod_alias (quitamos el # ) de modo que quede similar a esta:

[bash]
server.modules              = (
#                               &quot;mod_rewrite&quot;,
#                               &quot;mod_redirect&quot;,
                                &quot;mod_alias&quot;,
                                &quot;mod_access&quot;,
#                               &quot;mod_cml&quot;,
#                               &quot;mod_trigger_b4_dl&quot;,
#                               &quot;mod_auth&quot;,
#                               &quot;mod_status&quot;,
#                               &quot;mod_setenv&quot;,
                                &quot;mod_fastcgi&quot;,
#                               &quot;mod_proxy&quot;,
#                               &quot;mod_simple_vhost&quot;,
#                               &quot;mod_evhost&quot;,
#                               &quot;mod_userdir&quot;,
#                               &quot;mod_cgi&quot;,
#                               &quot;mod_compress&quot;,
#                               &quot;mod_ssi&quot;,
#                               &quot;mod_usertrack&quot;,
#                               &quot;mod_expire&quot;,
#                               &quot;mod_secdownload&quot;,
#                               &quot;mod_rrdtool&quot;,
                                &quot;mod_accesslog&quot; )
[/bash]

Mas abajo buscamos fastcgi.server y descomentamos de modo que quede similar a esto:

[bash]
#### fastcgi module
## read fastcgi.txt for more info
## for PHP don't forget to set cgi.fix_pathinfo = 1 in the php.ini
fastcgi.server             = ( &quot;.php&quot; =&gt;
                               ( &quot;localhost&quot; =&gt;
                                 (
                                   &quot;socket&quot; =&gt; &quot;/tmp/php-fastcgi.socket&quot;,
                                   &quot;bin-path&quot; =&gt; &quot;/usr/bin/php-cgi&quot;
                                 )
                               )
                            )
[/bash]

Guardamos los cambios y salimos del editor.

Nota: si en esta seccion de tu lighttpd.conf en la propiedad "socket" aparece alguna otra ruta distinta a /tmp/php-fastcgi.socket cambialo y dejalo igual a como aparece arriba.

Luego de esto debes reiniciar Lighttpd para que se apliquen los cambios tecleando:

[bash] service lighttpd restart [/bash]

con esto ya tendremos Lighttpd funcionando y ejecutando script php mediante fastcgi, podemos comprobar el funcionamiento colocando en el directorio raiz cualquier archivo .php y accesando a el por medio de la ip o dominio del servidor.

Pero bueno como les comentaba mas arriba lo que me hizo cambiar de Nginx a Lighttpd es probar y configurar un alias que me permitiera accesar al phpmyadmin, esto lo hice de la siguiente manera:

abrimos una vez mas el archivo lighttpd.conf tecleando en la terminal:

[bash] nano /etc/lighttpd/lighttpd.conf [/bash]

y agregamos en cualquier parte del archivo la siguiente linea:

[bash] alias.url =(&quot;/phpmyadmin/&quot; =&gt;  &quot;/tu/ruta/al/phpmyadmin/&quot;) [/bash]

Nota: cambiar "/tu/ruta/al/phpmyadmin/" por la direccion donde tienes instalado phpmyadmin, por ejemplo en mi servidor esta en "/usr/share/phpmyadmin"

guardamos los cambios y reiniciamos de nuevo el servicio Lighttpd.

una vez realizado el cambio podemos comprobar que funciona ingresando en el navegador http://tuservidor.net.ve/phpmyadmin

si todo a ido bien, ya deberias poder entrar a phpMyAdmin.

Saludos y espero les sirva tanto como a mi.
