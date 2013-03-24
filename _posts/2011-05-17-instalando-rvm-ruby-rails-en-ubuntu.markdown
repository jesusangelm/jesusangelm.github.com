---
layout: post
title: "Instalando RVM, Ruby y Rails en Linux."
tags: [ruby, rails, rvm, linux]
---
# Instalando RVM, Ruby y Rails en Linux.

{% include post_header.html %}

Hace unos días atras estaba intentando instalar Ruby 1.9.2  desde los repositorios, como ya mi laptop tenia la versión 1.8.7 me di a la tarea de desinstalar por completo esta versión. Luego de terminal de instalar Ruby 1.9.2 y hacer la primera prueba, me encontré con que con que no había salido todo bien, algunas aplicaciones como Gem y Rake estaban buscando el ejecutable de Ruby 1.8.7 (que ya no estaba) y no el de Ruby 1.9.2.  Leyendo en internet encontré algunas posibles soluciones en las que sugerían crear enlaces simbólicos para que de este modo las aplicaciones que buscaran determinadas versiones de Ruby (1.8.7 en mi caso) usara la versión instalada (Ruby 1.9.2). asi lo hice, pero no fue la solución optima ya que muchas aplicaciones no estaban trabajando del todo bien y seguían mostrando algunos errores.

<a href="http://imgur.com/zRyar"><img src="http://i.imgur.com/zRyar.png" title="Hosted by imgur.com" alt="" /></a>

De vuelta a los buscadores,  intentando encontrar alguna forma de tener Ruby 1.9.2 + Rails 3.0.7 y demás acompañantes en su ultima versión trabajando en armonía y sin problemas, me tope con  [RVM](https://rvm.beginrescueend.com) (Ruby Version Manager) el cual es una aplicación de linea de comandos que nos permite instalar, administrar y poder trabajar con múltiples versiones (o sabores) de Ruby y otras aplicaciones en gemas. Esto quiere decir que si asi lo queremos podríamos tener instalado en nuestra computadora Ruby 1.8.7, Ruby 1.9.2, Rails 2.x, Rails 3.07  y usar en cualquier momento la version que mas nos convenga. En este caso yo instale Ruby 1.9.2 + Rails 3.0.7 En Ubuntu 10.10 64bits.

**Instalación:**

Si nos vamos a la guia de<a href="https://rvm.beginrescueend.com/rvm/install/" target="_blank"> instalación</a> en la pagina oficial, lo primero que nos dice es que tenemos dos formas de instalación a elegir:

**Instalación para un solo usuario** es la mas comun, y la recomendada en la cual todo el contenido de RVM y la versión de Ruby y Gems a elegir estarán ubicadas en la carpeta del usuario que realice la instalación.

**Instalación multi-usuario (root)** este método es similar a como cuando instalas Ruby u otro paquete desde los repositorios usando privilegios de administrador, este metodo permise que todos los usuarios en el sistema puedan usar la instalacion de RVM y Ruby.

Como yo soy el único que usa esta Laptop y tan solo quiero Ruby para aprender y hacer pruebas, me basta con la primera opción, ademas de que me da la ventaja de mantener mi configuración en caso de que decida reinstalar el S.O tan solo haciendo un respaldo de mi carpeta personal y luego restaurándola en otra PC.

Para instalar RVM tecleamos en una terminal:

**Nota:** este comando requiere algunas dependencias instaladas, tan solo teclean **sudo aptitude install build-essential git-core curl** en la terminal y luego continua con:

{% highlight bash %}
bash <<(curl -s https://rvm.beginrescueend.com/install/rvm)
{% endhighlight %}

Esto nos descargara un script en bash (el cual recomiendan leer <a href="https://rvm.beginrescueend.com/install/rvm" target="_blank">aqui</a>) que luego es ejecutado por... ¡adivinen! :P  ¡si! por Bash. este script lo que hace es clonar RVM de su repositorio en <a href="https://github.com/wayneeseguin/rvm" target="_blank">GitHub</a>

Una vez terminada la instalacion, el contenido de RVM se ubicara en la carpeta <strong>.rvm</strong> que se encuentra dentro de tu carpeta de usuario <strong>~/ </strong>

**Cargando RVM en tu sesion Shell como funcion:**

Para que nuestra terminal pueda trabajar sin problemas con RVM debemos agregar la siguiente linea al archivo <strong>~/.bash_profile</strong>, para esto tecleamos en la terminal:

{% highlight bash %}
echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' && ~/.bash_profile
{% endhighlight %}

**Recargando la configuración de Shell y primera prueba:**

Cierra y abre tu terminal en uso, (o abre una nueva) y teclea en ella la siguiente linea para recargar la configuración nueva:

{% highlight bash %}
source .bash_profile
{% endhighlight %}

Luego teclea la siguiente linea para hacer una prueba y ver si todo esta trabajando bien:

{% highlight bash %}
type rvm | head -1
{% endhighlight %}

Si todo ha ido bien, nos deberia responder **rvm: es una función**

Ahora debemos verificar algunas otras dependencias a instalar antes de continuar:

{% highlight bash %}
rvm notes
{% endhighlight %}

Esto nos devuelve algo como esto:

{% highlight bash %}
Notes for Linux ( DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=10.10
DISTRIB_CODENAME=maverick
DISTRIB_DESCRIPTION="Ubuntu 10.10" )

NOTE: 'ruby' represents Matz's Ruby Interpreter (MRI) (1.8.X, 1.9.X)
             This is the *original* / standard Ruby Language Interpreter
      'ree'  represents Ruby Enterprise Edition
      'rbx'  represents Rubinius

bash >= 3.2 is required
curl is required
git is required (>= 1.7 recommended)
patch is required (for ree and some ruby-head's).

If you wish to install rbx and/or Ruby 1.9 head (MRI) (eg. 1.9.2-head),
then you must install and use rvm 1.8.7 first.

If you wish to have the 'pretty colors' again,
  set 'export rvm_pretty_print_flag=1' in ~/.rvmrc.

dependencies:
# For RVM
  rvm: bash curl git

# For Ruby (MRI &amp; ree)  you should install the following OS dependencies:
  ruby: /usr/bin/apt-get install build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev

# For JRuby (if you wish to use it) you will need:
  jruby: /usr/bin/apt-get install curl g++ openjdk-6-jre-headless
  jruby-head: /usr/bin/apt-get install ant openjdk-6-jdk

# In addition to ruby: dependencies,
  ruby-head: subversion

# For IronRuby (if you wish to use it) you will need:
  ironruby: /usr/bin/apt-get install curl mono-2.0-devel
{% endhighlight %}

Si leemos detenidamente notamos que una de las dependencias de RVM es Bash, Curl y Git, pero no necesitaremos instalarla ya que de seguro lo hiciste cuando ejecutaste el comando junto a la primera nota antes de instalar RVM, de lo contrario no estarías aqui :P También podemos ver que hay dependencia de acuerdo a la simplemente de Ruby que deseamos usar, en mi caso usare Ruby ('ruby' represents Matz's Ruby Interpreter (MRI) (1.8.X, 1.9.X)) el cual es el mas común ya uqe Jruby es una implementacion de Ruby+Java y Ironruby es implementacion de Ruby+plataforma .Net/Mono. por lo tanto las dependencias a instalar para Ruby serian:


{% highlight bash %}
sudo aptitude install build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev
{% endhighlight %}

¡Felicidades! ya has instalado RVM, pero todavia no hemos terminado...


**Instalando Ruby + Rails:**

Bien aquí viene la parte mas divertida, primero instalaremos Ruby, recuerden que en mi caso elegi la version 1.9.2 por lo que tecleo en la terminal:

{% highlight bash %}
rvm install 1.9.2
{% endhighlight %}

Este proceso puede llevar algunos minutos ya que el comando descargara las fuentes de Ruby, las extraerá en la carpeta ~/.rvm , lo compilara y luego lo instalara.

Una vez terminado el proceso deberás elegir la versión de Ruby a usar, en nuestro caso instalamos Ruby 1.9.2 por lo que tecleamos en la terminal:

{% highlight bash %}
rvm use 1.9.2
{% endhighlight %}

Bien ahora a comprobar que hemos hecho todo bien, tecleamos en la terminal:

{% highlight bash %}
ruby -v
{% endhighlight %}

lo que nos deberá responder algo similar a: **ruby 1.9.2p180 (2011-02-18 revision 30909) [x86_64-linux]**

**comprobación extra:** si tecleamos el comando <strong>which ruby</strong> podremos ver donde se encuentra el ejecutable de Ruby, en mi caso es: <strong>/home/angel/.rvm/rubies/ruby-1.9.2-p180/bin/ruby</strong> Si hubiésemos instalado ruby desde los repos la ubicacion seria algo como <strong>/usr/bin/ruby</strong>


Si queremos usar esta version de Ruby por defecto, deberemos teclear en la terminal:

{% highlight bash %}
rvm use 1.9.2 --default
{% endhighlight %}

<strong>Pero hay algo que debemos corregir</strong>, ya que si por ejemplo reiniciamos la PC y al entrar abrimos una terminal y tecleamos <strong>ruby -v</strong> de seguro obtendremos un error que nos dira que no tenemos ruby instalado, ¡como que no si lo acabo de hacer!, para solventar esto abrimos con tu editor de texto favorito el archivo <strong>.bashrc</strong> ubicado en tu carpeta de usuario <strong>~/.bashrc</strong> y al final del archivo coloca la siguiente linea:

{% highlight bash %}
source $HOME/.rvm/scripts/rvm
{% endhighlight %}

Ruby 1.9.2 incluye rubygems, asi que lo mas que podriamos hacer seria actualizar tecleando en la terminal:

{% highlight bash %}
gem update --system<
{% endhighlight %}

revisamos la versión de gem tecleando <strong>gem -v</strong> en la terminal

**Instalación de Rails:**

{% highlight bash %}
gem install rails
{% endhighlight %}

verificamos la version de rails tecleando en la terminal <strong>rails -v</strong>


Si eres de los que usas <strong>IRB</strong> (Ruby Interactivo) de seguro al ejecutarlo te mostrara un mensaje de error referente a <strong>readline</strong>, ademas en IRB no podras mover el cursor entre los caracteres y/o no tendrás auto-completado. Para solucionar esto tecleamos en la terminal estos tres comandos:

{% highlight bash %}
cd .rvm/src/ruby-1.9.2-p180/ext/readline/
ruby extconf.rb
make install
{% endhighlight %}

Para verificar abre de nuevo IRB, si todo ha salido bien, notaras que puedes mover el cursor entre los caracteres y tendrás auto-completado.


**Mejora Extra en IRB:**

si deseas tener coloreado en IRB instala las gemas wirble y hirb:

{% highlight bash %}
gem install wirble hirb
{% endhighlight %}

Luego abre el archivo <strong>.irbrc</strong> ubicado en tu carpeta de usuario <strong>~/.irbrc</strong> (crealo si no existe) y agrega lo siguiente:

{% highlight ruby %}
require 'rubygems'
require 'wirble'
require 'hirb'
Wirble.init
Wirble.colorize
# hirb (active record output format in table)
Hirb::View.enable

# IRB Options
IRB.conf[:AUTO_INDENT] = true
IRB.conf[:SAVE_HISTORY] = 1000
IRB.conf[:EVAL_HISTORY] = 200

# Log to STDOUT if in Rails
if ENV.include?('RAILS_ENV') &amp;&amp; !Object.const_defined?('RAILS_DEFAULT_LOGGER')
  require 'logger'
  RAILS_DEFAULT_LOGGER = Logger.new(STDOUT)
  #IRB.conf[:USE_READLINE] = true

  # Display the RAILS ENV in the prompt
  # ie : [Development]&gt;&gt;
  IRB.conf[:PROMPT][:CUSTOM] = {
   :PROMPT_N =>; "[#{ENV["RAILS_ENV"].capitalize}]&gt;&gt; ",
   :PROMPT_I =>; "[#{ENV["RAILS_ENV"].capitalize}]&gt;&gt; ",
   :PROMPT_S =>t; nil,
   :PROMPT_C =>; "?&gt; ",
   :RETURN =&gt; "=>; %s\n"
   }
  # Set default prompt
  IRB.conf[:PROMPT_MODE] = :CUSTOM
end

# We can also define convenient methods (credits go to thoughtbot)
# def me
#  User.find_by_email("me@gmail.com")</pre>
{% endhighlight %}



Bien esto es todo, ya queda de tu parte instalar las gemas que mas uses y adaptarlo de acuerdo a tus necesidades. :)

