---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBDaHJvbWl1biBlbiBVYnVudHUgS2FybWlj
excerpt: !binary |-
  Q2hvbWl1bSBlcyB1biBuYXZlZ2Fkb3IgZ3JhdHVpdG8geSB0b3RhbG1lbnRl
  IGxpYnJlIGVuIGVsIHF1ZSBzZSBiYXNhIGVsIGNvbm9jaWRvIG5hdmVnYWRv
  ciBkZSBHb29nbGUgbGxhbWFkbyBHb29nbGUgQ2hyb21lLCBsYXMgZGlmZXJl
  bmNpYXMgZW50cmUgZWxsb3Mgc29uIGNhc2kgbnVsYXMsIHBvciBlbmRlIHNv
  biBjYXNpIGlkZW50aWNvcy4gIExhIHVuaWNhIGRpZmVyZW5jaWEgcXVlIHNl
  IGhheSBlbnRyZSBlbGxvcyB5IGxhIHF1ZSBtZSBoaXpvIGNhbWJpYXJtZSBh
  IENocm9taXVtIGVuIHZleiBkZSB1c2FyIGVsIG5hdmVnYWRvciBkZSBHb29n
  bGUgZXMgcXVlIGVzdGUgdWx0aW1vLCBlcyBkZWNpciBHb29nbGUgQ2hyb21l
  IG5vIGVzIHVuIG5hdmVnYWRvciBsaWJyZSB5IGhheSBwcnVlYmFzIGRlIHF1
  ZSBhbCBpbnN0YWxhcnNlIGVuIExpbnV4IGFncmVnYSB1biBzY3JpcHQgImNy
  b24iIHF1ZSBzZSBlamVjdXRhIGEgZGlhcmlvIHBhcmEgYWdyZWdhciBhIG51
  ZXN0cmEgbGlzdGEgZGUgcmVwb3NpdG9yaW9zIGxvcyByZXBvcyBkZSBHb29n
  bGUuIGVzdG9zIHJlcG9yaXRvcmlvcyBxdWUgc2UgYWdyZWdhbiBzb24gc3Vw
  dWVzdGFtZW50ZSBwYXJhIGxhcyBhY3R1YWxpemFjaW9uZXMgZGVsIHNpc3Rl
  bWEsIGVsIGRldGFsbGUgZXN0YSBlbiBxdWUgc2kgbm9zIGRhIGxhIGdhbmEg
  ZGUgYm9ycmFybG9zIHNlIHZpZW5lbiB5IHNlIGluc3RhbGFuIHNvbG9zIGRl
  IG51ZXZvIGFsIGRpYSBzaWd1aWVudGUgISEhLg==
tags:
- !binary |-
  Z29vZ2xl
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  a2FybWlj
- !binary |-
  bGlicmU=
- !binary |-
  bGludXg=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  c29mdHdhcmU=
- !binary |-
  dWJ1bnR1
- !binary |-
  YWN0dWFsaXphY2lvbg==
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  dGVybWluYWw=
---
Chomium es un navegador gratuito y totalmente libre en el que se basa el conocido navegador de Google llamado Google Chrome, las diferencias entre ellos son casi nulas, por ende son casi identicos.  La unica diferencia que se hay entre ellos y la que me hizo cambiarme a Chromium en vez de usar el navegador de Google es que este ultimo, es decir Google Chrome no es un navegador libre y hay pruebas de que al instalarse en Linux agrega un script "cron" que se ejecuta a diario para agregar a nuestra lista de repositorios los repos de Google. estos reporitorios que se agregan son supuestamente para las actualizaciones del sistema, el detalle esta en que si nos da la gana de borrarlos se vienen y se instalan solos de nuevo al dia siguiente !!!.

Es por esto que es preferible usar el navegador Chromium en vez de Google Chrome, ademas asi podemos asegurarnos que estamos usando software 100% libre :D

Para instalar Chromium tan solo debemos agregar estos repos oficiales a nuestra lista de repositorios.

Abrimos la terminal y tecleamos:

[bash] sudo gedit /etc/apt/sources.list [/bash]

para abrir la lista de repositorios, y agregamos los repos

[bash] deb http://ppa.launchpad.net/chromium-daily/ppa/ubuntu karmic main
 deb-src http://ppa.launchpad.net/chromium-daily/ppa/ubuntu karmic main [/bash]

Guardamos y salimos.

Ahora tecleamos en la terminal

[bash] sudo apt-get update [/bash]

para actualizar la lista de paquetes.

Ahora para instalar chromium tecleamos:

[bash] sudo apt-get install chromium-browser [/bash]

y listo! tendremos nuestro navegador  instalado y listo para usar.

Saludos.
