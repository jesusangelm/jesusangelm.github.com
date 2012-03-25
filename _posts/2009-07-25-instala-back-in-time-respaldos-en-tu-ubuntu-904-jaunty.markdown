---
layout: post
title: !binary |-
  SW5zdGFsYSBCYWNrIGluIFRpbWUgLSBSZXNwYWxkb3MgZW4gdHUgVWJ1bnR1
  IDkuMDQgSmF1bnR5
tags:
- !binary |-
  Z25vbWU=
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  amF1bnR5
- !binary |-
  bGludXg=
- !binary |-
  cmVzcGFsZG8=
- !binary |-
  dWJ1bnR1
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  d2Vi
- !binary |-
  c2lzdGVtYXM=
---
Esta aplicacion de respandos es muy conocida y famosa. Para instalarlo tan solo debemos editar la lista de repos entrando en la consola y tecleando:

sudo gedit /etc/apt/sources.list

luego agregamos:

deb http://le-web.org/repository stable main

guardamos y luego tecleamos:

wget http://le-web.org/repository/le-web.key

y luego

sudo apt-key add le-web.key

para agregar la llave GPG

actualizamos tecleando:

sudo apt-get update

e instalamos el programa con:

sudo apt-get install backintime-common backintime-gnome

Una vez terminado la instalacion, deberia estar disponible en Aplicaciones/Herramientas de Sistemas/ Back in Time

Fuente: <a href="http://www.ubuntugeek.com/back-in-time-a-simple-backup-tool-for-ubuntu.html" target="_blank">Ubuntu Geek</a>
