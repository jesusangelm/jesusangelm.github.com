---
layout: post
title: !binary |-
  RWxpbWluYXIgR1JVQiBkZSBVYnVudHUgZW4gbGFwdG9wIGNvbiBXaW5kb3dz
  IFZpc3RhLg==
tags:
- !binary |-
  dWJ1bnR1
- !binary |-
  d2luZG93cw==
- !binary |-
  cG9ydGF0aWw=
- !binary |-
  YWN0dWFsaXphY2lvbg==
- !binary |-
  dmlzdGE=
- !binary |-
  Z3J1Yg==
- !binary |-
  bWJy
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  b3BlcmE=
- !binary |-
  YmFzaA==
- !binary |-
  Y29udHJhc2XDsWE=
- !binary |-
  bGFwdG9w
---
Bueno como hace unos dias comente, instale Ubuntu 9.10 en mi laptop HP Pavilion DV7-1243cl    pero lamentablemente y luego de una actualizacion, el Ubuntu no me queria arrancar.  Luego de buscar y buscar no pude encontrar ninguna solucion factible por lo que tube que optar por eliminar la particion de Ubuntu.

Pues aqui es donde viene un pequeño inconveniente, y es que con borrar la particion de Ubuntu (ext4)  y la de Intercambio (Swap), no se borra o recupera el arranque de windows vista que trae por defecto la portatil, probocando asi un error al intentar iniciarla e impidiendo entrar en el sistema operativo.

Lo bueno es que esto al parecer es relativamente facil de solucionarlo (al menos en mi caso) pues solo tube que arrancar la laptop desde una particion de recuperacion que trae esta portatil HP (casi todas las portatiles traen esta particion), entrar en una consola de recuperacion y teclar un comando para que eliminara y reestableciera el arranque de Vista.

Lo que exactamente hice fue:

-Arrancar la laptop desde la particion  de recuperacion que trae junto con el Windows Vista.

- Nos pedira en una de las ventanasla contraseña del usuario/administrador del sistema.

-Una vez dentro del sistema de recuperacion,  abrimos la consola de recuperacion.

-Dentro de la consola escribimos

[bash] BOOTREC /FIXMBR [/bash]

nos debe aparecer un mensaje que nos indique que se realizo correctamente.

Con esto se elimino el GRUB de Ubuntu y se restablecio el inicio automatico de Windows Vista.

cabe destacar como dije arriba que en mi caso la PC tiene una particion de recuperacion por lo que solo tube que arrancar desde ella, pero e leido por alli que tambien es posible hacerlo si se tiene el disco de recuperacion de Windows Vista (creo que lo traen algunas laptops o en mi caso se puede quemar copiando el contenido de la particion de recuperacion).

Saludos.
