---
layout: post
title: !binary |-
  Q29zYXMgcXVlIGhhY2VyIGRlc3B1ZXMgZGUgaW5zdGFsYXIgVWJ1bnR1IDku
  MTAgS2FybWljIEtvYWxhLg==
tags:
- !binary |-
  Y29kZWM=
- !binary |-
  Z25vbWU=
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  amF2YQ==
- !binary |-
  a2FybWlj
- !binary |-
  a29hbGE=
- !binary |-
  bGludXg=
- !binary |-
  bXVsdGltZWRpYQ==
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  c29mdHdhcmU=
- !binary |-
  dWJ1bnR1
- !binary |-
  d2luZG93cw==
- !binary |-
  YWN0dWFsaXphY2lvbg==
- !binary |-
  bWFudWFs
- !binary |-
  Z3J1Yg==
- !binary |-
  bWJy
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  ZXNjcml0b3Jpbw==
- !binary |-
  bWF5bw==
- !binary |-
  YmFy
- !binary |-
  YXBwbGV0
- !binary |-
  dmxj
- !binary |-
  cmVwcm9kdWN0b3I=
- !binary |-
  dmlkZW8=
- !binary |-
  YmFzaA==
- !binary |-
  Y2FjaGU=
- !binary |-
  d2Vi
- !binary |-
  cmVsZWFzZQ==
- !binary |-
  dGVybWluYWw=
- !binary |-
  ZG9jaw==
- !binary |-
  eW91dHViZQ==
---
<ul>
	<li> Instalar software mas rapidamente.</li>
</ul>
Suele ocurrir (y especialmente) cuando sale una nueva version de Ubuntu, que los repositorios desde los cuales nos solemos descargar software estan muy saturados. Si queremos descargar e instalar el software mas rapidamente, tendremos que modificar la lista de repositorios.

Existe una opcion de Synaptic, que nos permite seleccionar un servidor mas cercano a nuestra region. Para cambiar este servidor a uno mas cercano vamos a Sistema &gt; Administracion &gt; Origenes de software y en la pestaña “Software de Ubuntu”, seleccionamos “descargar desde:” indicando la region mas cercanaa la nuestra.
<ul>
	<li>Instalar el software basico de compilacion</li>
</ul>
Si queremos compilar algun paquete del que solo tenemos el codigo fuente, tendremos que instalar los paquetes
basicos de compilacion. Lo instalamos con:

[bash] sudo aptitude install build-essential [/bash]
<ul>
	<li>Instalar los extra restrictivos.</li>
</ul>
Hay ciertos paquetes que no vienen por defecto en Ubuntu por cuestiones legales. Cuando se instala ubuntu, por defecto y debido a un tema de licencias no instala todo ese software comercial que no ha liberado el codigo fuente, como por ejemplo puede ser el plugin de flash, o los codecs para poder reproducir algunos formatos de video. Existe un metapaquete (un paquete que agrupa e instala muchos mas paquetes) llamado ubuntu-restricted-extras que nos permiteinstalar todo este software que no es instalado por defecto.

Tras habilitar los repositorios universe y multiverse podemos instalar este metapaquete con:

[bash] sudo apt-get install ubuntu-restricted-extras [/bash]
<ul>
	<li>Otra opcion es añadir el repositorio mediubuntu</li>
</ul>
Mediubuntu es un repositorio donde podemos encontrar algunas aplicaciones y codecs que no son instalador por defecto. Podemos añadirlo a la lista de repositorios ejecutando, desde una terminal:

[bash] sudo wget http://www.medibuntu.org/sources.list.d/$(lsb_release -cs).list \
 --output-document=/etc/apt/sources.list.d/medibuntu.list &amp;&amp;
sudo apt-get -q update &amp;&amp;
sudo apt-get --yes -q --allow-unauthenticated install medibuntu-keyring &amp;&amp;
sudo apt-get -q update [/bash]
<ul>
	<li>Instalamos Codecs Multimedia DVD</li>
</ul>
[bash] sudo apt-get install libdvdread4 libdvdcss2 [/bash]

Segun nuestra plataforma, instalamos CODECS:
<ul>
	<li> For i386, the package is called w32codecs:  [bash] sudo apt-get install w32codecs [/bash]</li>
	<li> For amd64, the package is called w64codecs:  [bash] sudo apt-get install w64codecs [/bash]</li>
	<li> For ppc, the package is called ppc-codecs:  [bash] sudo apt-get install ppc-codecs [/bash]</li>
</ul>
* Instalar Avant Window Navigator  AWN es un dock similar al de Mac, que nos permite lanzar aplicaciones desde una barra con iconos que se instala en nuestro escritorio. Para instalar AWN no necesitamos añadir repositorios adicionales, dado que se encuentra en los repositorios de nuestro sistema.

[bash] sudo apt-get install awn-manager [/bash]

una vez instalado accedemos al programa desde Aplicaciones &gt; Accesorios &gt; Avant Window Navigator podemos cambiar sus preferencias desde Sistema &gt; Preferencias &gt; Awn manager  para tener un dock similar al de Mac, puedes bajarte este tema para Awn:  <a href="http://rapidshare.com/files/71511920/Transparent.tgz.html">http://rapidshare.com/files/71511920/Transparent.tgz.html</a>
<ul>
	<li>Alternativa a AWN (gnome-do con docky)</li>
</ul>
[bash] sudo apt-get install gnome-do [/bash]

<sub>*Una vez instalado ejecutar, click en la pestaña y seleccionar preferencias, en el cuadro </sub>

<sub>de dialogo que se abre, ir a la pestaña de apariencia y en "theme" seleccionar docky</sub>
<ul>
	<li>Instalar Mplayer con todos los codecs y soporte de DVD</li>
</ul>
Si queremos reproducir peliculas con Mplayer ejecutamos:

[bash] sudo apt-get install mplayer [/bash]

Si hemos instalado los ubuntu restricted extra, seguramente ya tengamos muchos de estos paquetes instalados.
<ul>
	<li>Instalar Sun Java Runtime Environment</li>
</ul>
Si queremos instalar java para poder ejecutar aplicaciones basadas en Java o tener el plugin de Java para el navegador,  ejecutamos:

[bash] sudo apt-get install sun-java6-fonts sun-java6-jre sun-java6-plugin [/bash]
<ul>
	<li>Instalar Flash Player Plugin</li>
</ul>
Si queremos por ejemplo ver esos videos de Youtube desde firefox, tendremos que instalar el plugin de Flash, que nos permitira ver esos videos desde el navegador que estemos usando:  Para instalar el plugin oficial ejecutamos:

[bash] sudo apt-get install flashplugin-nonfree libflashsupport [/bash]

Si en cambio queremos instalar el Open Source:

[bash] sudo apt-get install mozilla-plugin-gnash [/bash]
<ul>
	<li> Instalar Microsoft fonts package</li>
</ul>
Si queremos utilizar algunas de las fuentes de texto de Microsoft como por ejemplo son:  *  Andale Mono  * Arial Black  * Arial (Bold, Italic, Bold Italic)  * Comic Sans MS (Bold)  * Courier New (Bold, Italic, Bold Italic)  * Georgia (Bold, Italic, Bold Italic)  * Impact  * Times New Roman (Bold, Italic, Bold Italic)  * Trebuchet (Bold, Italic, Bold Italic)  * Verdana (Bold, Italic, Bold Italic)  * Webdings  Ejecutamos:

[bash] sudo apt-get install msttcorefonts [/bash]

y despues

[bash] sudo fc-cache [/bash]

para reiniciar la cache de fuentes del sistema. a partir de ahora tenemos disponibles esas fuentes de texto para poder usarlas con nuestros programas favoritos.
<ul>
	<li>Instalar adobe reader</li>
</ul>
Para leer documentos PDF, si estamos mas acostumbrados a usar el Adobe reader,  y no queremos usar el visor interno del propio Gnome, podemos instalar este visor con:

[bash] sudo apt-get install acroread [/bash]
<ul>
	<li>Downloader For X</li>
</ul>
Downloader X es un interesante gestor de descargas, lo podemos instalar con:

[bash] sudo aptitude install d4x [/bash]
<ul>
	<li>aMSN</li>
</ul>
¿Tienes amigos con los que quieres hablar mediante el Msn?. Podras seguir conversando con ellos si instalas este cliente de mensajeria:

[bash] sudo apt-get install amsn [/bash]
<ul>
	<li><strong>Alternativa ligera a Amsn (emesene):</strong></li>
</ul>
[bash] sudo apt-get install emesene [/bash]
<ul>
	<li>amule, deluge-torrent</li>
</ul>
Emule, es uno de los programas P2P mas populares para descargar por internet y deluge es el mejor cliente torrent, que jamas e utilizado. Las versiones en Linux se instalan con:

[bash] sudo aptitude install amule deluge-torrent [/bash]
<ul>
	<li>reproducir videos, VLC</li>
</ul>
VideoLan VLC es uno de los mejores reproductores de video. Lo puedes instalar con, ademas esta version no origina ya cortes con Imagenio.

[bash] sudo apt-get install vlc [/bash]
<ul>
	<li>reproducir videos, Smplayer</li>
</ul>
Otra alternativa a VLC para visualizar videos:

[bash] sudo apt-get install smplayer [/bash]
<ul>
	<li><strong>Instala Exaile (buena alternativa a Amarok):</strong></li>
</ul>
[bash] sudo apt-get install exaile [/bash]
<ul>
	<li><strong>Controla la mayoria de aplicaciones de sonido con Music applet:</strong></li>
</ul>
[bash] sudo apt-get install music-applet [/bash]
<ul>
	<li>Apagar el altavoz interno del PC</li>
</ul>
si te molesta puedes desactivarlo desde Sistema &gt; Preferencias &gt; Sonido y en la pestaña que indica “Altavoz del Sistema” desactivas la opcion “Activar altavoz”

Otra forma de hacerlo es deshabilitar el demonio con el comando:

[bash] sudo modprobe -r pcspkr [/bash]

puede volver a activarse con:

[bash] sudo modprobe pcspkr [/bash]
<ul>
	<li>Que no se muestren las unidades en el escritorio</li>
</ul>
Si quieres que no te aparezcan los iconos con las particiones que tienes en tus discos puedes ocultar los iconos ejecutando:

[bash] gconf-editor [/bash]

se abrira el editor del registro. entocnes debes buscar la cadena “volumes_visible” en apps/nautilus/desktop Puedes activar o desactivar esta opcion para mostrar los iconos de tus volumnes.

* Eliminar kernels antiguos
Si has hecho una actualizacion, veras que al arrancar el PC en tu menu de grub aparecen las entradas antiguas. Puedes ver que version actual de kernel estas usando con el comando:

[bash] uname -r [/bash]

Anota el numero de version que sale y ojo… “no se te ocurra borrar este kernel”. El resto de kernels puedes eliminarlos desde synaptic, buscando por la cadena “linux-image-2? te aparecera una lista de todos los kernels que tienes instalados en tu sistema y ya podras seleccionar para “eliminar” aquellos que no quieras.
<ul>
	<li>Instalar wine</li>
</ul>
Si tienes alguna aplicacion para Windows que uses y no esta disponible para Linux, es posible que puedas ejecutarla con wine.

[bash] apt-get install wine [/bash]

una vez instalado, con el comando “winecfg” podras configurar las opciones de wine
<ul>
	<li>Personalizar las animaciones y efectos de Compiz</li>
</ul>
Si quieres poder seleccionar de manera sencilla que animaciones y efectos deseas activar en compiz nada mejor que instalar su administrador:

[bash] sudo apt-get install compizconfig-settings-manager emerald [/bash]

Entonces ya podremos acceder al administrador de Compiz desde: Sistema &gt; Preferencias &gt;Administrador de opciones de compiz-config y al gestor Emerald desde Sistema &gt; Preferencias &gt; Gestor de Temas de Emerald

Cuando hagas esto y si usas Compiz y usas Emerald como decorador de ventanas, es posible que los bordes se vean mal o que no te cargue  directamente Emerald cuando inicias sesion. Para solucionarlo vas a “Configuracion avanzada de efectos de escritorio” y en el plugin “Window Decoration”debemos cambiar el apartado “Command” por esta línea:

/usr/bin/emerald --replace
<ul>
	<li>De  todos modo la mejor opcion es instalar FUSION-ICON:</li>
</ul>
[bash] sudo apt-get install fusion-icon [/bash]

Despues lo ponemos en el inicio del sistema: SISTEMA &gt; PREFERENCIAS &gt; SESIONES .. pulsamos en AÑADIR, y agregamos por nombre y por comando:

fusion-icon

** Al iniciar el Sistema podremos controlar compiz y seleccionar el gestor de ventanas deseados desde el fusion-icon.
<ul>
	<li><strong>Gestiona el gestor de arranque (grub):</strong></li>
</ul>
[bash] sudo apt-get install startupmanager [/bash]
<ul>
	<li>Añadir mas temas de escritorio para tunear el sistema</li>
</ul>
[bash] sudo apt-get install community-themes [/bash]

Con esto tendremos disponibles un monton de temas guapos en las opciones de sistema &gt; apariencia de nuestro nuevo sistema.

Fuente: <a href="http://www.tuxapuntes.com/drupal/node/1646" target="_blank">TuxApuntes</a>

Espero les sirva
