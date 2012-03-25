---
layout: post
title: !binary |-
  SW5zdGFsYSBDaHJvbWl1bSAoR29vZ2xlIENocm9tZSkgZW4gVWJ1bnR1IExp
  bnV4
tags:
- !binary |-
  Z29vZ2xl
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  amF1bnR5
- !binary |-
  bGludXg=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  c29mdHdhcmU=
- !binary |-
  dWJ1bnR1
- !binary |-
  d2luZG93cw==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  dGVybWluYWw=
---
Google Chrome es el navegador Open-Source de Google,  mejor conocido por su rapidez y fiabilidad, principalmente fue liberado para los S.O Windows, pero ya esta disponible su version para Linux.

Para instalarlo tan solo debemos:

- Editar el archivo /etc/apt/sources.list con el siguiente comando:

sudo gedit /etc/apt/sources.list

Para usuarios de Ubuntu 9.04 Jaunty agregar estos repositorios:

deb http://ppa.launchpad.net/chromium-daily/ppa/ubuntu jaunty main
deb-src http://ppa.launchpad.net/chromium-daily/ppa/ubuntu jaunty main

Para usuarios de Ubuntu 8.10 Intrepid agregar estos repositorios:

deb http://ppa.launchpad.net/chromium-daily/ppa/ubuntu intrepid main
deb-src http://ppa.launchpad.net/chromium-daily/ppa/ubuntu intrepid main

-Luego de agregar los repos de tu distro respectiva guarda los cambios y agregamos la llave GPG con el siguiente comando:

sudo apt-key adv <code>--</code>recv-keys <code>--</code>keyserver keyserver.ubuntu.com 0xfbef0d696de1c72ba5a835fe5a9bf3bb4e5e17b5

-Actualizamos la lista de software tecleando en la terminal:

sudo apt-get update

- Y ahora instalamos el Navegador con :

sudo apt-get install chromium-browser

Espero le haya servido a alguien, Saludos.

Fuente: <a href="http://www.ubuntugeek.com/install-chromium-google-chrome-web-browser-in-ubuntu.html" target="_blank">UbuntuGeek</a>
