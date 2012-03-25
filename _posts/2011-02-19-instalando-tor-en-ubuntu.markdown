---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBUb3IgZW4gVWJ1bnR1
tags:
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  a2FybWlj
- !binary |-
  bGlicmU=
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  bWJy
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  bHVjaWQ=
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  bWF2ZXJpY2s=
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
- !binary |-
  YW5vbmltYXRv
- !binary |-
  cHJpdmFjaWRhZA==
- !binary |-
  dG9y
- !binary |-
  cG9saXBv
---
<a href="https://www.torproject.org/">Tor</a> (The Onion Router) es una implementación libre de un sistema de encaminamiento llamado onion routing que permite a sus usuarios comunicarse en Internet de manera anónima.

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/02/Tor_logo0.png"><img class="aligncenter size-full wp-image-644" title="Tor_logo0" src="http://blog.jam.net.ve/imagenes/uploads/2011/02/Tor_logo0.png" alt="" width="138" height="84" /></a>

Para instalarlo en <a href="http://blog.jam.net.ve/tag/ubuntu/">Ubuntu</a> y poder navegar de manera "Anonima" en la red tan solo hay que seguir estos sencillos pasos:

Para instalar Tor es recomendable usar el repositorio oficial, en los repositorios de Ubuntu están los paquetes respectivos pero no es recomendable usarlos ya que son versiones inferiores y están desactualizados. Para añadir los repos oficiales tan solo debemos abrir el archivo /etc/apt/sources.list con tu editor favorito y agregar el repositorio. Desde la <a href="http://blog.jam.net.ve/tag/terminal/">terminal</a> podemos hacerlo ejecutando:
<pre lang="bash" line="1" escaped="true">sudo gedit /etc/apt/sources.list</pre>
y añadimos:
<pre lang="bash" line="1" escaped="true">deb http://deb.torproject.org/torproject.org maverick main</pre>
<strong>Nota:</strong> puedes sustituir "<a href="http://blog.jam.net.ve/tag/maverick/">maverick</a>" por el nombre codigo de tu distribucion. Ejem: "<a href="http://blog.jam.net.ve/tag/karmic/">karmic</a>", "<a href="http://blog.jam.net.ve/tag/lucid/">lucid</a>", etc.

Guardamos los cambios y cierra el archivo.

Ahora tan solo debemos añadir las llaves GPG del repositorio para luego actualizar la lista de paquetes e instalar Tor:
<pre lang="bash" line="1" escaped="true">gpg --keyserver keys.gnupg.net --recv 886DDD89</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | sudo apt-key add -</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">sudo aptitude update</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">sudo aptitude install tor tor-geoipdb</pre>
Con esto ya tendremos instalado Tor, pero todavia no esta listo para funcionar. Debemos instalar Polipo.

Para hacer esto tan solo debemos teclear en la terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install polipo</pre>
Polipo necesita algo de configuración, por suerte ya esta hecha, por lo que lo único que debemos hacer es descargarnos <a href="https://gitweb.torproject.org/torbrowser.git/blob_plain/HEAD:/build-scripts/config/polipo.conf">este archivo de configuración de Polipo</a> y guardarlo en la carpeta <strong>/etc/polipo</strong> con el nombre "<strong>config</strong>".

Debido a que luego de la instalación de polipo este mismo se inicio automaticamente debemos reiniciarlo para que tome la configuración nueva, por lo que debemos hacerlo tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">/etc/init.d/polipo restart</pre>
o con
<pre lang="bash" line="1" escaped="true">sudo service polipo restart</pre>
Por ultimo nos queda instalar el plugin <a href="https://addons.mozilla.org/en-US/firefox/downloads/latest/2275/addon-2275-latest.xpi?src=addondetail"><strong>Torbutton</strong> </a>en <strong>Firefox</strong> para que pueda usar la red de Tor y navegar de forma "Anonima". Una vez lo tengas instalado tan solo activalo y si todo a salido bien estaras navegando de forma "Anonima" en <a href="https://check.torproject.org/">internet.</a>
