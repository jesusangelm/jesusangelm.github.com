---
layout: post
title: !binary |-
  Q29zYXMgYSBoYWNlciBkZXNwdWVzIGRlIGluc3RhbGFyIFVidW50dSA5LjA0
  IEphdW50eSBKYWNrYWxvcGU=
tags:
- !binary |-
  YmFt
- !binary |-
  Y29kZWM=
- !binary |-
  Z25vbWU=
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  amFja2Fsb3Bl
- !binary |-
  amF1bnR5
- !binary |-
  amF2YQ==
- !binary |-
  bGludXg=
- !binary |-
  bXVsdGltZWRpYQ==
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  cmVjb21lbmRhY2lvbg==
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
  Y2FjaGU=
- !binary |-
  aW1wb3J0YXI=
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
- !binary |-
  ZG9jaw==
- !binary |-
  eW91dHViZQ==
---
Bueno hay una web sobre linux que me gusta mucho y cada vez que sacan una nueva distro ubuntu ellos colocan una serie de pasos e instalaciones recomendables para hacer juste despues de instalar Ubuntu.  Con la reciente salida de Ubuntu 9.04 Jaunty Jackalope aqui les dejo las recomendaciones que ellos dan:
<ul>
	<li><strong>Instalar software mas rapidamente.</strong></li>
</ul>
Suele ocurrir (y especialmente) cuando sale una nueva version de Ubuntu, que los repositorios desde los cuales nos solemos descargar software estan muy saturados. Si queremos descargar e instalar el software mas rapidamente, tendremos que modificar la lista de repositorios.

Existe una opcion de Synaptic, que nos permite seleccionar un servidor mas cercano a nuestra region. Para cambiar este servidor a uno mas cercano vamos a <strong>Sistema &gt; Administracion &gt; Origenes de software </strong>y en la pestaña “Software de Ubuntu”, seleccionamos “descargar desde:” indicando la region mas cercanaa la nuestra.
<ul>
	<li><strong>Instalar el software basico de compilacion</strong></li>
</ul>
Si queremos compilar algun paquete del que solo tenemos el codigo fuente, tendremos que instalar los paquetes
basicos de compilacion. Lo instalamos con:
<pre>sudo aptitude install build-essential</pre>
<ul>
	<li><strong>Instalar los extra restrictivos.</strong></li>
</ul>
Hay ciertos paquetes que no vienen por defecto en Ubuntu por cuestiones legales. Cuando se instala ubuntu, por defecto y debido a un tema de licencias no instala todo ese software comercial que no ha liberado el codigo fuente, como por ejemplo puede ser el plugin de flash, o los codecs para poder reproducir algunos formatos de video. Existe un metapaquete (un paquete que agrupa e instala muchos mas paquetes) llamado ubuntu-restricted-extras que nos permiteinstalar todo este software que no es instalado por defecto.

Tras habilitar los repositorios universe y multiverse podemos instalar este metapaquete con:
<pre>sudo apt-get install ubuntu-restricted-extras</pre>
<ul>
	<li><strong>Otra opcion es añadir el repositorio mediubuntu para Intrepid Ibex </strong></li>
</ul>
Mediubuntu es un repositorio donde podemos encontrar algunas aplicaciones y codecs que no son instalador por defecto. Podemos añadirlo a la lista de repositorios ejecutando, desde una terminal:
<p style="padding-left: 30px;"><code>sudo wget <a title="http://www.medibuntu.org/sources.list.d/jaunty.list" href="http://www.medibuntu.org/sources.list.d/jaunty.list">http://www.medibuntu.org/sources.list.d/jaunty.list</a> --output-document=/etc/apt/sources.list.d/medibuntu.list</code></p>

y despues
<blockquote><code>sudo apt-get update &amp;&amp; sudo apt-get install medibuntu-keyring &amp;&amp; sudo apt-get update</code></blockquote>
<ul>
	<li><strong>Instalamos Codecs Multimedia DVD</strong></li>
</ul>
<pre><code>sudo apt-get install libdvdread3</code></pre>
<em><strong>Segun nuestra plataforma, instalamos CODECS: </strong></em>
<ul>
	<li>
<p class="line862">For <strong>i386</strong>, the package is called <strong>w32codecs</strong>:</p>

<pre>sudo apt-get install w32codecs</pre>
</li>
	<li class="gap">
<p class="line862">For <strong>amd64</strong>, the package is called <strong>w64codecs</strong>:</p>

<pre>sudo apt-get install w64codecs</pre>
</li>
	<li class="gap">
<p class="line862">For <strong>ppc</strong>, the package is called <strong>ppc-codecs</strong>:</p>

<pre>sudo apt-get install ppc-codecs</pre>
</li>
</ul>
<strong>* Instalar Avant Window Navigator</strong>
AWN es un dock similar al de Mac, que nos permite lanzar aplicaciones desde una barra con iconos que se instala en nuestro escritorio. Para instalar AWN no necesitamos añadir repositorios adicionales, dado que se encuentra en los repositorios de nuestro sistema.
<pre> sudo apt-get install awn-manager-trunk awn-extras-applets-trunk</pre>
una vez instalado accedemos al programa desde <strong>Aplicaciones &gt; Accesorios &gt; Avant Window Navigator</strong> podemos cambiar sus preferencias desde <strong>Sistema &gt; Preferencias &gt; Awn manager</strong>

para tener un dock similar al de Mac, puedes bajarte este tema para Awn:

<a href="http://rapidshare.com/files/71511920/Transparent.tgz.html">http://rapidshare.com/files/71511920/Transparent.tgz.html</a>
<ul>
	<li><strong>Instalar <span class="entry-title-link">OpenOffice.org 3.0</span></strong></li>
</ul>
Lo primero que tendremos que hacer es añadir el repositorio correspondiente a sources.list yendo a Sistema -&gt; Administración -&gt; Orígenes de software -&gt; Software de terceros -&gt; Añadir, e introduciendo la línea
<blockquote>deb <a title="http://ppa.launchpad.net/openoffice-pkgs/ubuntu" href="http://ppa.launchpad.net/openoffice-pkgs/ubuntu">http://ppa.launchpad.net/openoffice-pkgs/ubuntu</a> jaunty main
deb-src <a title="http://ppa.launchpad.net/openoffice-pkgs/ubuntu" href="http://ppa.launchpad.net/openoffice-pkgs/ubuntu">http://ppa.launchpad.net/openoffice-pkgs/ubuntu</a> jaunty main</blockquote>
La clave publica la descargamos de:<span> <a href="http://news.softpedia.com/images/extra/LINUX/small/key" target="_blank"><strong>HERE</strong></a> , le damos a guardar como y la ponemos en el escritorio, luego desde claces le damos a importar y la seleccionamos,</span>

Pulsamos Cerrar y se nos preguntará si queremos actualizar la lista de los paquetes disponibles. Pulsamos sobre el botón Recargar y esperamos a que se termine de actualizar la lista.

Una vez hecho esto el sistema detectará que existe una versión más actual de OpenOffice.org (la 3.0) disponible en el repositorio que acabamos de añadir, y se mostrará el icono de Actualizaciones en la barra de tareas. Hacemos clic sobre el icono y seleccionamos "Instalar actualizaciones".
<ul>
	<li><strong>Instalar Mplayer con todos los codecs y soporte de DVD</strong></li>
</ul>
Si queremos reproducir peliculas con Mplayer ejecutamos:
<pre>sudo apt-get install mplayer</pre>
Si hemos instalado los ubuntu restricted extra, seguramente ya tengamos muchos de estos paquetes instalados.
<ul>
	<li><strong>Instalar Sun Java Runtime Environment</strong></li>
</ul>
Si queremos instalar java para poder ejecutar aplicaciones basadas en Java o tener el plugin de Java para el navegador,
ejecutamos:
<pre>sudo apt-get install sun-java6-fonts sun-java6-jre sun-java6-plugin</pre>
<ul>
	<li><strong>Instalar Flash Player Plugin</strong></li>
</ul>
Si queremos por ejemplo ver esos videos de Youtube desde firefox, tendremos que instalar el plugin de Flash, que nos permitira ver esos videos desde el navegador que estemos usando:

Para instalar el plugin oficial ejecutamos:
<pre>sudo apt-get install flashplugin-nonfree libflashsupport</pre>
Si en cambio queremos instalar el Open Source:
<pre>sudo apt-get install mozilla-plugin-gnash</pre>
<ul>
	<li><strong> Instalar Microsoft fonts package</strong></li>
</ul>
Si queremos utilizar algunas de las fuentes de texto de Microsoft como por ejemplo son:

*  Andale Mono
* Arial Black
* Arial (Bold, Italic, Bold Italic)
* Comic Sans MS (Bold)
* Courier New (Bold, Italic, Bold Italic)
* Georgia (Bold, Italic, Bold Italic)
* Impact
* Times New Roman (Bold, Italic, Bold Italic)
* Trebuchet (Bold, Italic, Bold Italic)
* Verdana (Bold, Italic, Bold Italic)
* Webdings

Ejecutamos:
<pre>sudo apt-get install msttcorefonts</pre>
y despues
<pre> sudo fc-cache</pre>
para reiniciar la cache de fuentes del sistema. a partir de ahora tenemos disponibles esas fuentes de texto para poder usarlas con nuestros programas favoritos.
<ul>
	<li><strong>Instalar adobe reader</strong></li>
</ul>
Para leer documentos PDF, si estamos mas acostumbrados a usar el Adobe reader,
y no queremos usar el visor interno del propio Gnome, podemos instalar este visor con:
<pre>sudo apt-get install acroread</pre>
<ul>
	<li><strong>Downloader For X</strong></li>
</ul>
Downloader X es un interesante gestor de descargas, lo podemos instalar con:
<pre>sudo aptitude install d4x</pre>
<ul>
	<li><strong>aMSN</strong></li>
</ul>
¿Tienes amigos con los que quieres hablar mediante el Msn?. Podras seguir conversando con ellos si instalas este cliente de mensajeria:
<pre>sudo apt-get install amsn</pre>
<ul>
	<li><strong>amule, deluge-torrent
</strong></li>
</ul>
Emule, es uno de los programas P2P mas populares para descargar por internet y deluge es el mejor cliente torrent, que jamas e utilizado. Las versiones en Linux se instalan con:
<pre>sudo aptitude install amule deluge-torrent</pre>
<ul>
	<li><strong>reproducir videos, VLC</strong></li>
</ul>
VideoLan VLC es uno de los mejores reproductores de video. Lo puedes instalar con, ademas <em><strong><span style="text-decoration: underline;">esta version no origina ya cortes con Imagenio</span>.</strong></em>
<pre>sudo apt-get install vlc</pre>
<ul>
	<li><strong>reproducir videos, Smplayer</strong></li>
</ul>
Otra alternativa a VLC para visualizar videos:
<pre>sudo apt-get install smplayer</pre>
<ul>
	<li><strong>Apagar el altavoz interno del PC</strong></li>
</ul>
si te molesta puedes desactivarlo desde Sistema &gt; Preferencias &gt; Sonido y en la pestaña que indica “Altavoz del Sistema” desactivas la opcion “Activar altavoz”

Otra forma de hacerlo es deshabilitar el demonio con el comando:
<pre>sudo modprobe -r pcspkr</pre>
puede volver a activarse con:
<pre>sudo modprobe pcspkr</pre>
<ul>
	<li><strong>Que no se muestren las unidades en el escritorio</strong></li>
</ul>
Si quieres que no te aparezcan los iconos con las particiones que tienes en tus discos puedes ocultar los iconos ejecutando:
<pre>gconf-editor</pre>
se abrira el editor del registro. entocnes debes buscar la cadena “<strong>volumes_visible</strong>” en <strong>apps/nautilus/desktop</strong> Puedes activar o desactivar esta opcion para mostrar los iconos de tus volumnes.

<strong>* Eliminar kernels antiguos</strong>
Si has hecho una actualizacion, veras que al arrancar el PC en tu menu de grub aparecen las entradas antiguas. Puedes ver que version actual de kernel estas usando con el comando:
<pre> uname -r</pre>
Anota el numero de version que sale y ojo… “no se te ocurra borrar este kernel”. El resto de kernels puedes eliminarlos desde synaptic, buscando por la cadena “linux-image-2? te aparecera una lista de todos los kernels que tienes instalados en tu sistema y ya podras seleccionar para “eliminar” aquellos que no quieras.
<ul>
	<li><strong>Instalar wine</strong></li>
</ul>
Si tienes alguna aplicacion para Windows que uses y no esta disponible para Linux, es posible que puedas ejecutarla con wine.
<pre>  apt-get install wine</pre>
una vez instalado, con el comando “winecfg” podras configurar las opciones de wine
<ul>
	<li><strong>Personalizar las animaciones y efectos de Compiz</strong></li>
</ul>
Si quieres poder seleccionar de manera sencilla que animaciones y efectos deseas activar en compiz nada mejor que instalar su administrador:
<pre>$ sudo apt-get install compizconfig-settings-manager emerald</pre>
Entonces ya podremos acceder al administrador de Compiz desde: <strong>Sistema &gt; Preferencias &gt;Administrador de opciones de compiz-config</strong> y al gestor Emerald desde <strong>Sistema &gt; Preferencias &gt; Gestor de Temas de Emerald</strong>

Cuando hagas esto y si usas Compiz y usas Emerald como decorador de ventanas, es posible que los bordes se vean mal o que no te cargue  directamente Emerald cuando inicias sesion. Para solucionarlo vas a “Configuracion avanzada de efectos de escritorio” y en el plugin “Window Decoration”debemos cambiar el apartado “Command” por esta línea:
<blockquote>/usr/bin/emerald --replace</blockquote>
<ul>
	<li>De  todos modo la mejor opcion es<strong> instalar FUSION-ICON</strong>:</li>
</ul>
<pre>sudo apt-get install fusion-icon</pre>
Despues lo ponemos en el inicio del sistema:<strong> SISTEMA &gt; PREFERENCIAS &gt; SESIONES</strong> .. pulsamos en AÑADIR, y agregamos por nombre y por comando:
<blockquote>fusion-icon</blockquote>
** Al iniciar el Sistema podremos controlar compiz y seleccionar el gestor de ventanas deseados desde el fusion-icon.
<ul>
	<li><strong>Añadir mas temas de escritorio para tunear el sistema</strong></li>
</ul>
<pre>sudo apt-get install community-themes</pre>
Con esto tendremos disponibles un monton de temas guapos en las opciones de <em><strong>sistema &gt; apariencia</strong></em> de nuestro nuevo sistema.

Fuente: <a href="http://www.tuxapuntes.com/drupal/?q=node/1319" target="_blank">www.tuxapuntes.com</a>

Autor en Fuente: <em><strong><span class="submitted">utopianegra </span></strong></em>
