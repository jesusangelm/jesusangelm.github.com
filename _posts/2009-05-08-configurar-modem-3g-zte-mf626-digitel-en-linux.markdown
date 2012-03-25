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

1)  Ir a esta pagina web (<a title="http://www.draisberghof.de/usb_modeswitch/" href="http://www.draisberghof.de/usb_modeswitch/">http://www.draisberghof.de/usb_modeswitch/</a>) y descargar el archivo “usb_modeswitch-0.9.6.tar.bz2? en la seccion Downloads.

2)  Hacer click derecho en el archivo y seleccionar &gt; Extraer Aqui.

3) Abrir Terminal, ir al directorio en el que descomprimio todo y ejecutar “sudo make install”… va a pedir password de root.

4) Editar el archivo de configuracion “usb_modeswitch.conf”. Para eso en terminal ejecutar “sudo gedit /etc/usb_modeswitch.conf” y se abrira el editor de textos de Gnome.

5) Buscarmas o menos por la linea 393 del archivo, el nombre del modem “ZTE MF626? y sacar los comentarios, el (#) y el (;), hasta que quede algo asi:
<blockquote>ZTE MF628+ (tested version from Telia / Sweden)
ZTE MF626

Contributor: Joakim Wennergren

DefaultVendor=  0×19d2
DefaultProduct= 0×2000

TargetVendor=   0×19d2
TargetProduct=  0×0031

MessageEndpoint=0×01

MessageContent=”555342431234567820000000800o0

c85010101180101010101000000000000?</blockquote>
6) Guardar y Salir.

7) Enchufar el modem, esperar unos segundos y ejecutar en Terminal “lsusb”. Aqui uno de los dispositivos deberia tener el r ID 19d2:2000.

<img class="wp-smiley" src="http://effiejayx.velugmaracaibo.org.ve/wp-includes/images/smilies/icon_cool.gif" alt="8)" /> Ejecutar en Terminal “sudo /usr/sbin/usb_modeswitch -W -c /etc/usb_modeswitch.conf”. Con esto le cambiaremos el modo y ahora el sistema lo va a ver como un modem. Si hacen “lsusb” de nuevo, deberia haber cambiado a ID 19d2:0031

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
<blockquote>[Dialer Defaults]
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

Baud = 9600</blockquote>
la ubicacion de este modem por lo general es en /dev/ttyUSB2 pero se han visto casos donde varia puesto a que el ocupa los espacios ttyUSB0 al ttyUSB3.

En el archivo /etc/ppp/options debemos comentar la autenticacion con PAP y activar la conexion con CHAP.

nos ubicamos en esta sección y nos aseguramos que este así.

<!--[if gte mso 9]><xml> <w :WordDocument> </w><w :View>Normal</w> <w :Zoom>0</w> <w :TrackMoves /> <w :TrackFormatting /> <w :HyphenationZone>21</w> <w :PunctuationKerning /> <w :ValidateAgainstSchemas /> <w :SaveIfXMLInvalid>false</w> <w :IgnoreMixedContent>false</w> <w :AlwaysShowPlaceholderText>false</w> <w :DoNotPromoteQF /> <w :LidThemeOther>ES-VE</w> <w :LidThemeAsian>X-NONE</w> <w :LidThemeComplexScript>X-NONE</w> <w :Compatibility> <w :BreakWrappedTables /> <w :SnapToGridInCell /> <w :WrapTextWithPunct /> <w :UseAsianBreakRules /> <w :DontGrowAutofit /> <w :SplitPgBreakAndParaMark /> <w :DontVertAlignCellWithSp /> <w :DontBreakConstrainedForcedTables /> <w :DontVertAlignInTxbx /> <w :Word11KerningPairs /> <w :CachedColBalance /> </w> <w :BrowserLevel>MicrosoftInternetExplorer4</w> <m :mathPr> <m :mathFont m:val="Cambria Math" /> <m :brkBin m:val="before" /> <m :brkBinSub m:val=" " /> <m :smallFrac m:val="off" /> <m :dispDef /> <m :lMargin m:val="0" /> <m :rMargin m:val="0" /> <m :defJc m:val="centerGroup" /> <m :wrapIndent m:val="1440" /> <m :intLim m:val="subSup" /> <m :naryLim m:val="undOvr" /> </m> </xml>< ![endif]--><!--[if gte mso 9]><xml> <w :LatentStyles DefLockedState="false" DefUnhideWhenUsed="true"   DefSemiHidden="true" DefQFormat="false" DefPriority="99"   LatentStyleCount="267"> <w :LsdException Locked="false" Priority="0" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Normal" /> <w :LsdException Locked="false" Priority="9" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="heading 1" /> <w :LsdException Locked="false" Priority="9" QFormat="true" Name="heading 2" /> <w :LsdException Locked="false" Priority="9" QFormat="true" Name="heading 3" /> <w :LsdException Locked="false" Priority="9" QFormat="true" Name="heading 4" /> <w :LsdException Locked="false" Priority="9" QFormat="true" Name="heading 5" /> <w :LsdException Locked="false" Priority="9" QFormat="true" Name="heading 6" /> <w :LsdException Locked="false" Priority="9" QFormat="true" Name="heading 7" /> <w :LsdException Locked="false" Priority="9" QFormat="true" Name="heading 8" /> <w :LsdException Locked="false" Priority="9" QFormat="true" Name="heading 9" /> <w :LsdException Locked="false" Priority="39" Name="toc 1" /> <w :LsdException Locked="false" Priority="39" Name="toc 2" /> <w :LsdException Locked="false" Priority="39" Name="toc 3" /> <w :LsdException Locked="false" Priority="39" Name="toc 4" /> <w :LsdException Locked="false" Priority="39" Name="toc 5" /> <w :LsdException Locked="false" Priority="39" Name="toc 6" /> <w :LsdException Locked="false" Priority="39" Name="toc 7" /> <w :LsdException Locked="false" Priority="39" Name="toc 8" /> <w :LsdException Locked="false" Priority="39" Name="toc 9" /> <w :LsdException Locked="false" Priority="35" QFormat="true" Name="caption" /> <w :LsdException Locked="false" Priority="10" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Title" /> <w :LsdException Locked="false" Priority="1" Name="Default Paragraph Font" /> <w :LsdException Locked="false" Priority="11" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Subtitle" /> <w :LsdException Locked="false" Priority="22" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Strong" /> <w :LsdException Locked="false" Priority="20" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Emphasis" /> <w :LsdException Locked="false" Priority="59" SemiHidden="false"    UnhideWhenUsed="false" Name="Table Grid" /> <w :LsdException Locked="false" UnhideWhenUsed="false" Name="Placeholder Text" /> <w :LsdException Locked="false" Priority="1" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="No Spacing" /> <w :LsdException Locked="false" Priority="60" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Shading" /> <w :LsdException Locked="false" Priority="61" SemiHidden="false"    UnhideWhenUsed="false" Name="Light List" /> <w :LsdException Locked="false" Priority="62" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Grid" /> <w :LsdException Locked="false" Priority="63" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 1" /> <w :LsdException Locked="false" Priority="64" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 2" /> <w :LsdException Locked="false" Priority="65" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 1" /> <w :LsdException Locked="false" Priority="66" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 2" /> <w :LsdException Locked="false" Priority="67" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 1" /> <w :LsdException Locked="false" Priority="68" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 2" /> <w :LsdException Locked="false" Priority="69" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 3" /> <w :LsdException Locked="false" Priority="70" SemiHidden="false"    UnhideWhenUsed="false" Name="Dark List" /> <w :LsdException Locked="false" Priority="71" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Shading" /> <w :LsdException Locked="false" Priority="72" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful List" /> <w :LsdException Locked="false" Priority="73" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Grid" /> <w :LsdException Locked="false" Priority="60" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Shading Accent 1" /> <w :LsdException Locked="false" Priority="61" SemiHidden="false"    UnhideWhenUsed="false" Name="Light List Accent 1" /> <w :LsdException Locked="false" Priority="62" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Grid Accent 1" /> <w :LsdException Locked="false" Priority="63" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 1 Accent 1" /> <w :LsdException Locked="false" Priority="64" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 2 Accent 1" /> <w :LsdException Locked="false" Priority="65" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 1 Accent 1" /> <w :LsdException Locked="false" UnhideWhenUsed="false" Name="Revision" /> <w :LsdException Locked="false" Priority="34" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="List Paragraph" /> <w :LsdException Locked="false" Priority="29" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Quote" /> <w :LsdException Locked="false" Priority="30" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Intense Quote" /> <w :LsdException Locked="false" Priority="66" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 2 Accent 1" /> <w :LsdException Locked="false" Priority="67" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 1 Accent 1" /> <w :LsdException Locked="false" Priority="68" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 2 Accent 1" /> <w :LsdException Locked="false" Priority="69" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 3 Accent 1" /> <w :LsdException Locked="false" Priority="70" SemiHidden="false"    UnhideWhenUsed="false" Name="Dark List Accent 1" /> <w :LsdException Locked="false" Priority="71" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Shading Accent 1" /> <w :LsdException Locked="false" Priority="72" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful List Accent 1" /> <w :LsdException Locked="false" Priority="73" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Grid Accent 1" /> <w :LsdException Locked="false" Priority="60" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Shading Accent 2" /> <w :LsdException Locked="false" Priority="61" SemiHidden="false"    UnhideWhenUsed="false" Name="Light List Accent 2" /> <w :LsdException Locked="false" Priority="62" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Grid Accent 2" /> <w :LsdException Locked="false" Priority="63" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 1 Accent 2" /> <w :LsdException Locked="false" Priority="64" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 2 Accent 2" /> <w :LsdException Locked="false"
 Priority="65" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 1 Accent 2" /> <w :LsdException Locked="false" Priority="66" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 2 Accent 2" /> <w :LsdException Locked="false" Priority="67" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 1 Accent 2" /> <w :LsdException Locked="false" Priority="68" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 2 Accent 2" /> <w :LsdException Locked="false" Priority="69" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 3 Accent 2" /> <w :LsdException Locked="false" Priority="70" SemiHidden="false"    UnhideWhenUsed="false" Name="Dark List Accent 2" /> <w :LsdException Locked="false" Priority="71" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Shading Accent 2" /> <w :LsdException Locked="false" Priority="72" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful List Accent 2" /> <w :LsdException Locked="false" Priority="73" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Grid Accent 2" /> <w :LsdException Locked="false" Priority="60" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Shading Accent 3" /> <w :LsdException Locked="false" Priority="61" SemiHidden="false"    UnhideWhenUsed="false" Name="Light List Accent 3" /> <w :LsdException Locked="false" Priority="62" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Grid Accent 3" /> <w :LsdException Locked="false" Priority="63" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 1 Accent 3" /> <w :LsdException Locked="false" Priority="64" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 2 Accent 3" /> <w :LsdException Locked="false" Priority="65" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 1 Accent 3" /> <w :LsdException Locked="false" Priority="66" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 2 Accent 3" /> <w :LsdException Locked="false" Priority="67" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 1 Accent 3" /> <w :LsdException Locked="false" Priority="68" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 2 Accent 3" /> <w :LsdException Locked="false" Priority="69" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 3 Accent 3" /> <w :LsdException Locked="false" Priority="70" SemiHidden="false"    UnhideWhenUsed="false" Name="Dark List Accent 3" /> <w :LsdException Locked="false" Priority="71" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Shading Accent 3" /> <w :LsdException Locked="false" Priority="72" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful List Accent 3" /> <w :LsdException Locked="false" Priority="73" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Grid Accent 3" /> <w :LsdException Locked="false" Priority="60" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Shading Accent 4" /> <w :LsdException Locked="false" Priority="61" SemiHidden="false"    UnhideWhenUsed="false" Name="Light List Accent 4" /> <w :LsdException Locked="false" Priority="62" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Grid Accent 4" /> <w :LsdException Locked="false" Priority="63" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 1 Accent 4" /> <w :LsdException Locked="false" Priority="64" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 2 Accent 4" /> <w :LsdException Locked="false" Priority="65" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 1 Accent 4" /> <w :LsdException Locked="false" Priority="66" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 2 Accent 4" /> <w :LsdException Locked="false" Priority="67" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 1 Accent 4" /> <w :LsdException Locked="false" Priority="68" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 2 Accent 4" /> <w :LsdException Locked="false" Priority="69" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 3 Accent 4" /> <w :LsdException Locked="false" Priority="70" SemiHidden="false"    UnhideWhenUsed="false" Name="Dark List Accent 4" /> <w :LsdException Locked="false" Priority="71" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Shading Accent 4" /> <w :LsdException Locked="false" Priority="72" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful List Accent 4" /> <w :LsdException Locked="false" Priority="73" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Grid Accent 4" /> <w :LsdException Locked="false" Priority="60" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Shading Accent 5" /> <w :LsdException Locked="false" Priority="61" SemiHidden="false"    UnhideWhenUsed="false" Name="Light List Accent 5" /> <w :LsdException Locked="false" Priority="62" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Grid Accent 5" /> <w :LsdException Locked="false" Priority="63" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 1 Accent 5" /> <w :LsdException Locked="false" Priority="64" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 2 Accent 5" /> <w :LsdException Locked="false" Priority="65" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 1 Accent 5" /> <w :LsdException Locked="false" Priority="66" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 2 Accent 5" /> <w :LsdException Locked="false" Priority="67" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 1 Accent 5" /> <w :LsdException Locked="false" Priority="68" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 2 Accent 5" /> <w :LsdException Locked="false" Priority="69" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 3 Accent 5" /> <w :LsdException Locked="false" Priority="70" SemiHidden="false"    UnhideWhenUsed="false" Name="Dark List Accent 5" /> <w :LsdException Locked="false" Priority="71" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Shading Accent 5" /> <w :LsdException Locked="false" Priority="72" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful List Accent 5" /> <w :LsdException Locked="false" Priority="73" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Grid Accent 5" /> <w :LsdException Locked="false" Priority="60" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Shading Accent 6" /> <w :LsdException Locked="false" Priority="61" SemiHidden="false"    UnhideWhenUsed="false" Name="Light List Accent 6" /> <w :LsdException Locked="false" Priority="62" SemiHidden="false"    UnhideWhenUsed="false" Name="Light Grid Accent 6" /> <w :LsdException Locked="false" Priority="63" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 1 Accent 6" /> <w :LsdException Locked="false" Priority="64" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Shading 2 Accent 6" /> <w :LsdException Locked="false" Priority="65" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 1 Accent 6" /> <w :LsdException Locked="false" Priority="66" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium List 2 Accent 6" /> <w :LsdException Locked="false" Priority="67" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 1 Accent 6" /> <w :LsdException Locked="false" Priority="68" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 2 Accent 6" /> <w :LsdException Locked="false" Priority="69" SemiHidden="false"    UnhideWhenUsed="false" Name="Medium Grid 3 Accent 6" /> <w :LsdException Locked="false" Priority="70" SemiHidden="false"    UnhideWhenUsed="false" Name="Dark List Accent 6" /> <w :LsdException Locked="false" Priority="71" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Shading Accent 6" /> <w :LsdException Locked="false" Priority="72" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful List Accent 6" /> <w :LsdException Locked="false" Priority="73" SemiHidden="false"    UnhideWhenUsed="false" Name="Colorful Grid Accent 6" /> <w :LsdException Locked="false" Priority="19" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Subtle Emphasis" /> <w :LsdException Locked="false" Pri
ority="21" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Intense Emphasis" /> <w :LsdException Locked="false" Priority="31" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Subtle Reference" /> <w :LsdException Locked="false" Priority="32" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Intense Reference" /> <w :LsdException Locked="false" Priority="33" SemiHidden="false"    UnhideWhenUsed="false" QFormat="true" Name="Book Title" /> <w :LsdException Locked="false" Priority="37" Name="Bibliography" /> <w :LsdException Locked="false" Priority="39" QFormat="true" Name="TOC Heading" /> </w> </xml>< ![endif]--><!--  /* Font Definitions */  @font-face 	{font-family:"Cambria Math"; 	panose-1:0 0 0 0 0 0 0 0 0 0; 	mso-font-charset:1; 	mso-generic-font-family:roman; 	mso-font-format:other; 	mso-font-pitch:variable; 	mso-font-signature:0 0 0 0 0 0;} @font-face 	{font-family:Calibri; 	panose-1:2 15 5 2 2 2 4 3 2 4; 	mso-font-charset:0; 	mso-generic-font-family:swiss; 	mso-font-pitch:variable; 	mso-font-signature:-1610611985 1073750139 0 0 159 0;} @font-face 	{font-family:Consolas; 	panose-1:2 11 6 9 2 2 4 3 2 4; 	mso-font-charset:0; 	mso-generic-font-family:modern; 	mso-font-pitch:fixed; 	mso-font-signature:-1610611985 1073750091 0 0 159 0;}  /* Style Definitions */  p.MsoNormal, li.MsoNormal, div.MsoNormal 	{mso-style-unhide:no; 	mso-style-qformat:yes; 	mso-style-parent:""; 	margin-top:0cm; 	margin-right:0cm; 	margin-bottom:10.0pt; 	margin-left:0cm; 	line-height:115%; 	mso-pagination:widow-orphan; 	font-size:11.0pt; 	font-family:"Calibri","sans-serif"; 	mso-ascii-font-family:Calibri; 	mso-ascii-theme-font:minor-latin; 	mso-fareast-font-family:Calibri; 	mso-fareast-theme-font:minor-latin; 	mso-hansi-font-family:Calibri; 	mso-hansi-theme-font:minor-latin; 	mso-bidi-font-family:"Times New Roman"; 	mso-bidi-theme-font:minor-bidi; 	mso-fareast-language:EN-US;} p.MsoPlainText, li.MsoPlainText, div.MsoPlainText 	{mso-style-priority:99; 	mso-style-link:"Texto sin formato Car"; 	margin:0cm; 	margin-bottom:.0001pt; 	mso-pagination:widow-orphan; 	font-size:10.5pt; 	font-family:Consolas; 	mso-fareast-font-family:Calibri; 	mso-fareast-theme-font:minor-latin; 	mso-bidi-font-family:"Times New Roman"; 	mso-bidi-theme-font:minor-bidi; 	mso-fareast-language:EN-US;} span.TextosinformatoCar 	{mso-style-name:"Texto sin formato Car"; 	mso-style-priority:99; 	mso-style-unhide:no; 	mso-style-locked:yes; 	mso-style-link:"Texto sin formato"; 	mso-ansi-font-size:10.5pt; 	mso-bidi-font-size:10.5pt; 	font-family:Consolas; 	mso-ascii-font-family:Consolas; 	mso-hansi-font-family:Consolas;} .MsoChpDefault 	{mso-style-type:export-only; 	mso-default-props:yes; 	mso-ascii-font-family:Calibri; 	mso-ascii-theme-font:minor-latin; 	mso-fareast-font-family:Calibri; 	mso-fareast-theme-font:minor-latin; 	mso-hansi-font-family:Calibri; 	mso-hansi-theme-font:minor-latin; 	mso-bidi-font-family:"Times New Roman"; 	mso-bidi-theme-font:minor-bidi; 	mso-fareast-language:EN-US;} .MsoPapDefault 	{mso-style-type:export-only; 	margin-bottom:10.0pt; 	line-height:115%;} @page Section1 	{size:612.0pt 792.0pt; 	margin:70.85pt 3.0cm 70.85pt 3.0cm; 	mso-header-margin:36.0pt; 	mso-footer-margin:36.0pt; 	mso-paper-source:0;} div.Section1 	{page:Section1;} --><!--[if gte mso 10]> <mce :style>< !   /* Style Definitions */  table.MsoNormalTable 	{mso-style-name:"Tabla normal"; 	mso-tstyle-rowband-size:0; 	mso-tstyle-colband-size:0; 	mso-style-noshow:yes; 	mso-style-priority:99; 	mso-style-qformat:yes; 	mso-style-parent:""; 	mso-padding-alt:0cm 5.4pt 0cm 5.4pt; 	mso-para-margin-top:0cm; 	mso-para-margin-right:0cm; 	mso-para-margin-bottom:10.0pt; 	mso-para-margin-left:0cm; 	line-height:115%; 	mso-pagination:widow-orphan; 	font-size:11.0pt; 	font-family:"Calibri","sans-serif"; 	mso-ascii-font-family:Calibri; 	mso-ascii-theme-font:minor-latin; 	mso-hansi-font-family:Calibri; 	mso-hansi-theme-font:minor-latin; 	mso-fareast-language:EN-US;} --> <!--[endif]-->
<blockquote>
<p class="MsoPlainText"><span style="font-family: &quot;Courier New&quot;;" lang="EN-US"># Require the peer to authenticate itself using PAP.
#+pap</span>

# Don’t agree to authenticate using PAP.
#-pap

# Require the peer to authenticate itself using CHAP [Cryptographic
# Handshake Authentication Protocol] authentication.
+chap

# Don’t agree to authenticate using CHAP.
#-chap</p></blockquote>
Bueno y Ya con esto debemos estar listos para navegar.

Cada vez que queramos conectarnos
<blockquote>sudo /usr/sbin/usb_modeswitch -W -c /etc/usb_modeswitch.conf
sudo wvdial</blockquote>
y debido a que la forma en que nos estamos conectado no aplica al escritorio que estemos usando. debemos asegurarnos que nuestro navegador no este trabajando en modo sin conexion.

Fuente:  <a href="http://effiejayx.velugmaracaibo.org.ve/" target="_blank">BsF 0.10...</a></mce>
