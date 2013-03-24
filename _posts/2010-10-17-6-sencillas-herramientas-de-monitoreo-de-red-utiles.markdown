---
layout: post
title: "6 sencillas herramientas para monitoreo de red utiles."
tags: [linux, red, sysadmin, seguridad]
---
# 6 sencillas herramientas para monitoreo de red utiles.

{% include post_header.html %}

Desde hace unos meses para aca e estado leyendo un poco de las grandes posibilidades que ofrece la terminal y su gran poder para controlar y administar practicamente toda tu PC.  Ultimamente e estado viendo aplicaciones y comandos para la terminal que me permitan ver y monitoriar las conexiones a internet por lo que les traigo aqui 3 comandos y 3 aplicaciones de terminal utiles para monitoriar tu red.

**Aplicaciones:**

- Iptraf:  Es una aplicacion basada en la terminal de estadisticas de red. tiene como caracteristicas el conteo de bytes y monitoreo de conexiones de paquetes TCP. Tambien ofrece estadisticas de las interfaces de red (eth0, ppp0, wlan0, etc) e indicadores de actividad, tambien nos muestra las interrupciones de trafico TCP/UDP.

<a href="http://imgur.com/kVLFF"><img src="http://i.imgur.com/kVLFFl.gif" title="Hosted by imgur.com" alt="" /></a>

Para instalarlo tan solo tecleamos en una terminal:
{% highlight bash %}
sudo aptitude install iptraf
{% endhighlight %}

y luego lo ejecutamos con:

{% highlight bash %}
sudo iptraf
{% endhighlight %}

- Iftop: Escucha el trafico que hay en una interfaz de red y nos muestra en una tabla el ancho de banda consumido ademas del nombre de host remoto al cual estamos conectados y el puerto usado para la conexion.

<a href="http://imgur.com/K8pwa"><img src="http://i.imgur.com/K8pwal.png" title="Hosted by imgur.com" alt="" /></a>

Para instalarlo tan solo debemos teclear en una terminal:

{% highlight bash %}
sudo aptitude install iftop
{% endhighlight %}

y lo ejecutamos tecleando:

{% highlight bash %}
sudo iftop -i ppp0
{% endhighlight %}

Nota: cambie ppp0 por su interfaz de red. ejemplo: eth0 (cableada), wlan0 (inalambrica), ppp0 (modem), etc...

- Ifstat: es una herramienta para informarnos sobre el ancho de banda de las interfaces de red muy similar a  vmstat/iostat.

<a href="http://imgur.com/Woif2"><img src="http://i.imgur.com/Woif2l.jpg" title="Hosted by imgur.com" alt="" /></a>

Para instalarlo tan solo ejecutamos en una terminal:

{% highlight bash %}
sudo aptitude install ifstat
{% endhighlight %}

y lo ejecutamos tecleando:

{% highlight bash %}
ifstat -i ppp0
{% endhighlight %}

Nota: cambie ppp0 por su interfaz de red. ejemplo: eth0 (cableada), wlan0 (inalambrica), ppp0 (modem), etc...

**Comandos:**

- lsof

{% highlight bash %}
sudo lsof -i4
{% endhighlight %}

Segun el Man (Manual) de lsof, nos dice que este comando lista los archivos abiertos (de alli deriva su nombre: ls "listar",  o > de open y f > de file = lsof ) por lo que al ejecutarlo veremos una lista de las conexiones abiertas, que aplicacion, proceso o archivo la esta usando y tambien el puerto por el cual se realiza dicha conexion. Una salida de este comando mostraria algo similar a esto:

{% highlight text %}
COMMAND    PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
avahi-dae 1056   avahi   13u  IPv4   7319      0t0  UDP *:mdns
avahi-dae 1056   avahi   15u  IPv4   7321      0t0  UDP *:53814
dnsmasq   1214 dnsmasq    4u  IPv4   7595      0t0  UDP *:domain
dnsmasq   1214 dnsmasq    5u  IPv4   7596      0t0  TCP *:domain (LISTEN)
cupsd     1327    root    6u  IPv4   7752      0t0  TCP localhost.localdomain:ipp (LISTEN)
xchat     2805  usuario   14u  IPv4  22697      0t0  TCP Pc-Linux:43198->antonieta.freenode.net:8001 (ESTABLISHED)
pidgin    2807   usuario    9w  IPv4  24691      0t0  TCP Pc-Linux:59995->baymsg1.gateway.messenger.live.com:msnp (ESTABLISHED)
pidgin    2807   usuario   17u  IPv4  24548   0t0  TCP Pc-Linux:57466->1e100.net:xmpp-client (ESTABLISHED)
{% endhighlight %}

Para saber mas sobre este comando lee su manual tecleando en la terminal:

{% highlight bash %}
man lsof
{% endhighlight %}

- netstat:

{% highlight bash %}
sudo netstat -lptu
{% endhighlight %}

netstat es un comando que nos puede mostrar las conexiones de red, tablas de enrutamiento, estadisticas de las diferentes interfaces de red,  conexiones enmascaradas entre otras funciones. Con la opcion -lptu en realidad le estamos diciendo a netstat que nos muestre multiples opciones de informacion (cada letra equivale a una opcion) por lo que en este caso le estamos pidiendo que liste los sockets abierto "l", nos mueste los programas que estan usando esos sockets "p" y que sean mediante protocolos TCP "t" y UTP "u"

una salida tipica de este comando seria similar a esto:

{% highlight text %}
Conexiones activas de Internet (solo servidores)
Proto  Recib Enviad Dirección local         Dirección remota       Estado       PID/Program name
tcp        0      0 *:domain                *:*                        ESCUCHAR    1214/dnsmasq
tcp        0      0 localhost.localdoma:ipp *:*                     ESCUCHAR    1327/cupsd
tcp6       0      0 [::]:domain             [::]:*                     ESCUCHAR    1214/dnsmasq
tcp6       0      0 PC-Linux:ipp          [::]:*                      ESCUCHAR    1327/cupsd
udp        0      0 *:mdns                  *:*                                 1056/avahi-daemon:
udp        0      0 *:domain                *:*                                 1214/dnsmasq
udp        0      0 *:53814                 *:*                                 1056/avahi-daemon:
udp6       0      0 [::]:mdns               [::]:*                              1056/avahi-daemon:
udp6       0      0 [::]:42850              [::]:*                              1056/avahi-daemon:
udp6       0      0 [::]:domain             [::]:*                              1214/dnsmasq
{% endhighlight %}

Para saber mas de este comando y sus posibilidades teclea en la terminal:

{% highlight bash %}
man netstat
{% endhighlight %}

- ss:

{% highlight bash %}
ss -o
{% endhighlight %}

ss es un comando muy similar a netstat que nos sirve para investigar cualquier informacion acerca de los sockets y conexiones abiertas. ademas de volcado de datos.

Una salida tipica de este comando seria algo como esto:

{% highlight text %}
State      Recv-Q Send-Q                Local Address:Port                         Peer Address:Port
ESTAB      0      0                                     127:xx:xx:xx:34123             69:xx:xx:xx:www
CLOSE-WAIT 1      0                                 127:xx:xx:xx:42456       69:xx:xx:xx:www
ESTAB      0      0                                     127:xx:xx:xx:59995             69:xx:xx:xx:msnp
ESTAB      0      0                                     127:xx:xx:xx:37673              69:xx:xx:xx:www
{% endhighlight %}

Para saber mas de este comando teclea en la terminal:

{% highlight bash %}
man ss
{% endhighlight %}

Saludos.
