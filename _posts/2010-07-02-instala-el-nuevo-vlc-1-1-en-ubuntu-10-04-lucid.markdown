---
layout: post
title: !binary |-
  SW5zdGFsYSBlbCBudWV2byBWTEMgMS4xIGVuIFVidW50dSAxMC4wNCBMdWNp
  ZCA=
tags:
- !binary |-
  YmxvZw==
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  dWJ1bnR1
- !binary |-
  bHVjaWQ=
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  dmxj
- !binary |-
  cmVwcm9kdWN0b3I=
- !binary |-
  dmlkZW8=
- !binary |-
  YmFzaA==
- !binary |-
  dGVybWluYWw=
---
Creo que este post llega algo tarde puesto que ya VLC 1.1 salio hace ya unas semanitas y puede que ya muchos lo tengan instalado y lo esten disfrutando mucho, pero en fin, no eh tenido mucho tiempo ultimamente para el blog asi que de todos modos les explico como instalarlo si todavia no lo han hecho.

VLC 1.1 viene con una novedad muy jugoza y es que ahora soporta aceleracion por hadware, es decir, por medio de la tarjeta grafica puede hacer que los videos se procecen por medio de tu trajeta grafica liberando asi esa cargas al procesador.  Esta funcion esta muy de moda ultimamente ya que se esta buscando implementar tambien en los navegadores y otras aplicaciones que todavia no contaban con dicha caracteristica.

Bien para instalar el nuevo VLC 1.1 tan solo debes agregar el siguiente repositorio tecleando en la terminal:

[bash] sudo add-apt-repository ppa:c-korn/vlc [/bash]

Luego de esto actualizamos la lista de paquetes tecleando:

[bash] sudo apt-get update [/bash]

despues tan solo instalamos el nuevo VLC tecleando:

[bash] sudo apt-get install vlc mozilla-plugin-vlc [/bash]

Bien despues de esto ya tendras VLC instalado y listo para utilizar.

Espero les sirva! :-P
