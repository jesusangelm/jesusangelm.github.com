---
layout: post
title: !binary |-
  Q29zYXMgcXVlIGhhZ28gZGVzcHVlcyBkZSBpbnN0YWxhciBVYnVudHUgMTAu
  MTAgTWF2ZXJpY2sgTWVlcmthdA==
tags:
- !binary |-
  Y29kZWM=
- !binary |-
  Y29ycmVv
- !binary |-
  ZHJpdmVycw==
- !binary |-
  ZXZvbHV0aW9u
- !binary |-
  Z2FkZ2V0
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
  bGlicmU=
- !binary |-
  bGludXg=
- !binary |-
  bW9kZW0=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  cGx1Z2lucw==
- !binary |-
  cmVjb21lbmRhY2lvbg==
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  c29mdHdhcmU=
- !binary |-
  dHV0b3JpYWw=
- !binary |-
  dWJ1bnR1
- !binary |-
  dW5peA==
- !binary |-
  dXNi
- !binary |-
  dmVuZXp1ZWxh
- !binary |-
  d2luZG93cw==
- !binary |-
  YmV0YQ==
- !binary |-
  bWFudWFs
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
  b3BlcmE=
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  Y2FjaGU=
- !binary |-
  ZG5z
- !binary |-
  ZG5zbWFzcQ==
- !binary |-
  Y2hhdA==
- !binary |-
  bWF2ZXJpY2s=
- !binary |-
  d2Vi
- !binary |-
  cmVsZWFzZQ==
- !binary |-
  dGVybWluYWw=
- !binary |-
  YXJjaGl2b3M=
- !binary |-
  c2lzdGVtYXM=
---
Bien hace menos de una semana salio la nueva version de Ubuntu 10.10 Maverick Meerkat la cual viene con unas cuantas mejoras aunque no se notan a simple vista, y alguna que otras decepciones como la ausencia de los windicators.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/10/suricato-yupi-ubuntu.jpg"><img class="aligncenter size-medium wp-image-434" title="suricato-yupi-ubuntu" src="http://blog.jam.net.ve/imagenes/uploads/2010/10/suricato-yupi-ubuntu-199x300.jpg" alt="" width="199" height="300" /></a>

Como les comente hace 6 meses en mi anterior <a href="http://blog.jam.net.ve/2010/05/19/cosas-que-hacer-despues-de-instalar-ubuntu-10-04-lucid-lynx/">Cosas que hacer despues de instalar Ubuntu </a>no recomiendo el uso de los script de instalacion que estan en algunas webs ya que es probable que estos te instalen aplicaciones que no necesitas o no usas por lo que perderas tu tiempo, espacio en disco y ancho de banda en tu conexion.

Asi que sin mas, esto es: Algunas cosas que hago despues de instalar Ubuntu 10.10 a lo JamUnix :D

Bien como usuario de Modem USB una de las primeras cosas que yo tenia que hacer era instalar usb_modeswitch y ponerme a configurar para que Ubuntu lo reconociera y luego configurar la conexion, pero una de las mejoras que se agradece en Ubuntu 10.10 Maverick es que usb_modeswitch viene instalado por defecto y por lo tanto ya solo basta conectar el modem y el mismo Ubuntu se encargara de reconocerlo como lo que en realidad es: Un "Modem USB"  y no como unidad de almacenamiento. Otra cosa que se agradece es la inclusion de las otras dos operadoras GSM de Venezuela ya que anteriormente solo estaba una en la lista de proveedores de internet.

- Muchos de los anteriores “Cosas que hacer despues de instalar …….”  recomendaban cambiar  los servidores de descargas de software por uno  que este destinado a el pais en el que te encuentres (en mi caso  Venezuela) pero luego de unas cuantas instalaciones de Ubuntu me e dado  cuenta de que estos se configuran automaticamente en la instalacion, ya  que cuando inicio Ubuntu por primera vez y reviso la lista de repos me  aparecen ya los ve.archive.ubuntu.com por lo que esto imagino que ya no  es necesario hacerlo. De todos modos si en tu caso no estan   configurados a los servidores asignados a tu pais Existe una opcion de  Synaptic, que nos permite seleccionar un servidor  mas cercano a nuestra  region. Para cambiar este servidor a uno mas  cercano vamos a Sistema  &gt; Administracion &gt; Origenes de software y  en la pestaña “Software  de Ubuntu”, seleccionamos “descargar desde:”  indicando la region mas  cercanaa la nuestra.

- Algo que e visto que se no se escribe en los “Cosas que hacer  despues de instalar …….” es que no mencionan que actualicen la lista de  repos antes de instalar algo, es decir teclear:
<pre lang="bash" line="1" escaped="true">sudo apt-get update</pre>
para asi actualizar cualquier posible nuevo paquete añadido a la los  servidores y asegurarnos de que instalaresmos los paquetes mas recientes  y estables.

- En el anterior manual les decia que una de las cosas que habia que hacer es activar los repositorios Restricted y Multiverse pero en Ubuntu 10.10 ya esto no es necesario ya que vienen activado por defecto.

-  Bien una de las cosas que se recomienda tambien hacer de primero es  instalar los paquetes basicos de compilacion, esto es porque si queremos  compilar algun paquete del que solo tenemos el codigo  fuente,  tendremos que instalar los paquetes
basicos de compilacion. Lo instalamos con:
<pre lang="bash" line="1" escaped="true">sudo apt-get install build-essential</pre>
<strong>- Agregar repositorios Medibuntu:</strong> <a href="http://medibuntu.org/" target="_blank">Mediubuntu</a> es un repositorio donde podemos encontrar algunas  aplicaciones y  codecs que no son instalador por defecto. Podemos  añadirlo a la lista  de repositorios ejecutando, desde una terminal:
<pre lang="bash" line="1" escaped="true">sudo wget --output-document=/etc/apt/sources.list.d/medibuntu.list http://www.medibuntu.org/sources.list.d/$(lsb_release -cs).list &amp;&amp; sudo apt-get --quiet update &amp;&amp; sudo apt-get --yes --quiet --allow-unauthenticated install medibuntu-keyring &amp;&amp; sudo apt-get --quiet update</pre>
Este repositorio te permitira instalar aplicaciones tales como el  lector de PDF Adobe Reader para Linux, Codecs de audio y video  de  formatos conocidos como los MP3 y WMV, y reproductores como el  RealPlayer

<strong>- Instalar Codecs : </strong>Bien aqui le comenzamos a sacar provecho al repositorio recien agregado ya que con el siguiente comandoinstalamos los codec no libres  para reproducir formatos de audio y video privativos.
<pre lang="bash" line="1" escaped="true">sudo apt-get install non-free-codecs</pre>
<strong>- Soporte para reproducir DVD: </strong>con este comando instalamos  el paquete que nos permitereproducir DVD encriptados con CSS
<pre lang="bash" line="1" escaped="true">sudo apt-get install libdvdread4</pre>
Luego debemos telclear:
<pre lang="bash" line="1" escaped="true">sudo /usr/share/doc/libdvdread4/install-css.sh</pre>
<strong>- Instalar principales Reproductores de video:</strong>

<strong>
<pre lang="bash" line="1" escaped="true">sudo apt-get install vlc</pre>
</strong>

&nbsp;
<pre lang="bash" line="1" escaped="true">sudo apt-get install mplayer</pre>
<pre lang="bash" line="1" escaped="true">sudo apt-get install smplayer</pre>
Bien ya a este nivel ya deberias tener los drivers graficos instalado y si no de seguro Ubuntu deberia estarte diciendo como instalarlo asi que entra en Sistemas &gt; Administracion &gt; Controladores Adicionales.   Elije los controladores que te aparescan y dale a "Activar" para que comience la descarga e instalacion.

<strong>- Aptitude: </strong>desde una o dos versiones atras en Ubuntu ya no esta viniendo este reconocido gestor de paquetes famoso por resolver muy bien las dependencias tanto en la instalacion como en la desinstalacion de paquetes, para instalarlo tan solo:
<pre lang="bash" line="1" escaped="true">sudo apt-get install aptitude</pre>
A pesar de que muchos novatos no usan este gestor de paquetes es recomendable probarlo asi que a partir de aqui en adelante todas las instalaciones en la terminal se harán usando este gestor :-P

<strong>- Compiz:</strong> para obtener esos bonitos efectos de escritorio re requiere instalar compiz, pero desde hace unas cuantas versiones atras el ya viene instalado por lo que para configurar y personalizar solo debemos instalar fusion-icon y compizconfig-settings-manager:
<pre lang="bash" line="1" escaped="true">sudo aptitude install compizconfig-settings-manager fusion-icon</pre>
<strong>- Gimp: </strong>el popular editor grafico no esta instalado por defecto desde Ubuntu 10.04 pero siempre podemos instalarlo con:
<pre lang="bash" line="1" escaped="true">sudo aptitude install gimp</pre>
<strong>- Inkscape:</strong> Si usas Gimp de seguro terminaras por usar o por lo menos probar una vez Inkscape para realizar imagenes vectoriales o editar algun .SVG
<pre lang="bash" line="1" escaped="true">sudo aptitude install inkscape</pre>
<strong>- Firestarter:</strong> este es una interfaz grafica para Iptables, es muy util instalar ya que asi tendras una interfaz sencilla "A prueba de tontos" :D para configurar tu cortafuego y navegar mas seguro.
<pre lang="bash" line="1" escaped="true">sudo aptitude install firestarter</pre>
<strong>- Xchat:</strong> uno de los mas populares clientes IRC para Linux, con el podras estar comunicado con toda la comunidad Linux y Ubuntu por medio de cualquier servidor IRC.
<pre lang="bash" line="1" escaped="true">sudo aptitude install xchat</pre>
<strong>- Thunderbird:</strong> Lo considero el mejor cliente de correos para Linux y Windows (no me gusta Evolution) con el podras configurar todas tus cuentas de correo, facil y sencillo.
<pre lang="bash" line="1" escaped="true">sudo aptitude install thunderbird</pre>
si por casualidad al abrirlo te sale en ingles teclea en la terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install thunderbird-locale-es-es</pre>
<strong>- Gdebi: </strong>a partir de de Ubuntu 10.10 los paquetes .Deb que descargues manualmente se instalan con el nuevo y mejorado "Centro de Software" al darle doble click, pero en mis experiencias prefiero usar Gdebi ya que este es mas liviano y se abre mas rapido, para instalar Gdebi tecleamos:
<pre lang="bash" line="1" escaped="true">sudo aptitude install gdebi gdebi-core</pre>
Para abrir los .Debs con Gdeb le damos click derecho algun archivo .deb que tengamos y seleccionamos "Propiedades"  en la ventana que se nos abra seleccionamos la pestaña "Abrir con" y en la lista seleccionamos a Gdebi.

de todos modos y si te gusta mas la terminal siempre puedes instalar estos paquetes con:
<pre lang="bash" line="1" escaped="true">sudo dpkg -i paquete.deb</pre>
<strong>- Talika: </strong>Desde que instale este Applet para Gnome me quede con el y es una de mis primeras instalaciones al actualizar mi Ubuntu, para instalar y configurar tan solo sigue estos pasos en guia de <a href="http://blog.jam.net.ve/2010/06/13/instalando-talika-en-ubuntu-10-04-lts-lucid-lynx/">Instalacion de Talika en Ubuntu</a>

<strong>- Conky:</strong> es otro de mis imprecindibles, es un panel en el cual se muestra la informacion de la pc y demas info que desees. similar a los widget o gadget. Para instalarlo sigue los pasos de mi guia de <a href="http://blog.jam.net.ve/2009/12/21/instalando-conky-en-ubuntu-karmic/">Instalacion de Conky en Ubuntu</a> y luego complementa con <a href="http://blog.jam.net.ve/2010/08/05/mejorando-la-apariencia-de-conky-con-conky-colors/">Mejorando la apariencia de conky con conky-color</a>

<strong>- Gparted:</strong> esta es una aplicacion que nos permite crear particiones en nuestro disco duro o unidades USB:
<pre lang="bash" line="1" escaped="true">sudo aptitude install gparted</pre>
<strong>- GPA:</strong> es una interfaz grafica muy completa y util para GnuPG con el cual podemos administrar nuestras llaves PGP, ademas de encriptar, firmar y desencriptar archivos o texto.
<pre lang="bash" line="1" escaped="true">sudo aptitude install gpa</pre>
<strong>- Htop: </strong>es una aplicacion para la terminal similar a el comando top que nos permite ver los diferentes procesos que se ejecutan en el sistema con la diferencia de que htop es un poco mas configurable y con caracteristicas interesantes como hacer scroll vertical u horizontal para poder visualizar mejor todos los procesos.
<pre lang="bash" line="1" escaped="true">sudo aptitude install htop</pre>
<strong>- Dnsmasq: </strong>nos permite acelerar un poco nuestra conexion usando una cache DNS, para instalar y configurar sigue mi guia de <a href="http://blog.jam.net.ve/2010/08/20/vuela-en-internet-usando-una-cache-dns-dnsmasq-en-ubuntu/">instalacion de DNSmasq en Ubuntu</a>.

<strong>- Adobe Flash: </strong>Para instalar los plugins flash 32bits tan solo teclea:
<pre lang="bash" line="1" escaped="true">sudo aptitude install flashplugin-installer</pre>
Pero si necesitas instalar los plugins Flash 64bits la unca opcion es instalar los plugins en fase beta de Adobe. para esto podemos agregar un PPA en donde estan estos plugins:
<pre lang="bash" line="1" escaped="true">sudo add-apt-repository ppa:sevenmachines/flash</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">sudo aptitude update</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">sudo aptitude install flashplugin64-installer</pre>
<strong>- Ubuntu tweak: </strong>es una util herramienta de configuracion y personalizacion para Ubuntu
<pre lang="bash" line="1" escaped="true">sudo add-apt-repository ppa:tualatrix/ppa
sudo aptitude update
sudo aptitude install ubuntu-tweak</pre>
<strong>- Ailurus: </strong> es una aplicacion similar a Ubuntu-tweak que vale la pena probar y tener:
<pre lang="bash" line="1" escaped="true">sudo add-apt-repository ppa:ailurus
sudo aptitude update
sudo aptitude install ailurus</pre>
<strong>- Chromium:</strong> es un interesante navegador web libre en el cual se basa el conocido navegador de Google Chrome:
<pre lang="bash" line="1" escaped="true">sudo aptitude install chromium-browser</pre>
<strong>- Opera: </strong>es otro de los populares navegadores web, para instalarlo solo descarga el paquete .deb desde la web oficial de <a href="http://www.opera.com/browser/download/">Opera.</a>

<strong>- Pidgin:</strong> es uno de los mejores clientes de mensajeria instantanea multiprotocolo.
<pre lang="bash" line="1" escaped="true">sudo aptitude install pidgin</pre>
<strong>- Java:</strong> bien este lenguaje y su JRE puede que sea necesario para ciertas  aplicaciones y paginas web, asi que conviene tenerlo instalado, para  hacerlo basta con teclear en la terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install sun-java6-jre sun-java6-plugin sun-java6-fonts</pre>
<strong>- Restaurar la posicion de los botones de las ventanas</strong>: Uno de los  cambios muy criticado que se hizo en Lucid es el cambio de los botones  de Maximizar, Minimizar y Cerrar al lado Izquierdo de las ventanas  similar al S.O Mac. porque han hecho esto? Ni idea :S intente  acostumbrarme pero a la hora ya me estaba molestando demasiado el  cambio.  Una de las maneras mas sencillas que encontre para volver a  colocar los botones al lado derecho de la ventana es con la aplicacion  Ailurus que ya deberias de haber instalado, aunque tambien puede hacerse  con Ubuntu Tweak.

* Para hacer el cambio con Ailurus: abres la aplicacion, luego click  en el icono “Sistema Configuraciones” y luego en ” Efecto de Ventanas”  en la parte de abajo donde dice “Presentacion de los botones de la barra  de titulos” de seguro aparecera “MAC OS X” Cambialo a “GNOME Clasico” y  listo. resuelto el problema.

* Para hacerlo con Ubuntu Tweak: Abres la aplicacion y has click en  el lado izquierdo donde dice “Configuracion del gestor de ventanas”   ahora en donde dice “Formato de botones en la barra de titulos de la  ventana”   marca la opcion “Derecho”  y listo!

Saludos y espero les sirva :D
