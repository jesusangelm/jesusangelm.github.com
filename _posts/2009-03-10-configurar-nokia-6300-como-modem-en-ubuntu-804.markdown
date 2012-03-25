---
layout: post
title: !binary |-
  Q29uZmlndXJhciBOb2tpYSA2MzAwIGNvbW8gTW9kZW0gZW4gVWJ1bnR1IDgu
  MDQ=
tags:
- !binary |-
  YmxvZw==
- !binary |-
  ZGViaWFu
- !binary |-
  ZGlnaXRlbA==
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bW9kZW0=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  dWJ1bnR1
- !binary |-
  dXNi
- !binary |-
  YmFy
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
---
Si alguno de ustedes a leido la pagina "<a title="Acerca de Jamunix Blog" href="http://blog.jam.net.ve/about/" target="_blank">Acerca De...</a>" sabra que mi primera instalacion fija de Ubuntu a fue la 8.10 que todavia uso, pero antes de eso y a modo de pruebas tenia instalado Ubuntu 8.04.  Una de las primeras cosas que queria hacer en Ubuntu apenas lo instale, era conectarme a internet. Luego de buscar por muchos foros y blog encontre un buen post en un blog de otro Venezolano que me ayudo a lograr conectar mi Nokia 6300 Digitel en Ubuntu 8.04
<p style="text-align: center;"><img class="aligncenter" title="Nokia 6300" src="http://www.jam.net.ve/blog/imagenes/nokia6300.gif" alt="" width="133" height="163" /></p>

Para realizar la configuracion debemos conectar el telefono por USB a la PC en "Modo Nokia" o "Modo Telefono"

Luego abrimos la Consola y tecleamos:
<blockquote><span style="color: #000000;">dmesg | grep ACM</span></blockquote>
<span style="color: #000000;">Ese comando deberia devolvernos algo como esto:</span>
<blockquote><span style="color: #000000;">cdc_acm 1-1:1.0: ttyACM0: USB ACM</span></blockquote>
<span style="color: #000000;">Eso nos hara saber que Ubuntu reconocio el telefono como modem.</span>

<span style="color: #000000;">Ahora teclearemos en la Consola:</span>
<blockquote><span style="color: #000000;">ls -lh /dev/ttyACM0</span></blockquote>
<span style="color: #000000;">y nos debe dar algo similar a esto.</span>
<blockquote><span style="color: #000000;">crw-r--r-- 1 root root 166, 0 Mar 17 07:47 /dev/ttyACM0</span></blockquote>
<span style="color: #000000;">Esto nos hace saber que tenemos acceso al dispositivo.</span>

<span style="color: #000000;">Ahora se tecleara en la consola:</span>
<blockquote><span style="color: #000000;">sudo chmod a+rw /dev/ttyACM0</span></blockquote>
<span style="color: #000000;">Para cambiar los permisos de acceso.</span>

<span style="color: #000000;">Hasta ahora todo bien, nos falta configurar Wvdial. Asi que escribe en la consola:</span>
<blockquote><span style="color: #000000;">sudo gedit /etc/wvdial.conf</span></blockquote>
<span style="color: #000000;">y se nos abrira el archivo wvdial.conf en el editor el cual cambaremos ciertos parametros:</span>

<strong><span style="color: #000000;">[Dialer Defaults]
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &amp;C1 &amp;D2 +FCLASS=0
Init3 = AT+CGDCONT=1,"IP","gprsweb.digitel.ve"
Modem Type = USB Modem
ISDN = 0
New PPPD = yes
Phone = *99#
Modem = /dev/ttyACM0
Username = guest
Password = guest
Baud = 460800</span></strong>

<span style="color: #000000;">Una vez editado guardamos, cerramos y nos vamos de nuevo a la consola para teclear:</span>
<blockquote><span style="color: #000000;">sudo wvdial</span></blockquote>
<span style="color: #000000;">y empesaran a correr varios mensajes de la secuencia de conexion, tan solo abre tu navegador y carga una pagina. Si todo a ido bien ya debes estar conectado a internet !!!</span>

<span style="color: #000000;">Para desconectarte tan solo debes usar la combinacion de tecla <strong>Ctrl+C</strong></span>

<span style="color: #000000;">Fuente: <a title="DmitriSite325" href="http://dmitrisite325.blogspot.com/2007/12/usando-un-celular-como-modem-en-ubuntu.html" target="_blank">Dmitrisite325</a></span>

<span style="color: #000000;">Esta configuracion se realizo con la consola y/o terminal en Ubuntu 8.04</span>

<span style="color: #000000;">Pero si tienes el nuevo Ubuntu 8.10 no es necesario o al menos no deberia ser necesario realizar esta configuracion, ya que Ubuntu 8.10 viene con soporte para conexiones 3G y reconoce automaticamente un Nokia 6300 como modem y crea la conexion.  Esta configuracion por medio de la consola tambien deberia ser funcional para distribuciones derivadas de Debian y/o Ubuntu.   Asi como tambien deberia de funcionar con otros modelos de telefonos Nokia y telefonos de otra marca.
</span>

<span style="color: #000000;">Saludos y espero le sirva a alguien mas.
</span>
