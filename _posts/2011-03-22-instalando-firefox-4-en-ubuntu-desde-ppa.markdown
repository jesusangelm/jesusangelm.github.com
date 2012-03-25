---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBGaXJlZm94IDQgZW4gVWJ1bnR1IGRlc2RlIFBQQQ==
tags:
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  bGludXg=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  dWJ1bnR1
- !binary |-
  YWN0dWFsaXphY2lvbg==
- !binary |-
  bHVjaWQ=
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  bWF2ZXJpY2s=
- !binary |-
  ZXN0YWJsZQ==
- !binary |-
  ZmlyZWZveA==
- !binary |-
  cHBh
---
Hace tan solo unas horas atrás fue liberado ¡¡¡por fin!!! la versión <strong>Estable</strong> de Firefox 4, luego de algo mas de un año de desarrollo, mockup, atrasos, unas cuantas liberaciones Betas, cancelaciones de funciones y dos Release Candidate, por fin tenemos en nuestras manos el popular navegador Firefox 4 cargado con un rediseño completo de la interfaz de usuarios el cual seria un cambio radical si vienes de la versión 3.6 o inferior ya que cambia la forma en la que se organizan las pestañas (arriba de la barra de navegación), el acceso al menú y demás funciones, muy similar al estilo del navegador Opera 11.

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/03/firefoxlogo.png"><img class="aligncenter size-medium wp-image-691" title="firefoxlogo" src="http://blog.jam.net.ve/imagenes/uploads/2011/03/firefoxlogo-300x289.png" alt="Logo Firefox" width="300" height="289" /></a>

Para instalar/actualizar a la nueva versión de Firefox 4 en Ubuntu podemos usar el PPA de MozillaTeam en Launchpad el cual podemos agregar tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">sudo add-apt-repository ppa:mozillateam/firefox-stable</pre>
y luego actualizamos la lista de repositorios tecleando:
<pre lang="bash" line="1" escaped="true">sudo aptitude update</pre>
Una vez realizado esto podemos instalarlo (si todavia no lo tienes) tecleando:
<pre lang="bash" line="1" escaped="true">sudo aptitude install firefox</pre>
En caso de que ya este instalado tan solo actualizamos tecleando:
<pre lang="bash" line="1" escaped="true">sudo aptitude safe-upgrade</pre>
Cabe destacar que en este PPA esta disponible solo para <strong>Lucid</strong> y <strong>Maverick</strong>.

Nota: esto nos descarga el navegador en Ingles, por lo que si deseas colocarlo al Español, debes Descargar el <a title="Idioma Español para Firefox 4" href="http://releases.mozilla.org/pub/mozilla.org/firefox/releases/4.0/linux-i686/xpi/es-ES.xpi" target="_blank">Pack de Idioma Español</a>. <strong>¡Gracias a Isaias!</strong> por la información y el comentario.
