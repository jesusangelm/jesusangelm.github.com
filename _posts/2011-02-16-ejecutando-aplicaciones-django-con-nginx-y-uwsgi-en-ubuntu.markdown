---
layout: post
title: !binary |-
  RWplY3V0YW5kbyBBcGxpY2FjaW9uZXMgRGphbmdvIGNvbiBOZ2lueCB5IHVX
  U0dJIGVuIFVidW50dQ==
tags:
- !binary |-
  bGludXg=
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  dWJ1bnR1
- !binary |-
  bmdpbng=
- !binary |-
  d2Vi
- !binary |-
  cHl0aG9u
- !binary |-
  ZGphbmdv
- !binary |-
  dXdzZ2k=
- !binary |-
  ZnJhbWV3b3Jr
- !binary |-
  cHJvZ3JhbWFjaW9u
---
&nbsp;

&nbsp;

&nbsp;

Desde hace un par de meses e estado leyendo un poco sobre Python y  aprendiendo este popular lenguaje de programación, como ya tengo algo de  conocimiento en este lenguaje decidí probar creando una pagina web  sencilla usando el <a href="http://www.djangoproject.com/">Framework Django</a>.

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/02/django-logo-positive.redimensionado.png"><img class="aligncenter size-full wp-image-638" title="django-logo-positive.redimensionado" src="http://blog.jam.net.ve/imagenes/uploads/2011/02/django-logo-positive.redimensionado.png" alt="" width="300" height="105" /></a><a href="http://blog.jam.net.ve/imagenes/uploads/2011/01/Nginx-logo.png"><img class="aligncenter size-medium wp-image-583" title="Nginx-logo" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Nginx-logo-300x65.png" alt="" width="300" height="65" /></a><a href="http://blog.jam.net.ve/imagenes/uploads/2011/02/logo_uWSGI.png"><img class="aligncenter size-full wp-image-639" title="logo_uWSGI" src="http://blog.jam.net.ve/imagenes/uploads/2011/02/logo_uWSGI.png" alt="" width="236" height="73" /></a>

Cuando uno comienza a hacer una aplicación en Django normalmente usa  el servidor de pruebas que viene con el, mientras se esta desarrollando  la aplicación, este puede ser suficiente. pero…  ¿y si no queremos usar  el servidor de pruebas? o ¿si ya hemos terminado el desarrollo de la  aplicación y queremos implementarla en un servidor en internet?. Pues  bueno aquí podemos usar los servidores web mas comunes como Apache, <strong>Nginx</strong>, Lighttpd, etc.  En este articulo explicare y usare como podemos implementar aplicaciones Django usando el servidor web <a href="http://wiki.nginx.org/"><strong>Nginx</strong></a> y <a href="http://projects.unbit.it/uwsgi/"><strong>uWSGI</strong></a>.

Para realizar esto debemos utilizar <strong>Nginx</strong> 0.8.40 o superior ya que a partir de esa versión el modulo <strong>uWSGI</strong> viene incluido en el servidor web. Si tienes instalado alguna versión inferior a esta deberás desinstalarla.

<strong>Instalando <strong>Nginx</strong>:</strong>

Para este articulo use la ultima versión estable de <strong>Nginx</strong> la cual en este momento es la 0.8.54.

Primero que nada debemos de instalar (en caso de que no las tengas todavia) algunas dependencias para <strong>Nginx</strong>.
<pre lang="bash" line="1" escaped="true">sudo aptitude install  build-essential libpcre3 libpcre3-dev libssl-dev</pre>
luego, nos movemos a la carpeta <strong>/opt</strong>, nos descargamos los fuentes, descomprimimos, compilamos e instalamos <strong>Nginx</strong>.
<pre lang="bash" line="1" escaped="true">cd /opt
sudo wget http://sysoev.ru/nginx/nginx-0.8.54.tar.gz
sudo tar -zxvf nginx-0.8.54.tar.gz
cd nginx-0.8.54/
./configure --prefix=/opt/nginx --user=nginx --group=nginx --with-http_ssl_module
sudo make
sudo make install</pre>
Agregamos un usuario para <strong>Nginx</strong>:
<pre lang="bash" line="1" escaped="true">adduser --system --no-create-home --disabled-login --disabled-password --group nginx</pre>
<strong>Notese:</strong> que el directorio donde se encuentra instalado es <strong>/opt/<strong>nginx</strong></strong>

Ahora necesitamos un init script para poder iniciar y detener nuestro servidor <strong>Nginx</strong>, uno muy bueno que podemos descargar, instalar y usar es:
<pre lang="bash" line="1" escaped="true">sudo wget https://library.linode.com/web-servers/nginx/installation/reference/init-deb.sh
sudo mv init-deb.sh /etc/init.d/nginx
sudo chmod +x /etc/init.d/nginx
/usr/sbin/update-rc.d -f nginx defaults
/etc/init.d/nginx start</pre>
a partir de ahora podemos usar:
<pre lang="bash" line="1" escaped="true">sudo service nginx start</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">sudo service nginx stop</pre>
para iniciar y detener <strong>Nginx</strong>.

<strong>Instalando <strong>uWSGI</strong>:</strong>

Ahora debemos instalar <strong>uWSGI</strong>, este es mas sencillo y lo primero que debemos hacer es instalar algunas dependencias:
<pre lang="bash" line="1" escaped="true">sudo aptitude install build-essential psmisc python-dev libxml2 libxml2-dev python-setuptools</pre>
En estos momentos en la termina debemos estar ubicados en /opt (si no es asi simplemente <strong>cd /opt/</strong> )por lo que ahora debemos descargar, descomprimir e instalar <strong>uWSGI</strong>.
<pre lang="bash" line="1" escaped="true">sudo wget http://projects.unbit.it/downloads/uwsgi-0.9.6.8.tar.gz
sudo tar -zxvf uwsgi-0.9.6.5.tar.gz
sudo mv uwsgi-0.9.6.5/ uwsgi/
cd uwsgi/
sudo python setup.py install</pre>
Agregamos su usuario respectivo:
<pre lang="bash" line="1" escaped="true">sudo adduser --system --no-create-home --disabled-login --disabled-password --group uwsgi</pre>
Asignamos algunos permisos necesarios y creamos el archivo de logs:
<pre lang="bash" line="1" escaped="true">sudo chown -R uwsgi:uwsgi /opt/uwsgi
sudo touch /var/log/uwsgi.log
sudo chown uwsgi /var/log/uwsgi.log</pre>
Al igual que con <strong>Nginx</strong>, podemos usar un init script:
<pre lang="bash" line="1" escaped="true">sudo wget https://library.linode.com/web-servers/nginx/python-uwsgi/reference/init-deb.sh
sudo mv /opt/init-deb.sh /etc/init.d/uwsgi
sudo chmod +x /etc/init.d/uwsgi</pre>
<strong>Configurando <strong>Nginx</strong>:</strong>

Bien, con esto ya tenemos los componentes instalados, ahora nos toca configurar <a href="../tag/nginx/"><strong>Nginx</strong></a> para que pueda trabajar correctamente con <strong>uWSGI</strong> y ejecutar la aplicacion Django, que en mi caso esta aplicacion se llamara “<strong>prueba1</strong>” y esta ubicada en <strong>/home/usuario/django</strong> teniendo esto en cuenta, tan solo deberemos agregar el siguiente codigo dentro de el bloque <strong>http</strong> de tu archivo de configuracion de <strong>nginx</strong> (<strong><strong>nginx</strong>.conf</strong>):
<pre lang="bash" line="1" escaped="true"># Configiguracion para Django -  uWSGI
upstream prueba1 {
server unix:/tmp/uwsgi.sock;
}</pre>
Dentro de bloque <strong>server</strong> en la seccion <strong>location/</strong> debes colocar lo siguiente:
<pre lang="bash" line="1" escaped="true">#Config para DJANGO
 uwsgi_pass  prueba1;
 include uwsgi_params;</pre>
La configuración completa debe quedar similar a <a href="http://blog.jam.net.ve/guias/confignginx.txt">esto.</a>

por ultimo necesitamos crear dentro de la carpeta de nuestro proyecto Django (en este caso es <strong>prueba1</strong>), un archivo .wsgi que usaremos para especificar algunos parametros para <strong>uWSGI</strong>, el archivo lo llamo django.wsgi y su contenido es:
<pre lang="bash" line="1" escaped="true">#django.wsgi
import os
import sys

sys.path.append(os.path.abspath(os.path.dirname(__file__)))

os.environ["DJANGO_SETTINGS_MODULE"] = "prueba1.settings"

import django.core.handlers.wsgi
application = django.core.handlers.wsgi.WSGIHandler()</pre>
Por ultimo para ejecutar ahora nuestra aplicacion Django tan solo debemos ejecutar a <strong>uWSGI</strong> pasandole unos cuantos parametros, el comando es similar a esto:
<pre lang="bash" line="1" escaped="true">uwsgi -p 1 -C -A 4 -m -s /tmp/uwsgi.sock --wsgi-file /home/usuario/django/prueba1/django.wsgi --pythonpath /home/usuario/django --pidfile /tmp/uwsgi.pid</pre>
Donde:

* -s /tmp/<strong>uwsgi</strong>.sock     es donde queremos que <strong>uWSGI</strong> coloque el archivo .sock

* –wsgi-file /home/usuario/django/prueba1/django.wsgi    es donde hemos colocado el archivo .wsgi que creamos previamente.

* –pythonpath /home/usuario/django    es la ruta completa al directorio donde tenemos la carpeta de nuestro proyecto Django.

* –pidfile /tmp/<strong>uwsgi</strong>.pid    es donde queremos que <strong>uWSGI</strong> coloque el archivo .pid

Ahora por ultimo debemos ir a nuestro navegador y teclear en la barra  de direccion http://localhost t si todo a ido bien deberemos poder ver  nuestra pagina web hecha en Django ejecutandose con el servidor <a href="../tag/nginx/"><strong>Nginx</strong></a> via <strong>uWSGI</strong> <img src="../wp-includes/images/smilies/icon_biggrin.gif" alt=":D" />

Saludos y espero les sirva tanto como a mi.
