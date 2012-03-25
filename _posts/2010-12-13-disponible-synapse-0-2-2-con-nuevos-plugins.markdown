---
layout: post
title: !binary |-
  RGlzcG9uaWJsZSBTeW5hcHNlIDAuMi4yIGNvbiBudWV2b3MgcGx1Z2lucw==
tags:
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  bGFuemFkb3I=
---
Leyendo en <a href="http://www.omgubuntu.co.uk/2010/12/synapse-update-brings-new-plugins-better-results/">OMG! Ubuntu</a> me encuentro con que ya esta disponible una nueva version de Synapse. Para los que no sepan todavia que es Synapse, pues se trata de un nuevo lanzador "semantico" de aplicaciones similar a el conocido Gnome Do y Kupfer.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Menú_013.jpeg"><img class="aligncenter size-medium wp-image-532" title="Menú_013" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Menú_013-300x84.jpg" alt="" width="300" height="84" /></a>

La nueva version de <a href="http://synapse.zeitgeist-project.com/wiki/index.php?title=Main_Page">Synapse 0.2.2</a> nos trae como novedad 3 nuevos plugins:

- Gnome Screensaver: Para bloquear la pantalla del equipo.

- OpenSearch: Para realizar busquedas en la web.

-Locate: Para buscar cosas en tu PC.

entre otras mejoras...

Si todavia no has instalado Synapse lo puedes hacer agregando el repositorio corresponiente tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">sudo add-apt-repository ppa:synapse-core/ppa</pre>
luego actualizamos el listado de paquetes con:
<pre lang="bash" line="1" escaped="true">sudo aptitude update</pre>
y instalamos Synapse con:
<pre lang="bash" line="1" escaped="true">sudo aptitude install synapse</pre>
Otra novedad que podemos encontrar es que ahora es posible sobreescribir el Theme por defecto (color blanco) y colocarlo de color negro, para hacer esto tan solo escribimos el siguiente codigo:
<pre lang="text" line="1" escaped="true">gtk_color_scheme = "green:#11ffeb\nbg_selected:#007269\nbg_normal:#232323\nfg_normal:#f5f5f5\nfg_selected:#ffffff\n" style "throbber" { fg[NORMAL] = @green bg[NORMAL] = shade (1.5 ,@bg_normal) } style "synapse" { bg[NORMAL] = @bg_normal bg[SELECTED] = @bg_selected base[SELECTED] =@bg_selected fg[NORMAL] = @fg_normal fg[SELECTED] = @fg_normal base[NORMAL] = lighter (lighter (@bg_normal)) base[SELECTED] = @bg_selected text[NORMAL] = @fg_normal text[SELECTED] = @fg_normal engine "murrine" { contrast = 0.6 arrowstyle = 2 reliefstyle = 3 highlight_shade = 1.0 glazestyle = 0 gradient_shades = {1.2, 1.0, 1.0, 0.8} roundness = 4 lightborder_shade = 1.26 lightborderstyle = 1 separatorstyle = 1 } } widget_class "*SynapseWindow*" style "synapse" #widget_class "*SynapseGuiListView*" style : highest "listview" widget_class "*SynapseGuiMenuThrobber*" style : highest "throbber"</pre>
En un archivo el cual llamaremos "gtkrc" (sin las comillas) y lo copiamos en la carpeta:
<pre lang="text" line="1" escaped="true">~/.config/synapse</pre>
Luego de eso reiniciamos el Synapse (en caso de que ya se estubiese ejecutando) o lo abrimos y ya deberiamos poder verlo con el theme oscuro :D
