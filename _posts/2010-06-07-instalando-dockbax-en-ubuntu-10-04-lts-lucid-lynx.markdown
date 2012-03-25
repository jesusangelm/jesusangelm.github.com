---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBEb2NrQmF4IGVuIFVidW50dSAxMC4wNCBMVFMgTHVjaWQg
  THlueA==
tags:
- !binary |-
  Z25vbWU=
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  d2luZG93cw==
- !binary |-
  dmlzdGE=
- !binary |-
  cGFuZWw=
- !binary |-
  bHVjaWQ=
- !binary |-
  bHlueA==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  ZXNjcml0b3Jpbw==
- !binary |-
  ZG9ja2Jhcg==
- !binary |-
  YmFy
- !binary |-
  YXBwbGV0
- !binary |-
  YmFzaA==
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
- !binary |-
  ZG9jaw==
- !binary |-
  ZG9ja2Jhcng=
---
Dockbarx es un Applet para el escritorio Gnome que permite visualizar en la barra de tareas las ventanas que tengas abiertas, la diferencia que tiene este applet es que Dockbarx las muestra en forma de botones similar a como lo hace Windows 7,  lo que a mi parecer  esta muy bien ya que permite ahorrar espacio en la barra de tareas si tenemos muchas ventanas abiertas y esteticamente es mas alegre a la vista.  Creo que a esta aplicacion le falta pulirse un poco ya que por ejemplo al tener una ventana minimizada decolora demasiado el icono de la misma, el applet predefinido en Gnome tambien lo hace pero no es tan drastico a como hace Dockbarx, sin embargo merece la pena probar... Quien quita y te quedes con ella para siempre :D

<a href="http://blog.jam.net.ve/imagenes/dockbarx.png"><img class="alignleft" title="DockBarX en Ubuntu Lucid Lynx" src="http://blog.jam.net.ve/imagenes/dockbarx.png" alt="DockBarX en Ubuntu Lucid Lynx" width="240" height="47" /></a>

Para instalarlo tan solo debemos agregar el repositorio para Ubuntu 10.04 Lucid Lynx:

- Abrimos una terminal y abrimos la lista de repositorios tecleando

[bash] sudo gedit /etc/apt/sources.list [/bash]



- dentro de la lista al final agregamos los siguientes repositorios

[bash] deb http://ppa.launchpad.net/dockbar-main/ppa/ubuntu lucid main

deb-src http://ppa.launchpad.net/dockbar-main/ppa/ubuntu lucid main [/bash]



Luego de esto guardamos el cambio y cerramos Gedit.

- Ahora actualizamos la lista de paquetes tecleando

[bash] sudo apt-get uptate [/bash]



e instalamos Dockbarx tecleando

[bash] sudo apt-get install dockbarx [/bash]



con esto ya lo tendras instalado y listo para usar, para agregarlo a tu panel tan solo has click derecho en un area vacia donde deseas colocar el applet y elige "Añadir al Panel" busca Dockbarx Applet y presiona añadir. Con esto ya deberia estar en tu barra de tareas de Gnome.

Si deseas configurarlo un poco puedes abrir el editor de preferencias en el menu Aplicaciones/Accesorios/DockbarX Preference o en el mismo panel has click derecho en el separador que esta en el extremo izquierdo del applet (una pequeña linea vertical negra) y elige propiedades.

Bien algo que no lei en ninguna explicacion en Español para instalar este applet es que al instalarlo veras el applet predefinido de Gnome y el DockbarX al mismo tiempo por lo que de seguro te quieres quitar el de Gnome para quedarte con uno solo. Para hacerlo basta con solo darle click derecho en el separador que esta en el extremo izquierdo del applet (una pequeña linea vertical negra) y elegir "Quitar del panel" con eso tendras un solo applet.

Si quieres volver a colocar el Applet predeterminado de Gnome has lo mismo que cuando agregaste el applet DockbarX al panel, solo que esta vez selecciona el applet llamado "Lista de Ventanas"


Saludos y espero les sirva !!! :D
