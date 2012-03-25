---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBMaWJyZU9mZmljZSAzLjMgZXN0YWJsZSBlbiBVYnVudHUu
tags:
- !binary |-
  bGludXg=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  dWJ1bnR1
- !binary |-
  bGlicmVvZmZpY2U=
---
Hace unos dias fue liberado la primera version estable de LibreOffice, para los que no sepan LibreOffice es un fork de lo que fue durante muchos años la mas popular suite ofimatica; les estoy hablando de OpenOffice.  ¿Porque ya OpenOffice ya no es popular? ¿porque se le hizo un fork que dio como resultado LibreOffice? ¿Porque Canonical confirmo el uso de LibreOffice en Ubuntu 11.04 en vez de OpenOffice? Pues la respuesta se conoce como ORACLE y lo que paso exactamente es una enorme historia ya contada en otros blogs y paginas.

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/01/LO33.png"><img class="aligncenter size-medium wp-image-621" title="LO33" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/LO33-300x225.png" alt="" width="300" height="225" /></a>

Para instalar LibreOffice (y liberarte de OpenOffice) en Ubuntu tan solo debemos hacer lo siguiente:

- He leido muchos comentarios que al instalar LibreOffice teniendo OpenOffice instalado genera problemas de diversos tipos, asi que para evitarlos es mejor desinstalar completamente OpenOffice  (al fin y al cabo ya nadie lo quiere) tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude purge openoffice.org-core openoffice.org-common openoffice.org-l10n-common</pre>
Si no usas Aptitude o te da problemas prueba
<pre lang="bash" line="1" escaped="true">sudo apt-get purge openoffice*.*</pre>
Aconsejable revisar si se te escondio algun paquete de openoffice instalado.

Una vez liberado tu PC de todo OpenOffice nos toca agregar el PPA de LibreOffice, actualizar el listado de paquetes e instalar LibreOffice:
<pre lang="bash" line="1" escaped="true">sudo add-apt-repository ppa:libreoffice/ppa</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">sudo aptitude update</pre>
&nbsp;
<pre lang="bash" line="1" escaped="true">sudo aptitude install libreoffice libreoffice-l10n-es language-support-writing-es libreoffice-gnome</pre>
Con esto tendras instalado LibreOffice, el paquete de idioma Español y la integracion con Gnome.

Para ms info sobre esta Suite Ofimatica, otros metodos de instalacion y detalle de las novedades visita:

<a href="http://www.libreoffice.org/">LibreOffice.</a>
