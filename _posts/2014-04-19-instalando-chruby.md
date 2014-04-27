---
layout: post
title: "Instalando chruby y ruby-install"
tags: [linux, archlinux, ubuntu, ruby]
---

**[chruby](https://github.com/postmodern/chruby)** es un administrador de versiones Ruby tal como RVM o rbenv pero que a
diferencia de estos dos ultimos, lleva la simplicidad al extremo ya que esa 
es basicamente su unica funcion, esto tambien le da la ventaja de ser uno de
los administradores de versiones Ruby mas ligero con cerca de [99 Lineas de codigo](https://github.com/postmodern/chruby/blob/master/share/chruby/chruby.sh).

La principal diferencia de **chruby** con respecto a **rvm** es su sencillez
debido a que no esta plagado de caracteristicas que probablemente no uses o que
en realidad no necesitas. Su principal diferencia con respecto a **rbenv** es
que no usa los fulanos `shims` los cuales en mi opinion y experiencia hacian que
los comandos ruby se ejecutaran con lentitud teniendo por ejemplo retrasos de
hasta 1 segundo para que respondiera un simple `ruby -v`.

<!-- more -->

Entre sus caracteristicas esta:

* Actualiza la Variable de Entorno `$PATH`.
* Agrega tambien los directorios RubyGems `bin/` a `$PATH`.
* Configura correctamente `$GEM_HOME` y `$GEM_PATH`.
  * lo que hace que para los usuarios las gemas se instalen en `~/.gem/$ruby/$version`.
  * y para el usuario root las gemas se instalen en `/path/to/$ruby/$gemdir`.
* Tambien configura las Variables de Entorno `$RUBY_ROOT`, `$RUBY_ENGINE`, `$RUBY_VERSION` y `$GEM_ROOT`.
* Opcionalmente puede configurar `$RUBYOPT` si se le da el argumento especifico.
* Llama a `hash -r` para limpiar el command-lookup hash-table.
* Por defecto usa la version ruby del sistema.
* Soporte opcional del cambiado automatico de rubies por medio del archivo `.ruby-version`.
* Soporte para bash y zsh.
* Ligero (~99 LOC).
* incluye tests.


##Instalacion:

La documentacion oficial de chruby te explica este paso pidiendote que
descargues la ultima version contenida en un archivo comprimido, pero yo
prefiero usar **Git**, listar los Tags de sus versiones y elegir la ultima
version para luego compilar desde alli, esto me permite estar al tanto de las
ultimas versiones con tan solo un `git pull` en vez de estar revisando la pagina
y descargar archivos comprimidos.

{% highlight bash %}
#clonamos el repositorio
$ git clone https://github.com/postmodern/chruby.git

#revisamos las versiones disponibles
$ git tag

#elegimos la ultima version disponible hasta ahora
$ git checkout v0.3.8

#instalamos
$ sudo make install
{% endhighlight %}

## Configuracion:

Luego de instalar **chruby** tan solo debemos modificar nuestro archivo de
configuracion `.bashrc` o `.zshrc` segun sea el caso y agregar la siguiente 
linea.

{% highlight bash %}
source /usr/local/share/chruby/chruby.sh
{% endhighlight %}

Ya con esto tenemos instalado y configurado chruby, pero debido a que chruby se
enfoca en ser lo mas simple y minimalista no podremos hacer nada con el sin
tener instalado alguna version de ruby. De hecho si escribes el comando `chruby`
en la terminal, este no te mostrara informacion alguna.

Es aqui donde entra **[ruby-install](https://github.com/postmodern/ruby-install)**. el cual es una aplicacion hecha por el
mismo creador de chruby la cual nos permite instalar cualquier version de ruby
que quieras, algo asi como el **ruby-build** de **rbenv** pero con
caracteristicas extras interesantes como resolucion de dependencias requeridas
para compilar las distintas versiones de ruby disponibles.

Para instalar ruby-install hacemos lo mismos pasos que hicimos para instalar
chruby:

{% highlight bash %}
#clonamos el repositorio
$ git clone https://github.com/postmodern/ruby-install.git

#revisamos las versiones disponibles
$ git tag

#elegimos la ultima version disponible hasta ahora
$ git checkout v0.4.2

#instalamos
$ sudo make install
{% endhighlight %}

Con esto tenemos instalado y listo para usar **ruby-install** por lo que modemos
probarla junto con **chruby** instalando alguna version de Ruby.

{% highlight bash %}
$ ruby-install ruby 2.1
{% endhighlight %}

Con esto comenzara la descarga, compilacion e instalacion de Ruby.

Si ejecutas `ruby-install` sin ningun parametro podras ver el listado de rubies
disponibles:

{% highlight bash %}
$ ruby-install 
Known ruby versions:
  ruby:
    1:      1.9.3-p545
    1.9:    1.9.3-p545
    1.9.3:  1.9.3-p545
    2.0:    2.0.0-p451
    2.0.0:  2.0.0-p451
    2:      2.1.1
    2.1:    2.1.1
    stable: 2.1.1
  jruby:
    1.7:    1.7.12
    stable: 1.7.12
  rbx:
    2.1:    2.1.1
    2.2:    2.2.6
    stable: 2.2.6
  maglev:
    1.0:    1.0.0
    1.1:    1.1RC1
    stable: 1.0.0
  mruby:
    1.0:    1.0.0
    stable: 1.0.0
{% endhighlight %}

Para decirle a **chruby** que use alguna version de ruby en especifico es tan
simple como un:

{% highlight bash %}
$ chruby ruby-2.1.1
{% endhighlight %}

chruby no cambia las versiones ruby por defecto y de hecho si reinicias la
terminal o la pc, no recuerda la version de ruby que acabas de perdirle que use,
por lo que si quieres que mantenga usando por defecto una version en especifica
puedes colocar en tu `.bashrc` o `.zshrc` ese mismo comando que usamos arriba.

