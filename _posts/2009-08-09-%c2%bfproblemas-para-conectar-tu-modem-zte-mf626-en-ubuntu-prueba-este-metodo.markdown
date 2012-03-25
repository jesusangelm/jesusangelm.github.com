---
layout: post
title: !binary |-
  wr9Qcm9ibGVtYXMgcGFyYSBjb25lY3RhciB0dSBtb2RlbSBaVEUgbWY2MjYg
  ZW4gVWJ1bnR1PyBwcnVlYmEgZXN0ZSBtZXRvZG8=
tags:
- !binary |-
  YmFt
- !binary |-
  YmxvZw==
- !binary |-
  ZGlnaXRlbA==
- !binary |-
  Z25vbWU=
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGlicmU=
- !binary |-
  bGludXg=
- !binary |-
  bW9kZW0=
- !binary |-
  dWJ1bnR1
- !binary |-
  dXNi
- !binary |-
  bWJy
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  bWF5bw==
- !binary |-
  YmFy
- !binary |-
  aHVhd2Vp
- !binary |-
  ZG5z
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
---
Bueno hace meses habia colocado 2 post en mi blog referente a la configuracion de la conexion de los modems Bam 3G de Digitel en Linux, tanto para el modelo ZTE como el Huawei.   En lo personal no habia probado esos metodos de configuracion ya que no disponia de ninguno de los dos.

Pues bueno hace un par de meses me compre el modelo ZTE MF626 y una de las primeras cosas que hice con el fue poner en practica la configuracion para poder navegar de manera segura y libre con Ubuntu 9.04, pero alli fue donde vino mi primer agarre con el dichoso modem, Ubuntu y los pasos de configuracion :D  no hubo manera que me funcionara :(

Luego de buscar en unos cuantos fotos diferentes metodos para realizar la conexion me di cuenta que la mayoria; por no decir todos los metodos son practicamente iguales a exepcion de algunos detalles.  me puse hoy a modificar ciertas partes del metodo publicado aca y empese a probar, hasta que di con mi solucion y logre conectarme, esto son los pasos que hice para que me funcionara la conexion:

NOTA: antes de hacer todo esto instalen el paquete wvdial para que les puedan funcionar el comando "sudo wvdial". normalmente esta en el DVD de Ubuntu, no se si tambien esta en el CD.

<!-- 		@page { margin: 2cm } 		P { margin-bottom: 0.21cm } 		A:link { so-language: zxx } -->

1)  Ir a esta pagina web (<a href="http://www.draisberghof.de/usb_modeswitch/">http://www.draisberghof.de/usb_modeswitch/</a>) y descargar el archivo “<a href="http://www.draisberghof.de/usb_modeswitch/usb_modeswitch-1.0.2.tar.bz2">usb_modeswitch-1.0.2.tar.bz2</a>? en la seccion Downloads.

2)  Hacer click derecho en el archivo y seleccionar &gt; Extraer Aqui.

3) Abrir Terminal, ir al directorio en el que descomprimio todo y ejecutar “sudo make install”… va a pedir password de root.

4) Editar el archivo de configuracion “usb_modeswitch.conf”. Para eso en terminal ejecutar “sudo gedit /etc/usb_modeswitch.conf” y se abrira el editor de textos de Gnome.

5) Buscarmas o menos por la linea 393 del archivo, el nombre del modem “ZTE MF626? y sacar los comentarios, el (#) y el (;), hasta que quede algo asi:

ZTE MF628+ (tested version from Telia / Sweden)
ZTE MF626

Contributor: Joakim Wennergren

DefaultVendor=  0×19d2
DefaultProduct= 0×2000

TargetVendor=   0×19d2
TargetProduct=  0×0031

MessageEndpoint=0×01
MessageContent=”55534243123456782000000080000c85010101180101010101000000000000?

6) Guardar y Salir.

7) Enchufar el modem, esperar unos segundos y ejecutar en Terminal “lsusb”. Aqui uno de los dispositivos deberia tener el r ID 19d2:2000.
8)Ejecutar en Terminal “sudo /usr/sbin/usb_modeswitch -W -c /etc/usb_modeswitch.conf”. Con esto le cambiaremos el modo y ahora el sistema lo va a ver como un modem. Si hacen “lsusb” de nuevo, deberia haber cambiado a ID 19d2:0031

9) Ejecutamos en Terminal “sudo /sbin/modprobe usbserial vendor=0×19d2 product=0×0031?

10)  Ahora deberia andar como modem… se puede definir un archivo para que lo reconozca el network manager, haciendo en la terminal “sudo gedit /usr/share/hal/fdi/information/20thirdparty/20-zte-mf626.fdi”. Esto abrira un archivo en blanco al que hay que escribirle esto adentro, guardarlo y salir.

&lt;!– -*- SGML -*- –&gt;
&lt;deviceinfo version=”0.2?&gt;
&lt;device&gt;
&lt;!– ZTE MF626 HSDPA USB Modem –&gt;
&lt;match key=”@info.parent:usb.vendor_id” int=”0×19d2?&gt;
&lt;match key=”@info.parent:usb.product_id” int=”0×0031?&gt;
&lt;match key=”@info.parent:usb.interface.number” int=”3?&gt;
&lt;append key=”modem.command_sets” type=”strlist”&gt;GSM-07.07&lt;/append&gt;
&lt;append key=”modem.command_sets” type=”strlist”&gt;GSM-07.05&lt;/append&gt;
&lt;append key=”info.capabilities” type=”strlist”&gt;modem&lt;/append&gt;
&lt;/match&gt;
&lt;/match&gt;
&lt;/match&gt;
&lt;/device&gt;
&lt;/deviceinfo&gt;

ya en este momento nuestro modem esta listo para usarse. Solo falta definir los parametros de la conexion con DIGITEL 3G. OJO, la conexion es parecida a la de los telefonos celulares solo cambian algunos parametros. Actualmente solo me he podido conectar con WVDIAL. aqui les dejo mi wvdial.conf y mi /etc/ppp/options para que vean la conexion. Es importante recalcar que por defecto ppp autentica con PAP, y la conexion digitel usa CHAP.

Para configurar su conexion ahora utilizamos wvdialconf. Con esta apliacion de wvdial se tiene una configuracion incial que luego vamos a cambiar:
<blockquote>sudo gedit /etc/wvdial.conf</blockquote>
Y hacemos cambios para que se vea así
<pre>[Dialer Defaults]

Init1 = ATZ

Init2 = ATQ0 V1 E1 S0=0 &amp;C1 &amp;D2 +FCLASS=0

Init3 = AT+CGDCONT=1,"IP","gprsweb.digitel.ve"

Modem Type = Analog Modem

Baud = 460800

New PPPD = yes

Modem = /dev/ttyUSB2

ISDN = off

Phone = *99#

Password = Digitel

Username = Digitel

Stupid Mode = on

Auto Reconnect = off

Abort on Busy = off

Carrier Check = off

Check Def Route = on

Abort on No Dialtone = on

Idle Seconds = 0

Auto DNS = off</pre>
la ubicacion de este modem por lo general es en /dev/ttyUSB2 pero se han visto casos donde varia puesto a que el ocupa los espacios ttyUSB0 al ttyUSB3.

En el archivo /etc/ppp/options debemos comentar la autenticacion con PAP y activar la conexion con CHAP.

nos ubicamos en esta sección y nos aseguramos que este así.
<p style="margin-left: 1cm; margin-right: 1cm;" lang="en-US"><!--[if gte mso 9]&gt;  Normal 0   21   false false false  ES-VE X-NONE X-NONE              MicrosoftInternetExplorer4              &lt;![endif]--><!--[if gte mso 9]&gt;--><!-- /* Font Definitions */  @font-face 	{font-family:"Cambria Math"; 	panose-1:0 0 0 0 0 0 0 0 0 0; 	mso-font-charset:1; 	mso-generic-font-family:roman; 	mso-font-format:other; 	mso-font-pitch:variable; 	mso-font-signature:0 0 0 0 0 0;} @font-face 	{font-family:Calibri; 	panose-1:2 15 5 2 2 2 4 3 2 4; 	mso-font-charset:0; 	mso-generic-font-family:swiss; 	mso-font-pitch:variable; 	mso-font-signature:-1610611985 1073750139 0 0 159 0;} @font-face 	{font-family:Consolas; 	panose-1:2 11 6 9 2 2 4 3 2 4; 	mso-font-charset:0; 	mso-generic-font-family:modern; 	mso-font-pitch:fixed; 	mso-font-signature:-1610611985 1073750091 0 0 159 0;}  /* Style Definitions */  p.MsoNormal, li.MsoNormal, div.MsoNormal 	{mso-style-unhide:no; 	mso-style-qformat:yes; 	mso-style-parent:""; 	margin-top:0cm; 	margin-right:0cm; 	margin-bottom:10.0pt; 	margin-left:0cm; 	line-height:115%; 	mso-pagination:widow-orphan; 	font-size:11.0pt; 	font-family:"Calibri","sans-serif"; 	mso-ascii-font-family:Calibri; 	mso-ascii-theme-font:minor-latin; 	mso-fareast-font-family:Calibri; 	mso-fareast-theme-font:minor-latin; 	mso-hansi-font-family:Calibri; 	mso-hansi-theme-font:minor-latin; 	mso-bidi-font-family:"Times New Roman"; 	mso-bidi-theme-font:minor-bidi; 	mso-fareast-language:EN-US;} p.MsoPlainText, li.MsoPlainText, div.MsoPlainText 	{mso-style-priority:99; 	mso-style-link:"Texto sin formato Car"; 	margin:0cm; 	margin-bottom:.0001pt; 	mso-pagination:widow-orphan; 	font-size:10.5pt; 	font-family:Consolas; 	mso-fareast-font-family:Calibri; 	mso-fareast-theme-font:minor-latin; 	mso-bidi-font-family:"Times New Roman"; 	mso-bidi-theme-font:minor-bidi; 	mso-fareast-language:EN-US;} span.TextosinformatoCar 	{mso-style-name:"Texto sin formato Car"; 	mso-style-priority:99; 	mso-style-unhide:no; 	mso-style-locked:yes; 	mso-style-link:"Texto sin formato"; 	mso-ansi-font-size:10.5pt; 	mso-bidi-font-size:10.5pt; 	font-family:Consolas; 	mso-ascii-font-family:Consolas; 	mso-hansi-font-family:Consolas;} .MsoChpDefault 	{mso-style-type:export-only; 	mso-default-props:yes; 	mso-ascii-font-family:Calibri; 	mso-ascii-theme-font:minor-latin; 	mso-fareast-font-family:Calibri; 	mso-fareast-theme-font:minor-latin; 	mso-hansi-font-family:Calibri; 	mso-hansi-theme-font:minor-latin; 	mso-bidi-font-family:"Times New Roman"; 	mso-bidi-theme-font:minor-bidi; 	mso-fareast-language:EN-US;} .MsoPapDefault 	{mso-style-type:export-only; 	margin-bottom:10.0pt; 	line-height:115%;} @page Section1 	{size:612.0pt 792.0pt; 	margin:70.85pt 3.0cm 70.85pt 3.0cm; 	mso-header-margin:36.0pt; 	mso-footer-margin:36.0pt; 	mso-paper-source:0;} div.Section1 	{page:Section1;} --><!--[if gte mso 10]&gt; &lt;!   /* Style Definitions */  table.MsoNormalTable 	{mso-style-name:"Tabla normal"; 	mso-tstyle-rowband-size:0; 	mso-tstyle-colband-size:0; 	mso-style-noshow:yes; 	mso-style-priority:99; 	mso-style-qformat:yes; 	mso-style-parent:""; 	mso-padding-alt:0cm 5.4pt 0cm 5.4pt; 	mso-para-margin-top:0cm; 	mso-para-margin-right:0cm; 	mso-para-margin-bottom:10.0pt; 	mso-para-margin-left:0cm; 	line-height:115%; 	mso-pagination:widow-orphan; 	font-size:11.0pt; 	font-family:"Calibri","sans-serif"; 	mso-ascii-font-family:Calibri; 	mso-ascii-theme-font:minor-latin; 	mso-hansi-font-family:Calibri; 	mso-hansi-theme-font:minor-latin; 	mso-fareast-language:EN-US;} --><!--[endif]--><span style="font-family: &quot;&quot;;"># Require the peer to authenticate itself using PAP.
#+pap</span>
<blockquote># Don’t agree to authenticate using PAP.
#-pap</blockquote>
<blockquote># Require the peer to authenticate itself using CHAP [Cryptographic
# Handshake Authentication Protocol] authentication.
+chap</blockquote>
<blockquote># Don’t agree to authenticate using CHAP.
#-chap</blockquote>
Bueno y Ya con esto debemos estar listos para navegar.

Cada vez que queramos conectarnos

sudo /usr/sbin/usb_modeswitch -W -c /etc/usb_modeswitch.conf
sudo wvdial

si asi tampoco funciona verificamos que el dispositivo este siendo reconocido como modem, tecleando "lsusb" deberia devolvernos en unas de las lineas este ID 19d2:0031 ... si te muestra otro es porque no esta siendo reconocido como modem, asi que tecleamos:

Y bueno como muestra un boton, este post lo escribi usando Ubuntu 9.04 conectado por Bam 3G Digitel :D

De seguro se preguntaran, ¿y al reiniciar o apagar la Pc  que pasa? ¿seguro se pierde toda la configuracion?

Pues bueno yo pense lo mismo asi que despues de descargar todo lo necesario reinicie la pc (deje conectado el modem al puerto USB) y al volver.....  no me funcionaba de manera directa el wvdial :(  no encontraba el dispositivo en /dev/ttyUSB3 asi que probando lo cambie a /dev/ttyUSB2
<blockquote>sudo /usr/sbin/usb_modeswitch -W -c /etc/usb_modeswitch.conf</blockquote>
y luego
<blockquote>sudo wvdial</blockquote>
<blockquote></blockquote>
Saludos y espero que ahora si les funcione a todos</p>
