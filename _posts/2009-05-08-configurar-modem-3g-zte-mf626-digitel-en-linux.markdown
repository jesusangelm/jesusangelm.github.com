---
layout: post
title: !binary |-
  Q29uZmlndXJhciBNb2RlbSAzRyBaVEUgTUY2MjYgRGlnaXRlbCBlbiBMaW51
  eA==
tags:
- !binary |-
  YmFt
- !binary |-
  ZGlnaXRlbA==
- !binary |-
  Z25vbWU=
- !binary |-
  Z3VpYQ==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  bW9kZW0=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  dXNi
- !binary |-
  bWJy
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  ZXNjcml0b3Jpbw==
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
---
Este es otra guia que encontre para configurar el modem ZTE MF626 del Bam 3G de Digitel. Lo que deben hacer es lo Siguiente:

1)  Ir a esta pagina web (<a title="http://www.draisberghof.de/usb_modeswitch/" href="http://www.draisberghof.de/usb_modeswitch/">http://www.draisberghof.de/usb_modeswitch/</a>) y descargar el archivo “usb_modeswitch-0.9.6.tar.bz2 en la seccion Downloads.

2)  Hacer click derecho en el archivo y seleccionar Extraer Aqui.

3) Abrir Terminal, ir al directorio en el que descomprimio todo y ejecutar 

{% highlight bash %}
$ sudo make install
{% endhighlight %}

 va a pedir password de root.

4) Editar el archivo de configuracion “usb_modeswitch.conf”. Para eso en terminal ejecutar 

{% highlight bash %}
$ sudo gedit /etc/usb_modeswitch.conf
{% endhighlight %}

y se abrira el editor de textos de Gedit.

5) Buscarmas o menos por la linea 393 del archivo, el nombre del modem “ZTE MF626" y sacar los comentarios, el (#) y el (;), hasta que quede algo asi:

{% highlight bash session%}
ZTE MF628+ (tested version from Telia / Sweden)
ZTE MF626

Contributor: Joakim Wennergren

DefaultVendor=  0×19d2
DefaultProduct= 0×2000

TargetVendor=   0×19d2
TargetProduct=  0×0031

MessageEndpoint=0×01

MessageContent=”555342431234567820000000800o0

c85010101180101010101000000000000
{% endhighlight %}

6) Guardar y Salir.

7) Enchufar el modem, esperar unos segundos y ejecutar en Terminal “lsusb”. Aqui uno de los dispositivos deberia tener el ID 19d2:2000.

8) Ejecutar en Terminal 

{% highlight bash %}
$ sudo /usr/sbin/usb_modeswitch -W -c /etc/usb_modeswitch.conf
{% endhighlight %}

Con esto le cambiaremos el modo y ahora el sistema lo va a ver como un modem. 
Si hacen “lsusb” de nuevo, deberia haber cambiado a ID 19d2:0031

9) Ejecutamos en Terminal 

{% highlight bash %}
$ sudo /sbin/modprobe usbserial vendor=0×19d2 product=0×0031
{% endhighlight %}

10)  Ahora deberia andar como modem… se puede definir un archivo para que lo reconozca el network manager, haciendo en la terminal 

{% highlight bash %}
$ sudo gedit /usr/share/hal/fdi/information/20thirdparty/20-zte-mf626.fdi
{% endhighlight %}

Esto abrira un archivo en blanco al que hay que escribirle esto adentro, guardarlo y salir.

{% highlight bash %}
!– -*- SGML -*- –
deviceinfo version=”0.2
device
!– ZTE MF626 HSDPA USB Modem –
match key=”@info.parent:usb.vendor_id” int=”0×19d2
match key=”@info.parent:usb.product_id” int=”0×0031
match key=”@info.parent:usb.interface.number” int=”3
append key=”modem.command_sets” type=”strlist” GSM-07.07 /append
append key=”modem.command_sets” type=”strlist” GSM-07.05 /append
append key=”info.capabilities” type=”strlist” modem /append
/match
/match
/match
/device
/deviceinfo
{% endhighlight %}

ya en este momento nuestro modem esta listo para usarse. Solo falta definir los parametros de la conexion con DIGITEL 3G. OJO, la conexion es parecida a la de los telefonos celulares solo cambian algunos parametros. Actualmente solo me he podido conectar con WVDIAL. aqui les dejo mi wvdial.conf y mi /etc/ppp/options para que vean la conexion. Es importante recalcar que por defecto ppp autentica con PAP, y la conexion digitel usa CHAP.

Para configurar su conexion ahora utilizamos wvdialconf. Con esta apliacion de wvdial se tiene una configuracion incial que luego vamos a cambiar:

{% highlight bash %}
$ sudo gedit /etc/wvdial.conf
{% endhighlight %}

Y hacemos cambios para que se vea así

{% highlight bash %}
#La conexion de Digitel lleva el pin de la sim card   0000
Init1 = ATZ+CPIN=”0000?
Init2 = ATQ0 V1 E1 +FCLASS=0

Init3 = AT+CGDCONT=1,”IP”,”gprsweb.digitel.ve”

Modem Type = Analog Modem

Phone = *99#

ISDN = 0

Username = Digitel

Password = Digitel

Modem = /dev/ttyUSB2

Baud = 9600
{% endhighlight %}

la ubicacion de este modem por lo general es en /dev/ttyUSB2 pero se han visto casos donde varia puesto a que el ocupa los espacios ttyUSB0 al ttyUSB3.

En el archivo /etc/ppp/options debemos comentar la autenticacion con PAP y activar la conexion con CHAP.

nos ubicamos en esta sección y nos aseguramos que este así.

{% highlight bash %}
# Require the peer to authenticate itself using PAP.
#+pap</span>

# Don’t agree to authenticate using PAP.
#-pap

# Require the peer to authenticate itself using CHAP [Cryptographic
# Handshake Authentication Protocol] authentication.
+chap

# Don’t agree to authenticate using CHAP.
#-chap
{% endhighlight %}

Bueno ya con esto debemos estar listos para navegar.

Cada vez que queramos conectarnos

{% highlight bash %}
$ sudo /usr/sbin/usb_modeswitch -W -c /etc/usb_modeswitch.conf
$sudo wvdial
{% endhighlight %}

y debido a que la forma en que nos estamos conectado no aplica al escritorio que estemos usando. debemos asegurarnos que nuestro navegador no este trabajando en modo sin conexion.

Fuente:  <a href="http://effiejayx.velugmaracaibo.org.ve/" target="_blank">BsF 0.10...</a>
