---
layout: post
title: !binary |-
  SW5zdGFsYSB5IHBydWViYSBEaWFzcG9yYSBQcmV2aWV3IGVuIFVidW50dSAt
  IFtBY3R1YWxpemFkb10=
tags:
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  bGludXg=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  dHV0b3JpYWw=
- !binary |-
  dWJ1bnR1
- !binary |-
  bWFudWFs
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFy
- !binary |-
  YmFzaA==
- !binary |-
  c2VndXJpZGFk
- !binary |-
  ZGlhc3BvcmE=
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
---
<strong>Nota: </strong>este articulo contiene una actualizacion importante que debe ser leida antes de continuar, por favor salte al final de este articulo.

<a href="http://www.joindiaspora.com/">Diaspora</a> es una aplicacion para crear redes sociales de codigo abierto enfocada en la seguridad y privacidad. Ayer fue liberado su codigo fuente para los desarrolladores y ya es posible instalarla en un servidor o en tu pc para probarla y/o comenzar a aportar ideas y reportar bugs que sean encontrados.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/09/default.jpg"><img class="aligncenter size-full wp-image-407" title="default" src="http://blog.jam.net.ve/imagenes/uploads/2010/09/default.jpg" alt="" width="190" height="190" /></a><a href="http://blog.jam.net.ve/imagenes/uploads/2010/09/diaspora_caps.png"><img class="aligncenter size-full wp-image-408" title="diaspora_caps" src="http://blog.jam.net.ve/imagenes/uploads/2010/09/diaspora_caps.png" alt="" width="143" height="21" /></a>

El codigo fuente de Diaspora se encuentra en <a href="http://github.com/diaspora/diaspora">GitHub</a> y contiene un completo manual (readme) el cual nos explica los pasos necesarios para la instalacion, aqui en este articulo le hare una traduccion, explicacion y le dare unos datos para que no les ocurran los mismos errores que me aparecieron a mi.

Bien primero que nada necesitamos instalar dependencias y aplicaciones que necesita diaspora para su funcionamiento:

<strong>1) Build Tools:</strong> Es probable que ya tengas algunas instaladas pero para asegurarnos tecleamos en la terminal

[bash] sudo apt-get install build-essential libxslt1.1 libxslt1-dev libxml2 libxslt-dev libxml2-dev [/bash]

Nota: en el readme no aparecen los dos ultimos paquetes pero yo los e agregado aqui ya que son necesarios para instalar nokogiri mas adelante.

<strong>2) Ruby:</strong> Diaspora esta hecho en Ruby por lo que tenemos que instalar este lenguaje, recomendable que sea Ruby 1.8.7:

[bash] sudo apt-get install ruby-full [/bash]

Nota: asegurate de instalar ruby-full y todas sus dependencias, si ya tienes instalado el paquete ruby basico y no instalas ruby-full puede que tengas problemas mas adelante en la instalacion.

<strong>3) MongoDB:</strong> Mondodb es una base de datos nosql que usara diaspora, para instalarla debemos agregar los repositorios oficiales editando /etc/apt/sources.list y agregando

[bash] deb http://downloads.mongodb.org/distros/ubuntu 10.4 10gen [/bash]

Luego de esto agregamos la llave GPG:

[bash] sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10 [/bash]

Actualizamos la lista de repositorios:

[bash] sudo apt-get update [/bash]

e instalamos MongoDB

[bash] sudo apt-get install mongodb-stable [/bash]

<strong>4) OpenSSL:</strong> Es muy probable que ya lo tengas instalado ya que viene por defecto en Ubuntu, asi que lo saltamos :-)

<strong>5) ImageMagicK:</strong>

[bash] sudo apt-get install imagemagick libmagick9-dev [/bash]

<strong>6) Git:</strong> El repo de Diaspora esta en Git asi que necesitamos instalarlo para bajarnos el fuente desde el mismo:

[bash] sudo apt-get install git-core [/bash]

<strong>7) RubyGems:</strong> Ya que Diaspora esta hecho en Ruby, se vale de algunas Gemas. Para instalarlo nos descargamos RubyGems:

[bash] wget http://production.cf.rubygems.org/rubygems/rubygems-1.3.7.tgz [/bash]

Luego lo descomprimimos

[bash] tar -xf rubygems-1.3.7.tgz [/bash]

Luego nos movemos a la carpeta resultante:

[bash] cd rubygems-1.3.7 [/bash]

Ahora instalamos el RubyGems:

[bash] sudo ruby setup.rb [/bash]

y por ultimo tecleamos

[bash] sudo ln -s /usr/bin/gem1.8 /usr/bin/gem [/bash]

<strong>8) Bundler: </strong>Esta aplicacion es una especie de manejador de dependencias para aplicaciones ruby el cual nos instalara las aplicaciones (un monton de gemas) necesarias para que Diaspora se ejecute correctamente, para instalarlo tecleamos:

[bash] sudo gem install bundler [/bash]

<strong>9) Diaspora: </strong>Bien ahora si nos toca bajarnos el fuente de Diaspora desde el git:

[bash] git clone http://github.com/diaspora/diaspora.git [/bash]

<strong>10) Instalando las gemas necesarias:</strong> Para ejecutar Diaspora necesitamos instalar algunas gemas de las que diaspora depende, para esto, abrimos la terminal y nos movemos dentro de carpeta donde se descargo el codigo fuente de Diaspora cuando ejecutamos el comando anterior, una vez alli tecleamos:

[bash] sudo bundle install [/bash]

Con esto Bundler nos instalara unas cuantas gemas que usa Diaspora.

<strong>11) Iniciar MongoDB:</strong> Ya que la instalacion la estamos haciendo en Ubuntu es probable que MongoDB ya este iniciado, de lo contrario podemos teclear el comando:

[bash] sudo service mongodb status [/bash]

para comprobar que esta corriendo, o si no tecleamos

[bash] sudo service mongodb start [/bash]

para iniciarlo.

<strong>12) Corriendo la Aplicacion: </strong>Si no has tenido ningun problema y has realizado correctamente la instalacion entonces podemos pasar a ejecutar el servicio y correr Diaspora tecleando en la terminal:

[bash] sudo bundle exec thin start [/bash]

Ya con esto deberias estar corriendo la Preview de Diaspora!!! :-)

Tan solo abre tu navegador y teclea en la barra de direccion:

[bash] http://localhost:3000 [/bash]

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/09/diaspora-local-ubuntu.png"><img class="aligncenter size-medium wp-image-409" title="diaspora-local-ubuntu" src="http://blog.jam.net.ve/imagenes/uploads/2010/09/diaspora-local-ubuntu-300x171.png" alt="" width="300" height="171" /></a>

Saludos y Espero les sirva...

Fuente: <a href="http://github.com/diaspora/diaspora">Github Diaspora</a>

<strong>Actualizacion al 29-01-2011: Diaspora* dejo por ahora la base de datos NoSQL MongoDB y migro sus datos a MySQL, por lo que esta guia queda desactualizada y no refleja el nuevo cambio. Por favor siga la guia oficial de <a href="https://github.com/diaspora/diaspora/wiki/Installing-and-Running-Diaspora">instalacion de Diaspora* </a>(en Ingles). queda el articulo en publiacion a modo de historial.
</strong>
