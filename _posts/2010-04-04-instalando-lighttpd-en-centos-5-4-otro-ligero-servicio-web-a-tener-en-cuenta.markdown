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
{% include JB/setup %}

Como algunos de mis 0.000 lectores ya saben hace ya casi un mes me donaron un servidor dedicado el cual eh estado usando para aprender y estudiar la administracion de servidores y VPS.  Bien, debido a los bajos recursos que tiene este servidor muchos me han recomendado usar servicios web ligeros que consuman pocos procesos y memoria ram. Pues bien como el unico que conocia hasta entonces es <a href="http://blog.jam.net.ve/2010/02/16/instalando-nginx-en-centos/" target="_blank">Nginx</a> del cual ya les e hablado y e publicado una explicacion de como instalarlo, fue el primero que instale y configure en el servidor dedicado.

Pero luego de unos dias de configuracion me tope con un inconveniente, Nginx no me dejaba accesar a phpMyAdmin usando un alias y entrando en la direccion http://miservidor.net.ve/phpmyadmin/.  Despues de casi un mes de busqueda e intento de posibles soluciones, el alias con Nginx nunca me quiso trabajar por lo que tube que dejar Nginx a un lado e intentar con otro servicio web.

Lighttpd es un servicio web de bajos recursos y muy ligero que me recomendaron varias veces, asi que me decidi a instalarlo y probarlo a  ver que tal tabaja y si hacia lo que queria.

Bien para instalarlo segui tan solo estos pasos:

- Primero que nada y al igual a como lo hice en <a href="http://blog.jam.net.ve/2010/02/16/instalando-nginx-en-centos/" target="_blank">mi publicacion de Nginx</a>, debemos agregar los repositorios EPEL tecleando en la terminal y dependiendo de la arquitectura de tu S.O

* Para Centos 64bit

{% highlight bash %}
sudo rpm  -Uvh http://download.fedora.redhat.com/pub/epel/5Server/x86_64/epel-release-5-3.noarch.rpm
{% endhighlight %}

* Para Centos 32bit

{% highlight bash %}
sudo rpm -Uvh http://download.fedora.redhat.com/pub/epel/5Server/i386/epel-release-5-3.noarch.rpm
{% endhighlight %}

- Luego de esto ya podemos continuar e instalar Lighttpd tecleando en la terminal:

{% highlight bash %}
yum install lighttpd
{% endhighlight %}

Luego de esto ya tendremos instalado Lighttpd.

- Ahora podemos iniciar el servicio tecleando en la terminal:

{% highlight bash %}
service lighttpd start
{% endhighlight %}

Si nos vamos a el navegador y entramos la ip o dominio de nuestro servidor, podremos ver la pagina predeterminada que coloca Lighttpd. curiosamente la pagina predeterminada te mostrara un error 404 - Not Found, esto se debe a que el directorio raiz de Lighttpd esta vacio y no hay ningun archivo index.html en ella.

Para cambiar esto tan solo debemos agregar alguna pagina html en el directorio raiz el cual es:

{% highlight bash %}
/srv/www/lighttpd
{% endhighlight %}

Bien para poder tener soporte PHP y poder montar paginas escritas en este lenguaje debemos instalar fastcgi y hacer algunas configuraciones extras.

- Instalamos los paquetes lighttpd-fastcgi y php-cli

{% highlight bash %}
yum install lighttpd-fastcgi php-cli
{% endhighlight %}

luego de esto configuramos lighttpd para que soporte php, abrimos el archivo /etc/php.ini tecleando en la terminal:

{% highlight bash %}
vim /etc/php.ini
{% endhighlight %}

y agregamos al final del archivo esta linea:

{% highlight bash %}
cgi.fix_pathinfo = 1
{% endhighlight %}

luego de esto abrimos /etc/lighttpd/lighttpd.conf tecleando en la terminal:

{% highlight bash %}
vim /etc/lighttpd/lighttpd.conf
{% endhighlight %}

y descomentamos la linea que dice mod_fastcgi y mod_alias (quitamos el # ) de modo que quede similar a esta:

{% highlight bash %}
server.modules              = (
#                               "mod_rewrite",
#                               "mod_redirect",
                                "mod_alias",
                                "mod_access",
#                               "mod_cml",
#                               "mod_trigger_b4_dl",
#                               "mod_auth",
#                               "mod_status",
#                               "mod_setenv",
                                "mod_fastcgi",
#                               "mod_proxy",
#                               "mod_simple_vhost",
#                               "mod_evhost",
#                               "mod_userdir",
#                               "mod_cgi",
#                               "mod_compress",
#                               "mod_ssi",
#                               "mod_usertrack",
#                               "mod_expire",
#                               "mod_secdownload",
#                               "mod_rrdtool",
                                "mod_accesslog" )
{% endhighlight %}

Mas abajo buscamos fastcgi.server y descomentamos de modo que quede similar a esto:

{% highlight bash %}
#### fastcgi module
## read fastcgi.txt for more info
## for PHP don't forget to set cgi.fix_pathinfo = 1 in the php.ini
fastcgi.server             = ( ".php" =>
                               ( "localhost" =>
                                 (
                                   "socket" => "/tmp/php-fastcgi.socket",
                                   "bin-path" => "/usr/bin/php-cgi"
                                 )
                               )
                            )
{% endhighlight %}

Guardamos los cambios y salimos del editor.

Nota: si en esta seccion de tu lighttpd.conf en la propiedad "socket" aparece alguna otra ruta distinta a /tmp/php-fastcgi.socket cambialo y dejalo igual a como aparece arriba.

Luego de esto debes reiniciar Lighttpd para que se apliquen los cambios tecleando:

{% highlight bash %}
service lighttpd restart
{% endhighlight %}

con esto ya tendremos Lighttpd funcionando y ejecutando script php mediante fastcgi, podemos comprobar el funcionamiento colocando en el directorio raiz cualquier archivo .php y accesando a el por medio de la ip o dominio del servidor.

Pero bueno como les comentaba mas arriba lo que me hizo cambiar de Nginx a Lighttpd es probar y configurar un alias que me permitiera accesar al phpmyadmin, esto lo hice de la siguiente manera:

abrimos una vez mas el archivo lighttpd.conf tecleando en la terminal:

{% highlight bash %}
vim /etc/lighttpd/lighttpd.conf
{% endhighlight %}

y agregamos en cualquier parte del archivo la siguiente linea:

{% highlight bash %}
alias.url =("/phpmyadmin/" =>  "/tu/ruta/al/phpmyadmin/")
{% endhighlight %}

Nota: cambiar "/tu/ruta/al/phpmyadmin/" por la direccion donde tienes instalado phpmyadmin, por ejemplo en mi servidor esta en "/usr/share/phpmyadmin"

guardamos los cambios y reiniciamos de nuevo el servicio Lighttpd.

una vez realizado el cambio podemos comprobar que funciona ingresando en el navegador http://tuservidor.net.ve/phpmyadmin

si todo a ido bien, ya deberias poder entrar a phpMyAdmin.

Saludos y espero les sirva tanto como a mi.
