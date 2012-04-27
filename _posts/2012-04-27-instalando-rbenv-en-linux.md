---
layout: post
title: "Instalando rbenv en linux"
categories: [herramientas, linux, programacion]
tags: [rbenv, linux, archlinux, ruby, programacion]
---
{% include JB/setup %}

#rbenv

Es una herramienta en linea de comandos que nos permite administrar y cambiar fácilmente
entre nuestras múltiples instalaciones de diversas versiones de Ruby. Es muy sencillo, discreto, 
y sigue la tradicion UNIX.

**[Rbenv](https://github.com/sstephenson/rbenv)** a diferencia de **RVM** solo nos permite en su instalacion 
por defecto administrar multiples versiones de Ruby, lo que nos lleva a una solucion mas limpia y 
simple con menos peculiaridades y trampas. **rbenv** fue creado por [Sam Stephenson](http://sstephenson.us/) de
[37Signal](http://37signals.com/) el cual creo el Framework JavaScript [Prototype](http://prototypejs.org/).

#Que hace rbenv?

- Nos permite cambiar la versión de Ruby global de usuario.

- Proporciona soporte para las versiones de Ruby en pre-proyecto o desarrollo.

- Permite reemplazar la version de Ruby con variables de entorno.

#En contraste con RVM, rbenv no...

- **Necesita ser cargado en una terminal.**

- **No sobreescribe comandos de consola como `cd`.** Eso es peligroso y propenso a errores.

- **Tiene un archivo de configuracion. No hay nada que configurar excepto que version de Ruby quieres usar.**

- **Instala Ruby.** Tu puedes compilar e instalar Ruby por tu cuenta, o usar [ruby-build](https://github.com/sstephenson/ruby-build) para automatizar el proceso.

- **Administra gemas.** Para ese trabajo existen muy buenas herramientas dedicadas como [Bundler](http://gembundler.com/).

- **Exige cambios de las librerias Ruby para compatibilidad.**

- **Pregunta con advertencias cuando cambios a un proyecto.** En lugar de ejecutar código arbitrario, rbenv lee solo el nombre de la version de cada proyecto.

#Instalacion.

**Antes que nada tengo que advertirte que rbenv no es compatible con RVM** por lo que si estas usandolo
te aconsejo desinstalarlo. Como lo puedes hacer? simplemente elimina la carpeta `~/.rvm` y borra cualquier
referencia hacia **RVM** en tu `~/.bashrc` o `~/.bash_profile` o `~/.zshrc`.

**Antes de instalar rbenv debes instalar algunas dependencias basicas** para compilar Ruby entre otras cosas,
probablemente ya las tengas instaladas pero si obtienes algun error compilando Ruby te recomiendo leer 
mi **[Guia de instalacion de RVM](http://blog.jam.net.ve/2011/05/17/instalando-rvm-ruby-rails-en-ubuntu/)**.

- En primer lugar clonamos **rbenv** desde su repositorio Github a una carpeta en `~/.rbenv` ejecutanto en la terminal:

{% highlight bash %}
$ cd
$ git clone git://github.com/sstephenson/rbenv.git .rbenv
{% endhighlight %}

- Agregamos `~/.rbenv/bin` a nuestro `$PATH` para acceder al comando `rbenv`:

{% highlight bash %}
$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
{% endhighlight %}

**En caso de que uses Zsh** modifica `~/.zshrc` en lugar de `~/.bash_profile`

- Agrega `rbenv init` a tu shell para activar shims y autocompletado:

{% highlight bash %}
$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
{% endhighlight %}

**En caso de que uses Zsh** modifica `~/.zshrc` en lugar de `~/.bash_profile`

- Reinicia tu terminal, simplemente cierrala y vuelve a abrirla o ejecuta:

{% highlight bash %}
$ exec $SHELL
{% endhighlight %}

**FELICITACIONES!!! Con esto ya tienes instalado rbenv!!!**

#Instalacion de Ruby.

Existen dos metodos de instalar Ruby con rbenv:

**1-** Compilando desde sus fuentes:

Tan solo instala la versionde Ruby que desees en `~./rbenv/versions` por ejemplo si queremos instalar Ruby 1.9.3-p194:

- Descargamos los fuentes desde [ftp.ruby-lang.org](http://ftp.ruby-lang.org/pub/ruby/1.9/)

luego descomprimes el archivo, entramos a el en una terminal y ejecutamos los siguientes comandos:

{% highlight bash %}
$ ./configure --prefix=$HOME/.rbenv/versions/1.9.3-p194
$ make
$ make install
{% endhighlight %}

Con esto ya tendriamos instalado Ruby, tan solo nos faltaria reconstruir los archivos shim (calce) binarios:

{% highlight bash %}
$ rbenv rehash
{% endhighlight %}

**Nota** Esto lo debemos hacer cada vez que se instala un nuevo binario de Ruby como por ejemplo cuando
instalamos una nueva version de Ruby o cuando instalamos una Gema que contiene un binario como por ejemplo rake.

**2-** Por medio de el plugin [ruby-build](https://github.com/sstephenson/ruby-build)

Tan solo debemos instalarlo como plugins para rbenv dentro de `~/.rbenv/plugins` ejecutando los siguientes comandos:

{% highlight bash %}
$ mkdir -p ~/.rbenv/plugins
$ cd ~/.rbenv/plugins
$ git clone git://github.com/sstephenson/ruby-build.git
{% endhighlight %}

Luego de esto puedes usar el comando `rbenv install` por ejemplo si queremos instalar Ruby 1.9.2-p318 ejecutamos:

{% highlight bash %}
$ rbenv install 1.9.2-p318
{% endhighlight %}

**Nota:** debido a que **ruby-build** usa una especie de [recipes o definiciones de compilacion](https://github.com/sstephenson/ruby-build/tree/master/share/ruby-build) para descargar, compilar e instalas las distintas versiones de Ruby, al momento de ser liberada una nueva version de ruby te recomiendo 

**Antes** de intentar instalarla, actualizar el plugin **ruby-build** ejecutando en la terminal:

{% highlight bash %}
$ cd ~/.rbenv/plugins/ruby-build
$ git pull
{% endhighlight %}

Si luego de esto todavia no puedes instalar la nueva version de Ruby es posible que no este todavia actualizado
el repositorio de ruby-build por lo que deberas instalar descargando los fuentes y compilandolos tal cual 
explico en el 1er metodo.

**Nota:** Recuerda ejecutar `rbenv rehash` cada vez que instales una version de Ruby o instales una gema que
contenga binarios, esto es lo unico en lo que hay que tener cuidado con **rbenv**.


#Actualizando rbenv.

Debido a que rbenv se descarga desde su repositorio de desarrollo Github usando `git`, podemos actualizarlo a
la ultima version facilmente ejecutando en la terminal:

{% highlight bash %}
$ cd ~/.rbenv
$ git pull
{% endhighlight %}

#Usos basicos de rbenv.

Bien ya tenemos instalado rbenv y algunas versiones de Ruby, ahora nos toca ver como podemos cambiar entre
las distintas versiones que tenemos instaladas.

rbenv determina cual version de Ruby sera utilizada con un simple modelo de prioridad:

**global > local > shell**

- El parametro **global** le indica a rbenv que se usara la version de Ruby indicada en todo el sistema y todas
las consolas que se abran.

`rbenv global 1.9.3-p194`

- El parametro **local** le indica a rbenv que se usara la version de Ruby indicada solo en la carpeta 
(y subcarpetas) o proyecto en el que te encuentres, y lo configura creando un archivo oculto **.rbenv-version**
en la raiz de la carpeta en la que estas.

`rbenv local 1.9.2-p318`

- El parametro **shell** le indica a rbenv que se usara la version de ruby indicada solo en esa sesion shell
en ejecucion, por lo que al cerrar esa terminal y volverla abrir se fijara la version de
Ruby indicada en el parametro **global**

`rbenv shell 1.9.3-p125`

- Existe un parametro especial que le indica a rbenv usar la version de Ruby instalada en el sistema.
para acceder a ella tan solo ejecuta:

`rbenv system`

Para mas comandos utiles de rbenv puedes ejecutar `rbenv help` para leer la ayuda.
