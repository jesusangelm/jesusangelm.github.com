---
layout: post
title: !binary |-
  NiBTZW5jaWxsYXMgaGVycmFtaWVudGFzIGRlIG1vbml0b3JlbyBkZSByZWQg
  dXRpbGVz
tags:
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  bW9kZW0=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  bWFudWFs
- !binary |-
  bWJy
- !binary |-
  bW9uaXRvcg==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  ZG5z
- !binary |-
  ZG5zbWFzcQ==
- !binary |-
  Y2hhdA==
- !binary |-
  Y29tYW5kb3M=
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
- !binary |-
  bW9uaXRvcmVhcg==
- !binary |-
  ZXN0YWRpc3RpY2Fz
- !binary |-
  YXJjaGl2b3M=
- !binary |-
  cmVtb3Rv
---
Desde hace unos meses para aca e estado leyendo un poco de las grandes posibilidades que ofrece la terminal y su gran poder para controlar y administar practicamente toda tu PC.  Ultimamente e estado viendo aplicaciones y comandos para la terminal que me permitan ver y monitoriar las conexiones a internet por lo que les traigo aqui 3 comandos y 3 aplicaciones de terminal utiles para monitoriar tu red.

<strong>Aplicaciones:</strong>

- Iptraf:  Es una aplicacion basada en la terminal de estadisticas de red. tiene como caracteristicas el conteo de bytes y monitoreo de conexiones de paquetes TCP. Tambien ofrece estadisticas de las interfaces de red (eth0, ppp0, wlan0, etc) e indicadores de actividad, tambien nos muestra las interrupciones de trafico TCP/UDP.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/10/iptraf-iptm1.gif"><img class="aligncenter size-medium wp-image-453" title="iptraf-iptm1" src="http://blog.jam.net.ve/imagenes/uploads/2010/10/iptraf-iptm1-300x188.gif" alt="" width="300" height="188" /></a>

Para instalarlo tan solo tecleamos en una terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install iptraf</pre>
y luego lo ejecutamos con:
<pre lang="bash" line="1" escaped="true">sudo iptraf</pre>
- Iftop: Escucha el trafico que hay en una interfaz de red y nos muestra en una tabla el ancho de banda consumido ademas del nombre de host remoto al cual estamos conectados y el puerto usado para la conexion.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/10/iftop_normal.png"><img class="aligncenter size-medium wp-image-454" title="iftop_normal" src="http://blog.jam.net.ve/imagenes/uploads/2010/10/iftop_normal-300x183.png" alt="" width="300" height="183" /></a>

Para instalarlo tan solo debemos teclear en una terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install iftop</pre>
y lo ejecutamos tecleando:
<pre lang="bash" line="1" escaped="true">sudo iftop -i ppp0</pre>
Nota: cambie ppp0 por su interfaz de red. ejemplo: eth0 (cableada), wlan0 (inalambrica), ppp0 (modem), etc...

- Ifstat: es una herramienta para informarnos sobre el ancho de banda de las interfaces de red muy similar a  vmstat/iostat.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/10/Selección_002.jpeg"><img class="aligncenter size-medium wp-image-455" title="Selección_002" src="http://blog.jam.net.ve/imagenes/uploads/2010/10/Selección_002-300x234.jpg" alt="" width="300" height="234" /></a>

Para instalarlo tan solo ejecutamos en una terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install ifstat</pre>
y lo ejecutamos tecleando:
<pre lang="bash" line="1" escaped="true">ifstat -i ppp0</pre>
Nota: cambie ppp0 por su interfaz de red. ejemplo: eth0 (cableada), wlan0 (inalambrica), ppp0 (modem), etc...

<strong>Comandos:</strong>

-lsof
<pre lang="bash" line="1" escaped="true">sudo lsof -i4</pre>
Segun el Man (Manual) de lsof, nos dice que este comando lista los archivos abiertos (de alli deriva su nombre: ls &gt;listar,  o &gt; de open y f &gt; de file = lsof ) por lo que al ejecutarlo veremos una lista de las conexiones abiertas, que aplicacion, proceso o archivo la esta usando y tambien el puerto por el cual se realiza dicha conexion. Una salida de este comando mostraria algo similar a esto:
<pre lang="text" line="1" escaped="true">COMMAND    PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
avahi-dae 1056   avahi   13u  IPv4   7319      0t0  UDP *:mdns
avahi-dae 1056   avahi   15u  IPv4   7321      0t0  UDP *:53814
dnsmasq   1214 dnsmasq    4u  IPv4   7595      0t0  UDP *:domain
dnsmasq   1214 dnsmasq    5u  IPv4   7596      0t0  TCP *:domain (LISTEN)
cupsd     1327    root    6u  IPv4   7752      0t0  TCP localhost.localdomain:ipp (LISTEN)
xchat     2805  usuario   14u  IPv4  22697      0t0  TCP Pc-Linux:43198-&gt;antonieta.freenode.net:8001 (ESTABLISHED)
pidgin    2807   usuario    9w  IPv4  24691      0t0  TCP Pc-Linux:59995-&gt;baymsg1.gateway.messenger.live.com:msnp (ESTABLISHED)
pidgin    2807   usuario   17u  IPv4  24548   0t0  TCP Pc-Linux:57466-&gt;1e100.net:xmpp-client (ESTABLISHED)</pre>
Para saber mas sobre este comando lee su manual tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">man lsof</pre>
- netstat:
<pre lang="bash" line="1" escaped="true">sudo netstat -lptu</pre>
netstat es un comando que nos puede mostrar las conexiones de red, tablas de enrutamiento, estadisticas de las diferentes interfaces de red,  conexiones enmascaradas entre otras funciones. Con la opcion -lptu en realidad le estamos diciendo a netstat que nos muestre multiples opciones de informacion (cada letra equivale a una opcion) por lo que en este caso le estamos pidiendo que liste los sockets abierto "l", nos mueste los programas que estan usando esos sockets "p" y que sean mediante protocolos TCP "t" y UTP "u"

una salida tipica de este comando seria similar a esto:
<pre lang="text" line="1" escaped="true">Conexiones activas de Internet (solo servidores)
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
udp6       0      0 [::]:domain             [::]:*                              1214/dnsmasq</pre>
Para saber mas de este comando y sus posibilidades teclea en la terminal:
<pre lang="bash" line="1" escaped="true">man netstat</pre>
- ss:
<pre lang="bash" line="1" escaped="true">ss -o</pre>
ss es un comando muy similar a netstat que nos sirve para investigar cualquier informacion acerca de los sockets y conexiones abiertas. ademas de volcado de datos.

Una salida tipica de este comando seria algo como esto:
<pre lang="bash" line="1" escaped="true">State      Recv-Q Send-Q                Local Address:Port                         Peer Address:Port
ESTAB      0      0                                     127:xx:xx:xx:34123             69:xx:xx:xx:www
CLOSE-WAIT 1      0                                 127:xx:xx:xx:42456       69:xx:xx:xx:www
ESTAB      0      0                                     127:xx:xx:xx:59995             69:xx:xx:xx:msnp
ESTAB      0      0                                     127:xx:xx:xx:37673              69:xx:xx:xx:www</pre>
Para saber mas de este comando teclea en la terminal:
<pre lang="bash" line="1" escaped="true">man ss</pre>
Saludos.
