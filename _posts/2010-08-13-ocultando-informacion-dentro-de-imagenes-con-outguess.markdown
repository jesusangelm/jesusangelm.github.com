---
layout: post
title: !binary |-
  T2N1bHRhbmRvIGluZm9ybWFjaW9uIGRlbnRybyBkZSBpbWFnZW5lcyBjb24g
  T3V0R3Vlc3M=
tags:
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  bWJy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  c2VndXJpZGFk
- !binary |-
  ZXN0ZWdhbm9ncmFmaWE=
- !binary |-
  ZW5jcmlwdGFjaW9u
- !binary |-
  Y29udHJhc2XDsWE=
- !binary |-
  dGVybWluYWw=
- !binary |-
  YXJjaGl2b3M=
---
Ultimamente e estado leyendo informacion sobre la seguridad en internet, linux y servidores y en una de estas me encontre <a href="http://www.outguess.org/">OutGuess</a> el cual es una sencilla aplicacion que nos permite encriptar informacion dentro de una imagen .jpg usando la <a href="http://es.wikipedia.org/wiki/Esteganograf%C3%ADa" target="_blank">Esteganografia</a>

Para instalarlo tan solo tecleamos en la terminal:

[bash] sudo apt-get install outguess [/bash]

Ahora bien OutGuess se usa por medio de la terminal, imaginemos que tenemos el archivo secreto.txt en el cual esta la informacion privada que queremos esconder (contraseñas, paginas pornos que visitas, el pin del Blackberry de binladen, etc) y una imagen-inocente.jpg cuaquiera la cual usaremos para insertar en ella la informacion que vamos a encriptar, para realizar esto debemos teclear en la terminal:

[bash] outguess -k &quot;contraseña&quot; -d secreto.txt imagen-inocente.jpg imagen-malvada.jpg [/bash]

en donde:

- contraseña es la contraseña que luego se usara para extraer la informacion que esta encriptada dentro de la imagen.

- secreto.txt es el archivo el cual contiene la informacion a encriptar.

- imagen-inocente.jpg es la imagen que se usara para insertar la informacion a encriptar

- imagen-malvada.jpg es el nombre de la imagen que nos va generar OutGuess con la informacion encriptada e insertada dentro (puedes colocar el nombre que quieras).

Como vemos esto nos va a generar una imagen-malvada.jpg el cual contiene la informacion encriptada, Ahora bien si deseamos extraer la informacion que esta oculta en esa imagen tan solo debemos teclear en la terminal:

[bash] outguess -k &quot;contraseña&quot; -r imagen-malvada.jpg secretofuera.txt [/bash]

En donde:

- contraseña es la contraseña necesaria para desencriptar la imagen (es la misma que se uso para encriptarla)

- imagen-malvada.jpg es el nombre de la imagen que tiene la informacion encriptada

- secretofuera.txt es el archivo que contiene la informacion que estaba encriptada dentro de la imagen (puedes colocar el nombre que quieras).

Con este comando nos creara el archivo  secretofuera.txt el cual contiene la informacion que estaba encriptada dentro de la imagen.

Tambien existe otra aplicacion llamada <a href="http://steghide.sourceforge.net/ ">StegHide</a> que va mas alla y nos permite encriptar informacion dentro de archivos de imagenes .bmp y de sonido .wav y .au  pero de este les comentare luego.

Saludos y espero les sirva.
