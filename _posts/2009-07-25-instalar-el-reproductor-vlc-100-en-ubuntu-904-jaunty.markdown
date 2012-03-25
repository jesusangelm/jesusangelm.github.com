---
layout: post
title: !binary |-
  SW5zdGFsYXIgZWwgUmVwcm9kdWN0b3IgVkxDIDEuMC4wIGVuIFVidW50dSA5
  LjA0IEphdW50eQ==
tags:
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  amF1bnR5
- !binary |-
  bGludXg=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  dWJ1bnR1
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  dmxj
- !binary |-
  cmVwcm9kdWN0b3I=
- !binary |-
  dmlkZW8=
---
Para instalar la version 1.0.0 del reproductor VLC Media Player tan solo debemos editar el archivo /etc/apt/sources.lis

Para eso tecleamos en consola:
<blockquote>sudo gedit /etc/apt/sources.list</blockquote>
y agregamos la siguiente linea:
<blockquote>deb http://ppa.launchpad.net/c-korn/vlc/ubuntu jaunty main</blockquote>
Guardamos y cerramos.

Luego tecleamos:
<blockquote>sudo apt-key adv <code>--</code>recv-keys <code>--</code>keyserver keyserver.ubuntu.com 7613768D</blockquote>
para añadir la llave GPG

luego de eso tecleamos tambien en consola:
<blockquote>sudo apt-get update</blockquote>
y luego:
<blockquote>sudo apt-get install vlc mozilla-plugin-vlc</blockquote>
Esto nos descargara los componentes, cuando haya finalizado la instalacion lo tendremos disponible en Aplicaciones/Sonido y Video/ VLC Media Player

Fuente: <a href="http://www.ubuntugeek.com/howto-install-vlc-media-player-1-0-0-in-ubuntu.html" target="_blank">Ubuntu Geek</a>
