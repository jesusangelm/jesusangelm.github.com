---
layout: post
title: !binary |-
  Q29zYXMgcXVlIGhhY2VyIGRlc3B1ZXMgZGUgaW5zdGFsYXIgVWJ1bnR1IDEw
  LjA0IEx1Y2lkIEx5bng=
tags:
- !binary |-
  YmxvZw==
- !binary |-
  Y29kZWM=
- !binary |-
  Z25vbWU=
- !binary |-
  Z29vZ2xl
- !binary |-
  Z3VpYQ==
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  amFtdW5peA==
- !binary |-
  amF2YQ==
- !binary |-
  a2FybWlj
- !binary |-
  bGlicmU=
- !binary |-
  bGludXg=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  c29mdHdhcmU=
- !binary |-
  dWJ1bnR1
- !binary |-
  dmVuZXp1ZWxh
- !binary |-
  d2luZG93cw==
- !binary |-
  dmlzdGE=
- !binary |-
  bWJy
- !binary |-
  Y29ua3k=
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  YXVkaW8=
- !binary |-
  cGFuZWw=
- !binary |-
  bHVjaWQ=
- !binary |-
  bHlueA==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  bWF5bw==
- !binary |-
  YmFy
- !binary |-
  dmxj
- !binary |-
  cmVwcm9kdWN0b3I=
- !binary |-
  dmlkZW8=
- !binary |-
  b3BlcmE=
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  d2Vi
- !binary |-
  cmVsZWFzZQ==
- !binary |-
  Y29tYW5kb3M=
- !binary |-
  dGVybWluYWw=
- !binary |-
  Z3VpYXM=
- !binary |-
  bGFwdG9w
---
Este post puede que llegue algo tarde, ya que hace unas cuantas semanas que salio Ubuntu 10.04. El dia del lanzamiento de Lucid Lynx y luego de instalarlo en mi laptop, una de las primeras cosas que hice fue buscar los tipicos "Cosas que hacer despues de instalar ......." para Lucid, pero ese dia me sorprendi con que en la mayoria de los sitios que frecuento habian publicado Scripts de instalacion de aplicaciones de manera automatizada y no los pasos para instalar y configurar las aplicaciones que mas se usan o las mas populares.

Bien no tengo nada en contra con estos Script pero no me llamo mucho la atencion ni me convencieron ya que estos pueden instalar aplicaciones que uno la verdad no necesite o use, por lo que por lo menos en mi caso (que mi internet no es ilimitado) no me serviria ya que gastaria Mb o Gb de descargas de datos en algo que no me interesa.  Luego de ver tantos script repartidos por la web decidi crear mi propio "Cosas que hacer despues de instalar ......."  orientandome en los pocas guias que encontre  en la web y basandome en las aplicaciones que yo mas uso y las que mas se usan en Linux.

Asi que sin mas, esto es: Algunas cosas que hago despues de instalar Ubuntu 10.04

- Muchos de los anteriores "Cosas que hacer despues de instalar ......." recomendaban cambiar  los servidores de descargas de software por uno que este destinado a el pais en el que te encuentres (en mi caso Venezuela) pero luego de unas cuantas instalaciones de Ubuntu me e dado cuenta de que estos se configuran automaticamente en la instalacion, ya que cuando inicio Ubuntu por primera vez y reviso la lista de repos me aparecen ya los ve.archive.ubuntu.com por lo que esto imagino que ya no es necesario hacerlo. De todos modos si en tu caso no estan  configurados a los servidores asignados a tu pais Existe una opcion de Synaptic, que nos permite seleccionar un servidor  mas cercano a nuestra region. Para cambiar este servidor a uno mas  cercano vamos a Sistema &gt; Administracion &gt; Origenes de software y  en la pestaña “Software de Ubuntu”, seleccionamos “descargar desde:”  indicando la region mas cercanaa la nuestra.

- Algo que e visto que se no se escribe en los "Cosas que hacer despues de instalar ......." es que no mencionan que actualicen la lista de repos antes de instalar algo, es decir teclear:

[bash] sudo apt-get update [/bash]

para asi actualizar cualquier posible nuevo paquete añadido a la los servidores y asegurarnos de que instalaresmos los paquetes mas recientes y estables.

- Otra cosa que deberiamos hacer antes de instalar algo y que por cierto deberiamos hacer antes del comando anterior es la de activar los repositorios Restricted y Multiverse en caso de no estar habilitados. esto lo hacemos abriendo Synaptic, luego click en Configuracion y luego en Repositorios. en la pestaña que dice: Software de Ubuntu marcamos las primeras 4 casillas pertenecientes a los repositorios Main, Universe Restricted y Multiverse respectivamente. Luego de esto cerramos y en una terminal tecleamos el comando anterior para que se actualicen el listado de paquetes.

-  Bien una de las cosas que se recomienda tambien hacer de primero es instalar los paquetes basicos de compilacion, esto es porque si queremos compilar algun paquete del que solo tenemos el codigo  fuente, tendremos que instalar los paquetes
basicos de compilacion. Lo instalamos con:

[bash] sudo apt-get install build-essential [/bash]

- Agregar repositorios Medibuntu:  <a href="http://medibuntu.org/" target="_blank">Mediubuntu</a> es un repositorio donde podemos encontrar algunas  aplicaciones y codecs que no son instalador por defecto. Podemos  añadirlo a la lista de repositorios ejecutando, desde una terminal:

[bash] sudo wget --output-document=/etc/apt/sources.list.d/medibuntu.list http://www.medibuntu.org/sources.list.d/$(lsb_release -cs).list &amp;&amp; sudo apt-get --quiet update &amp;&amp; sudo apt-get --yes --quiet --allow-unauthenticated install medibuntu-keyring &amp;&amp; sudo apt-get --quiet update [/bash]

Este repositorio te permitira instalar aplicaciones tales como el lector de PDF Adobe Reader para Linux, Codecs de audio y video  de formatos conocidos como los MP3 y WMV, y reproductores como el RealPlayer

- Instalar Codecs : Bien aqui le comenzamos a sacar provecho al repositorio recien agregado ya que con el siguiente comando

[bash] sudo apt-get install non-free-codecs [/bash]

instalamos los codec no libres  para reproducir formatos de audio y video privativos.

- Soporte para reproducir DVD: con este comando instalamos  el paquete que nos permite reproducir DVD encriptados con CSS

[bash] sudo apt-get install libdvdread4 [/bash]

Luego de esto debemos teclear:

[bash] sudo /usr/share/doc/libdvdread4/install-css.sh [/bash]

-  Intalar el reproductor VLC:  Para instalar este genial reproductor tecleamos en la terminal

[bash] sudo apt-get install vlc [/bash]

VLC es mi reproductor de video favorito y el unico que instalo en Linux, pero si prefieres otro puedes instalar tambien:

Mplayer

[bash] sudo apt-get install mplayer [/bash]

SMPlayer

[bash] sudo apt-get install smplayer [/bash]

<code><strong> </strong><strong> </strong><strong>
</strong></code>

- Instalar Ubuntu Tweak:  Ubuntu Tweak es una aplicacion que nos permite configurar  a gusto y de manera muy sencilla nuestro Ubuntu, ademas de ayudarnos a instalar unas cuantas aplicaciones sin necesidad de estar agregando repositorios o teclear comandos en la terminal por lo que es muy conveniente para nosotros si es una de nuestras primeras instalaciones. Para descargarlo tan solo debemos ir a la pagina oficial en www.ubuntu-tweak.com y hacer click en el enlace de descarga para bajar el .deb una vez descargado le damos dobleclick al mismo para instalar la aplicacion.

Otra aplicacion similar a Ubuntu Tweak  a tener en cuenta es Ailurus el cual podemos instalar agregando el siguiente repositorio tecleando en la terminal:

[bash] sudo add-apt-repository ppa:ailurus [/bash]

luego de esto actualizamos el listado de paquetes... ya a estas alturas deberias saber con que comando pero bueh aqui te va por si no lo recuerdas:

[bash] sudo apt-get update [/bash]

y luego instalamos Ailurus tecleando:

[bash] sudo apt-get install ailurus [/bash]

puedes instalar los dos y asi decides tu mismo cual satisface mejor tus necesidades o cual te gusta mas... yo me voy por Ubuntu Tweak aunque tambien tengo Ailurus :D

- Instalar el navegador Chromium: Chromium es el navegador Libre en el que se basa Google para desarrollas su navegador Google Chrome el cual es Privativo, a simple vista no hay diferencias ya que son identicos pero en cuanto a codigo si hay diferencias ya que Chromium es libre y Chrome no lo es, ademas  hace poco se conocio una noticia que afirmaba que Google Chrome nos registraba el historial de navegacion y esa informacion al parecer era utilizada por google, asi que tambien por privacidad es conveniente instalar Chromium en vez de Chrome, para hacerlo tan solo tecleamos en la terminal:

[bash] sudo apt-get install chromium-browser [/bash]

- Instalar el navegador Opera: Este navegador me gusta mucho ya que me permite navegar en paginas WAP ademas de las Web, para instalarlo tan solo debemos ir a la pagina de Opera y descargar el paquete .Deb haciendo click <a href="http://www.opera.com/browser/download/" target="_blank">Aqui</a>

- Instalar el editor GIMP:  Desde Ubuntu 10.04 en adelante ya no viene por defecto el programa de edicion de imagenes Gimp, una lastima! pero no hay de que preocuparse ya que podemos instalarlo tecleando en la terminal:

[bash] sudo apt-get install gimp [/bash]

- Instalar VirtualBox:  Eh probado muchas aplicaciones de virtualizacion de maquinas tanto en Linux como en Windows y en los dos S.O me e quedado con la mejor VirtualBox !!!  solo espero que Oracle no la vaya a cagar y tenga que buscarle remplazo. con esta aplicacion podremos crear maquinas virtuales de otros S.O dentro de nuestro Ubuntu, muy util si queremos probar otra distro y no queremos matarnos con un dualboot o eliminar S.O que tengamos ya instalados.  Para instalarla tan dolo debemos ir a la web oficial y descargarnos el .Deb haciendo <a href="http://www.virtualbox.org/wiki/Linux_Downloads" target="_blank">click aqui.</a>

ya sabes luego de descargar le damos doble click al archivo .deb y se instalara automaticamente (puede que te pida dependencias asi que asegurate de estar conectado a internet cuando lo hagas).

- Instalar Pidgin:  Esta es uno de mis clientes favoritos de MI ( Mensajeria Instantanea ) ironicamente lo conoci primero en Windows antes que Linux gracias a PortableApps.  Para instalarlo tan solo debemos teclear en la terminal:

[bash] sudo apt-get install pidgin [/bash]

- Instalar Java:  bien este lenguaje y su JRE puede que sea necesario para ciertas aplicaciones y paginas web, asi que conviene tenerlo instalado, para hacerlo basta con teclear en la terminal

[bash] sudo apt-get install sun-java6-jre sun-java6-plugin sun-java6-fonts [/bash]

- Instalar Conky: Conky es una muy buena aplicacion que permite mostrar en una especie de panel lateral casi cualquier informacion de tu PC, yo lo defino mas bien como un hibrido entre panel lateral y Widget :D

A esta hora de la madrugada ya me da ladilla teclear comandos asi que para instalar tan solo deben visitar Blog.Jam.Net.Ve  jejejejeje porque ya tengo un post explicando como instalarlo, tan solo has <a href="http://blog.jam.net.ve/2009/12/21/instalando-conky-en-ubuntu-karmic/" target="_blank">click Aqui</a>.   En el post se explica la instalacion en Ubuntu Karmic pero tambien funciona a la perfeccion para Lucid.

- Restaurar la posicion de los botones de las ventanas: Uno de los cambios muy criticado que se hizo en Lucid es el cambio de los botones de Maximizar, Minimizar y Cerrar al lado Izquierdo de las ventanas similar al S.O Mac. porque han hecho esto? Ni idea :S intente acostumbrarme pero a la hora ya me estaba molestando demasiado el cambio.  Una de las maneras mas sencillas que encontre para volver a colocar los botones al lado derecho de la ventana es con la aplicacion Ailurus que ya deberias de haber instalado, aunque tambien puede hacerse con Ubuntu Tweak.

* Para hacer el cambio con Ailurus: abres la aplicacion, luego click en el icono "Sistema Configuraciones" y luego en " Efecto de Ventanas" en la parte de abajo donde dice "Presentacion de los botones de la barra de titulos" de seguro aparecera "MAC OS X" Cambialo a "GNOME Clasico" y listo. resuelto el problema.

* Para hacerlo con Ubuntu Tweak: Abres la aplicacion y has click en el lado izquierdo donde dice "Configuracion del gestor de ventanas"  ahora en donde dice "Formato de botones en la barra de titulos de la ventana"   marca la opcion "Derecho"  y listo!

Bien esto es todo, no es un listado de centenares de aplicaciones como otros "cosas que hacer despues de instalar ....."  ya que como dije es basado en las aplicaciones que mas uso o las mas populares, pero si quieren instalar otras aplicaciones basta con abrir Ubuntu Tweak o Ailurus y agregar Repos e instalar desde alli y de manera automatizada y facil las aplicaciones que deseas que para eso se instalaron :D   ahh  otra cosa, no se olviden de Synaptic... no es un Ubuntu Tweak o Ailurus pero si tiene muchas mas aplicaciones que estos dos jajajajaja.

Saludos y espero les sirva.
