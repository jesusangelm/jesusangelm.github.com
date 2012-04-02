---
layout: post
title: Vuela en internet usando una cache DNS - Dnsmasq en Ubuntu
category: Ubuntu
tags: [dnsmasq, internet, opendns, tutorial, mejora, ubuntu, archlinux, linux, cache, dns]
---
{% include JB/setup %}

Desde hace unos meses para aca mi internet HSDPA ha estado presentando molestos inconveniente los cuales me obligan a 
recargar o solicitar las paginas mas de una vez para que estas puedan presentarse completamente y sin errores por lo que
decidi usar una cache DNS con Dnsmasq para probar como puede esto ayudar a mi conexion y que las paginas cargen a la primera 
solicitud y sin problemas.

[Dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) es un servidor DHCP y  DNS ligero y de bajo impacto 
para el sistema que nos permite usarlo cachear las peticiones DNS  hacia internet que realiza nuestro computador 
pra resolver la IP de un dominio, de manera que cuando se desee accesar de nuevo a un dominio ya resuelto, no se 
tenga que volver a solicitar a los servidores DNS en internet sino que se resuelven en la misma PC ya que esta 
conoce de antemano la ip correspondiente.

Antes de instalar Dnsmasq vemos los tiempos aproximados que se tarda mi conexion en resolver la ip de un dominio:

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-23.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-23-300x134.png" width="300" height="134" /></a>

Para instalar Dnsmasq tan solo debemos ejecutar en la terminal la siguiente orden, pero antes asegurese de tener 
activado los repositorios "universe"

{% highlight bash %}
sudo apt-get install dnsmasq
{% endhighlight %}

Luego de esto pasamos a configurar dnsmasq editando el archivo dnsmasq.conf tecleando en la terminal:

{% highlight bash %}
sudo gedit /etc/dnsmasq.conf
{% endhighlight %}

descomentamos y modificamos la linea que contiene:

{% highlight bash %}
#listen-address=
{% endhighlight %}

para que quede de esta manera:

{% highlight bash %}
listen-address=127.0.0.1
{% endhighlight %}

Luego de esto nos toca editar el cliente DHCP tecleando en la terminal:

{% highlight bash %}
sudo gedit /etc/dhcp3/dhclient.conf
{% endhighlight %}

y nos aseguramos que las siguientes lineas:

{% highlight bash %}
prepend domain-name-servers 127.0.0.1;
request subnet-mask, broadcast-address, time-offset, routers,
domain-name, domain-name-servers, domain-search, host-name,
netbios-name-servers, netbios-scope, interface-mtu,
rfc3442-classless-static-routes, ntp-servers;
{% endhighlight %}

esten descomentada y tenga la IP  127.0.0.1

Por ultimo nos toca editar el archivo resolv.conf  y agregar la ip de nuestro servidor cache dns local tecleando en la terminal:

{% highlight bash %}
sudo vim /etc/resolv.conf
{% endhighlight %}

y colocamos nuestra IP local de primero en la lista de modo que quede similar a esto:

{% highlight bash %}
nameserver 127.0.0.1
nameserver 208.67.222.222
nameserver 208.67.220.220
{% endhighlight %}

por ultimo reiniciamos dnsmasq para que aplique la configuracion:

{% highlight bash %}
sudo /etc/init.d/dnsmasq restart
{% endhighlight %}

Por ultimo consultamos 2 veces el mismo dominio para ver el tiempo que se toma ahora ¿porque dos veces? la primera 
para que haga la consulta a internet y permitir que dnsmasq la almacene en cache y la segunda para que se realice 
la consulta de manera local ya que dnsmasq conoce ya la ip resultante y no se necesita hacer consultas al exterior.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-24.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-24-300x128.png" width="300" height="128" /></a>

como ven ahora es mucho mas rapido si se realizan consultas locales a dominios ya resueltos con anterioridad.

Saludos y espero le sirva.
