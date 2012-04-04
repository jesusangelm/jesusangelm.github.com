---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBXZWJtaW4gZW4gVlBTIGNvbiBDZW50T1MvRGViaWFu
tags:
- !binary |-
  ZGViaWFu
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  bGludXg=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  dWJ1bnR1
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  d2VibWlu
- !binary |-
  Y2VudG9z
- !binary |-
  cGFuZWw=
- !binary |-
  dnBz
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFy
- !binary |-
  b3BlcmE=
- !binary |-
  d2VibQ==
- !binary |-
  YmFzaA==
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
- !binary |-
  c2lzdGVtYXM=
---
{% include JB/setup %}

Hace unos cuantos meses me dio por  leer un poco, investigar y aprender como administrar servidores web tanto dedicados como VPS, para mis primeras pruebas instale Debian 5.03 en mi PC y le agrege todo lo necesario como para tener un servidor web en la plataforma LAMP ademas del servidor Open-SSH para poder conectarnos de forma remota y administrar por medio de SSH.

Una de las cosas que tambien quise agregarle al servidor y que me facilitaria algo la administracion del servidor es tener un panel de control, pero en este caso uno gratuito ya que por los momentos este servidor seria solo para pruebas, ademas no hay fuertes como para pagar licencias jejejeje.

El panel que elegi es <a href="http://webmin.com" target="_blank">Webmin</a> el cual es gratuito y tiene todo o casi todo lo necesario como para administrar el servidor.

Para instalarlo nos podemos descargar el paquete .deb de Webmin tecleando en la terminal:

{% highlight bash %}
$ wget -c http://prdownloads.sourceforge.net/webadmin/webmin_1.500_all.deb
{% endhighlight %}

Pero antes de instalarlo debemos cumplir e instalar algunas dependencias de webmin, para esto tecleamos en la terminal:

{% highlight bash %}
# apt-get install perl libnet-ssleay-perl openssl libauthen-pam-perl libpam-runtime libio-pty-perl libmd5-perl
{% endhighlight %}

una ves descargado e instalada las dependencias, lo instalamos webmin teclando en la terminal:

{% highlight bash %}
dpkg --install webmin_1.500_all.deb
{% endhighlight %}

Si todo nos a salido bien deberiamos terner instalado Webmin, para comprobarlo y accesar de una vez a nuestro panel de control abrimos el navegador y colocamos  en la barra de direcciones:

{% highlight bash session %}
http://localhost:10000
{% endhighlight %}

El puerto 10000 es en el que el servicio de webmin escucha para poder permitirnos entrar al panel, pero en ocaciones y luego de una instalacion no es posible accesar ya que el servicio de webmin no esta corriendo. para iniciarlo teclamos en la terminal:

{% highlight bash %}
 service webmin start
{% endhighlight %}

e ingresamos de nuevo http://localhost:10000 en el navegador.

y listo tenemos nuestro panel de control instalado y funcionando.

<a href="http://imgur.com/HCRI4"><img src="http://i.imgur.com/HCRI4l.png" title="Hosted by imgur.com" alt="" /></a>

Bien pero el post menciona tambien a CentOS, pues hace unas semanas pude tener acceso a un VPS para hacer pruebas, y una de las primeras cosas que hice fue instalar Webmin. Este VPS tiene como sistema operativo CentOS 5.4 y los pasos para instalar Webmin son basicamente los mismo.

En primer lugar nos descargamos el paquete .rpm de Webmin tecleando en la terminal:

{% highlight bash %}
$ wget -c http://prdownloads.sourceforge.net/webadmin/webmin-1.500-1.noarch.rpm
{% endhighlight %}

una ves descargado, lo instalamos tecleando en la terminal:

{% highlight bash %}
rpm -U webmin-1.500-1.noarch.rpm
{% endhighlight %}

Si todo nos a salido bien deberiamos terner instalado Webmin, para comprobarlo y accesar de una vez a nuestro panel de control abrimos el navegador y colocamos  en la barra de direcciones:

{% highlight bash %}
http://localhost:10000
{% endhighlight %}

en caso de que el servicio no tampoco este corriendo podemos hacer igual que con debian y teclear el comando para iniciar el servicio de Webmin.

Otro inconveniente que puede suceder es que algunos de los modulos de Firewall que estes corriendo en Linux, te este bloqueando el puerto de escucha de webmin, para añadir una exepcion y permitirnos accesar al panel de control de webmin desde el navegador debemos editar el archivo correspondiente a nuestra distribucion.

- Para sistemas <strong>RedHat</strong> y derivados como por ejemplo <strong>Fedora</strong> o <strong>CentOS</strong> editamos el archivo <strong>iptables</strong> ubicado en <strong>/etc/sysconfig/iptables</strong>

Para editarlo tecleamos en la terminal:

{% highlight bash %}
nano /etc/sysconfig/iptables
{% endhighlight %}

y agregamos esta linea :

{% highlight bash %}
-A INPUT -p tcp -m tcp --dport 10000 -j ACCEPT
{% endhighlight %}

- Para sistemas <strong>Debian</strong> y derivados como<strong> Ubuntu</strong> editamos el mismo archivo <strong>iptables</strong> pero en este caso lo ubicaremos en <strong>/var/lib/iptables</strong>

Para editarlo tecleamos en la terminal:

{% highlight bash %}
nano /var/lib/iptables
{% endhighlight %}

y agregamos la linea:

{% highlight bash %}
-A INPUT -p tcp -m tcp --dport 10000 -j ACCEPT
{% endhighlight %}

ahora reiniciamos iptables tecleando:

{% highlight bash %}
sudo /etc/init.d/iptables
{% endhighlight %}

Listo espero que le sirvan tanto como a mi.

Links de interes:

- <a href="http://webmin.com/download.html" target="_blank">Descarga de Webmin</a>

- <a href="http://webmin.com/deb.html" target="_blank">Instalacion desde paquete .Deb</a>

- <a href="http://webmin.com/rpm.html" target="_blank">Instalacion desde paquete .Rpm</a>

- <a href="http://webmin.com/firewall.html" target="_blank">Añadiendo exepcion al firewall</a>
