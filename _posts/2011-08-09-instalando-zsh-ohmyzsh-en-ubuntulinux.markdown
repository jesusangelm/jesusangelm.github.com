---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBaU0ggKyBPaE15WlNIIGVuIFVidW50dS9MaW51eA==
tags:
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  bGludXg=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  c29mdHdhcmU=
- !binary |-
  dWJ1bnR1
- !binary |-
  dW5peA==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  dGVybWluYWw=
- !binary |-
  enNo
- !binary |-
  b2hteXpzaA==
---
Extraído de Wikipedia:

<strong>ZSH:</strong>
<blockquote>Es un potente <a title="Shell (informática)" href="http://es.wikipedia.org/wiki/Shell_(inform%C3%A1tica)">intérprete de comandos</a> para sistemas operativos de tipo <a title="Unix" href="http://es.wikipedia.org/wiki/Unix">Unix</a>, como por ejemplo los <a title="BSD" href="http://es.wikipedia.org/wiki/BSD">BSD</a> o <a title="GNU/Linux" href="http://es.wikipedia.org/wiki/GNU/Linux">GNU/Linux</a>.<sup id="cite_ref-0"><a href="http://es.wikipedia.org/wiki/Zsh#cite_note-0">1</a></sup> La primera versión de zsh fue escrita por <a title="Paul Falstad (aún no redactado)" href="http://es.wikipedia.org/w/index.php?title=Paul_Falstad&amp;action=edit&amp;redlink=1">Paul Falstad</a> en <a title="1990" href="http://es.wikipedia.org/wiki/1990">1990</a>, cuando era estudiante en la <a title="Universidad de Princeton" href="http://es.wikipedia.org/wiki/Universidad_de_Princeton">Universidad de Princeton</a>. Zsh se diseñó para poder usarse interactivamente. Se le han incorporado muchas de las características principales de otras shells de Unix como, <a title="Bash" href="http://es.wikipedia.org/wiki/Bash">bash</a>, <a title="Ksh" href="http://es.wikipedia.org/wiki/Ksh">ksh</a>, o <a title="Tcsh" href="http://es.wikipedia.org/wiki/Tcsh">tcsh</a>y además posee características propias originales</blockquote>
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/uploads/2011/08/Pantallazo-60.png"><img class="aligncenter size-full wp-image-821" title="Pantallazo-60" src="http://blog.jam.net.ve/imagenes/uploads/2011/08/Pantallazo-60.png" alt="" width="141" height="120" /></a><span style="color: #000000;"><strong>+</strong></span></p>
<a href="http://blog.jam.net.ve/imagenes/uploads/2011/08/ohmyzsh_o.png"><img class="aligncenter size-full wp-image-822" title="ohmyzsh_o" src="http://blog.jam.net.ve/imagenes/uploads/2011/08/ohmyzsh_o.png" alt="" width="100" height="100" /></a>

Una de las características de Zsh que enamoran al usuario es su alta capacidad de personalización y ser compatible con Bash. pues bien estas dos características justamente son las que me hicieron probar por unos meses Zsh y luego usarla como Shell por defecto en mi PC y Laptop.

<strong>OhMyZsh:</strong> Es un framework impulsado por la comunidad para la administración de las configuraciones de Zsh, el cual le agrega características como auto-completado, corrección de escritura y viene con mas de 50 plugins opcionales que agregan aun mas funcionalidades a la shell. no conforme con esto también incluye la posibilidad de personalizar la forma en que se muestra tu shell y la información que esta muestre mediante themes que puedes crear tu mismo, o usar uno de los que incluye <a title="OhMyZsh on Github" href="https://github.com/robbyrussell/oh-my-zsh">OhMyZsh</a> (mas de 90).

Instalación: Para instalar Zsh en Ubuntu tan solo debemos ejecutar en la terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install zsh</pre>
con esto ya tendremos instalado Zsh con las caracteristicas que vienen por defecto, pero como en este caso queremos es explotar sus capacidades de personalización necesitaremos instalar OhMyZsh.

<a title="OhMyZsh on GitHub" href="https://github.com/robbyrussell/oh-my-zsh">OhMyZsh</a> se instala descargándolo desde su <a href="https://github.com/robbyrussell/oh-my-zsh">repositorio en GitHub</a>, el autor ofrece un comando que automatiza la descarga e instalacion del mismo, pero para poder ejecutarlo necesitas tener instalado Git para clonar el repositorio, esto lo haces son un simple: <strong>sudo aptitude install</strong> git una vez instalado Git puedes instalar OhMyZsh tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">wget --no-check-certificate https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh</pre>
Con este comando se descargara <a href="https://github.com/robbyrussell/oh-my-zsh">OhMyZsh</a> desde su repo en github y lo clonara en la carpeta ~/.oh-my-zsh de tu usuario, luego de eso podrás comenzar a usarlo.

Instalación Manual: el metodo mas largo (la verdad no tanto) para instalar <a href="https://github.com/robbyrussell/oh-my-zsh">OhMyZsh</a> es simple, tan solo clona el repositorio en una carpeta oculta llamada <strong>.oh-my-zsh</strong> tecleando:
<pre lang="bash" line="1" escaped="true">git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh</pre>
luego de esto creas tu archivo de configuracion <strong>.zshrc</strong> copiando la plantilla que OhMyZsh trae por defecto:
<pre lang="bash" line="1" escaped="true">cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc</pre>
Por ultimo ajusta Zsh para que sea tu shell predeterminada:
<pre lang="bash" line="1" escaped="true">chsh -s /usr/bin/zsh</pre>
ya luego de esto solo debes reiniciar o abrir una nueva terminal para ver Zsh+OhMyZsh funcionando.

<strong>Personalización:</strong> si vas a la carpeta ~/.oh-my-zsh/themes  y ~/.oh-my-zsh/plugins veras los themes y plugins disponibles para personalizar tu shell y activar nuevas funcionalidades.

<strong>*</strong> Para activar y usar un plugins tan solo debes abrir con tu editor favorito el archivo ~/.zshrc y buscar la linea:
<pre lang="bash" line="1" escaped="true">plugins=(git)</pre>
y agregar dentro de los paréntesis el nombre del plugins que quieres usar, por ejemplo en las ultimas actualizaciones de han agregado plugins como cloudapp el cual es una herramienta para subir imágenes desde la terminal  a el hosting de imagenes en getcloudapp.com que hasta donde se puede ver en la pagina solo ofrece soporte para MacOS, pero como dispone de una API, podemos usarlo tambien en Linux :P  asi que para agregarlo tan solo escribimos:
<pre lang="bash" line="1" escaped="true">plugins=(git cloudapp)</pre>
<strong>*</strong> Para activar y usar themes es similar a como hicimos para ctivar plugins. pero en vez de buscar la linea plugins, buscamos la linea:
<pre lang="bash" line="1" escaped="true">ZSH_THEME="robbyrussell"</pre>
y cambiamos "robbyrussell" por el nombre del theme que quieras usar.

yo en mi caso me hice mi <a title="JAM Zsh Theme" href="https://github.com/jesusangelm/Jam-Zsh-Theme">propio theme</a> modificando y combinando funciones de varios themes que vienen incluidos, mi theme lo llame "<a href="https://github.com/jesusangelm/Jam-Zsh-Theme">jam</a>" por lo que en mi caso esta linea se ve asi:
<pre lang="bash" line="1" escaped="true">ZSH_THEME="jam"</pre>
y mi shell se ve asi:

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/08/jamzshtheme.jpeg"><img class="aligncenter size-medium wp-image-823" title="jamzshtheme" src="http://blog.jam.net.ve/imagenes/uploads/2011/08/jamzshtheme-300x71.jpg" alt="" width="300" height="71" /></a>
