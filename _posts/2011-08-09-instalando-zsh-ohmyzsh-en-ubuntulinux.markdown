---
layout: post
title: "Instalando Zsh y OhMyZsh en Linux"
tags: [zsh, personalizacion, linux, shell]
---

Extraído de Wikipedia:

**ZSH:**

> Es un potente intérprete de comandos para sistemas operativos de tipo Unix, como por ejemplo los BSD o GNU/Linux.1 La primera versión de zsh fue escrita por Paul Falstad en 1990, cuando era estudiante en la Universidad de Princeton. Zsh se diseñó para poder usarse interactivamente. Se le han incorporado muchas de las características principales de otras shells de Unix como, bash, ksh, o tcshy además posee características propias originales

<!-- more -->

Una de las características de Zsh que enamoran al usuario es su alta capacidad de personalización y ser compatible con Bash. pues bien estas dos características justamente son las que me hicieron probar por unos meses Zsh y luego usarla como Shell por defecto en mi PC y Laptop.

**OhMyZsh:** Es un framework impulsado por la comunidad para la administración de las configuraciones de Zsh, el cual le agrega características como auto-completado, corrección de escritura y viene con mas de 50 plugins opcionales que agregan aun mas funcionalidades a la shell. no conforme con esto también incluye la posibilidad de personalizar la forma en que se muestra tu shell y la información que esta muestre mediante themes que puedes crear tu mismo, o usar uno de los que incluye <a title="OhMyZsh on Github" href="https://github.com/robbyrussell/oh-my-zsh">OhMyZsh</a> (mas de 90).

**Instalación:** Para instalar Zsh en Ubuntu tan solo debemos ejecutar en la terminal:

{% highlight bash %}
sudo aptitude install zsh
{% endhighlight %}

con esto ya tendremos instalado Zsh con las caracteristicas que vienen por defecto, pero como en este caso queremos es explotar sus capacidades de personalización necesitaremos instalar OhMyZsh.

OhMyZsh se instala descargándolo desde su <a href="https://github.com/robbyrussell/oh-my-zsh">repositorio en GitHub</a>, el autor ofrece un comando que automatiza la descarga e instalacion del mismo, pero para poder ejecutarlo necesitas tener instalado Git para clonar el repositorio, esto lo haces son un simple: **sudo aptitude install** git una vez instalado Git puedes instalar OhMyZsh tecleando en la terminal:

{% highlight bash %}
wget --no-check-certificate https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
{% endhighlight %}

Con este comando se descargara <a href="https://github.com/robbyrussell/oh-my-zsh">OhMyZsh</a> desde su repo en github y lo clonara en la carpeta ~/.oh-my-zsh de tu usuario, luego de eso podrás comenzar a usarlo.

**Instalación Manual:** el metodo mas largo (la verdad no tanto) para instalar <a href="https://github.com/robbyrussell/oh-my-zsh">OhMyZsh</a> es simple, tan solo clona el repositorio en una carpeta oculta llamada <strong>.oh-my-zsh</strong> tecleando:

{% highlight bash %}
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
{% endhighlight %}

luego de esto creas tu archivo de configuracion <strong>.zshrc</strong> copiando la plantilla que OhMyZsh trae por defecto:

{% highlight bash %}
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
{% endhighlight %}

Por ultimo ajusta Zsh para que sea tu shell predeterminada:

{% highlight bash %}
chsh -s /usr/bin/zsh
{% endhighlight %}

ya luego de esto solo debes reiniciar o abrir una nueva terminal para ver Zsh+OhMyZsh funcionando.

**Personalización:** si vas a la carpeta ~/.oh-my-zsh/themes  y ~/.oh-my-zsh/plugins veras los themes y plugins disponibles para personalizar tu shell y activar nuevas funcionalidades.

* Para activar y usar un plugins tan solo debes abrir con tu editor favorito el archivo ~/.zshrc y buscar la linea:

{% highlight bash %}
plugins=(git)
{% endhighlight %}

y agregar dentro de los paréntesis el nombre del plugins que quieres usar, por ejemplo en las ultimas actualizaciones de han agregado plugins como cloudapp el cual es una herramienta para subir imágenes desde la terminal  a el hosting de imagenes en getcloudapp.com que hasta donde se puede ver en la pagina solo ofrece soporte para MacOS, pero como dispone de una API, podemos usarlo tambien en Linux :P  asi que para agregarlo tan solo escribimos:

{% highlight bash %}
plugins=(git cloudapp)
{% endhighlight %}

* Para activar y usar themes es similar a como hicimos para ctivar plugins. pero en vez de buscar la linea plugins, buscamos la linea:

{% highlight bash %}
ZSH_THEME="robbyrussell"
{% endhighlight %}

y cambiamos "robbyrussell" por el nombre del theme que quieras usar.

yo en mi caso me hice mi [propio theme](https://github.com/jesusangelm/Jam-Zsh-Theme) modificando y combinando funciones de varios themes que vienen incluidos, mi theme lo llame "<a href="https://github.com/jesusangelm/Jam-Zsh-Theme">jam</a>" por lo que en mi caso esta linea se ve asi:

{% highlight bash %}
ZSH_THEME="jam"
{% endhighlight %}

y mi shell se ve asi:

<a href="http://imgur.com/GqNVC"><img src="http://i.imgur.com/GqNVCl.jpg" title="Hosted by imgur.com" alt="" /></a>
