---
layout: post
title: !binary |-
  TWVqb3JhbmRvIEdlZGl0IGNvbiBHbWF0ZQ==
tags:
- !binary |-
  Z25vbWU=
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  a2FybWlj
- !binary |-
  bGludXg=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  dWJ1bnR1
- !binary |-
  dW5peA==
- !binary |-
  cmFpbHM=
- !binary |-
  bHVjaWQ=
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  cnVieQ==
- !binary |-
  ZWRpdG9y
- !binary |-
  Z2VkaXQ=
- !binary |-
  Z21hdGU=
---
Saludos, tenia meses que no publicaba nada en mi blog, :P

Gedit es un popular editor que viene por defecto en muchas distribuciones Linux basadas en Gnome, su rapidez, poco consumo de recursos y facilidad de uso combinado con la posibilidad de mejorarlo mediante plugins, lo convierten en una buena opción para usarlo como editor preferido para programadores.

&nbsp;

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/07/regtransf_Mongoid.rb-programacion-proyectos-git-RT_RB_Mongoid-gedit_050.jpeg"><img class="aligncenter size-medium wp-image-812" title="regtransf_Mongoid.rb (~-programacion-proyectos-git-RT_RB_Mongoid) - gedit_050" src="http://blog.jam.net.ve/imagenes/uploads/2011/07/regtransf_Mongoid.rb-programacion-proyectos-git-RT_RB_Mongoid-gedit_050-300x249.jpg" alt="" width="300" height="249" /></a>

&nbsp;

Gmate por su parte es una colección de plugins, snippets, themes y demás utilidades para mejorar Gedit y convertirlo en un poderoso editor. Muchos de estos plugins, themes y snippets han sido inspirados o se han convertido de funciones y características que se encuentran en TextMate, el famoso editor para Mac y muy usado por desarrolladores Ruby/Rails.

Para instalar Gmate en Linux tenemos dos opciones:

- Instalando Gmate en Ubuntu desde PPA:

Si usas Ubuntu podras instalar Gmate desde su repo en Launchpad, nada mas tenemos que agregar dicho repo tecleando en una terminal:

&nbsp;
<pre lang="bash" line="1" escaped="true">sudo apt-add-repository ppa:ubuntu-on-rails/ppa</pre>
Actualizamos el listado de paquetes con <strong>sudo aptitude update</strong> y luego instalamos Gmate con:
<pre lang="bash" line="1" escaped="true">sudo apt-get install gedit-gmate</pre>
&nbsp;

Con esto ya tendremos instalado Gmate, con todos sus plugins habilitados, nada mas tendríamos que ir a las preferencias y adaptarlo a nuestro gusto :D tocando las opciones de configuración de Gmate y de los plugins.

&nbsp;

- La otra opcion que tenemos para instalar Gmate es desde su repositorio en GitHub, esta opcion nos permite instalarlo en cualquier distro Linux y tener siempre la ultima version.

Para esto debemos tener instalado el sistema de control de versiones Git el cual puedes instalar en distros basadas en Debian con: <strong>sudo aptitude install git-core</strong>.

una vez instalado Git debemos instalar unas dependencias para Gmate, tan solo teclea:
<pre lang="bash" line="1" escaped="true">sudo aptitude install python-webkit python-pyinotify ack-grep</pre>
Luego de esto podemos clonar en nuestra PC el repositorio git tecleando:
<pre lang="bash" line="1" escaped="true">git clone git://github.com/gmate/gmate.git</pre>
luego nos movemos a la carpeta del repositorio gmate tecleando <strong>cd gmate</strong> y ejecutamos el instalador de Gmate tecleando:
<pre lang="bash" line="1" escaped="true">sh install.sh</pre>
Con esto tendremos instalado Gmate, por lo que tan solo queda configurar a gusto :D

Yo lo he usado durante mas de dos meses para programar en Ruby y Rails y puedo decir que me va muy bien. :P
