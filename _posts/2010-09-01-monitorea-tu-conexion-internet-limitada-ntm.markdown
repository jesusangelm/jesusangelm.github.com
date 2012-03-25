---
layout: post
title: !binary |-
  TW9uaXRvcmVhIHR1IGNvbmV4aW9uIGEgaW50ZXJuZXQgTGltaXRhZGEgY29u
  IE5UTQ==
tags:
- !binary |-
  ZGlnaXRlbA==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bW9kZW0=
- !binary |-
  dWJ1bnR1
- !binary |-
  dXNi
- !binary |-
  bWFudWFs
- !binary |-
  bW9uaXRvcg==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  dGVybWluYWw=
---
Si eres de los que posees una conexion a internet con limites de datos, sesiones o algun tipo de horario y no la monitoreas bien o te es engorroso hacerlo de manera manual, de seguro mas de una vez has tenido que pagar sobreprecio por el tiempo o datos extras de conexion. Para facilitarnos la labor de llevar las cuentas en cuanto a los datos consumidos nos viene bien la aplicacion <a href="http://netramon.sourceforge.net/eng/index.html">NTM</a> (Network Traffic Monitor).

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/09/Pantallazo-27.png"><img class="aligncenter size-full wp-image-386" title="Pantallazo-27" src="http://blog.jam.net.ve/imagenes/uploads/2010/09/Pantallazo-27.png" alt="" width="157" height="180" /></a>

NTM lo podemos configurar de acuerdo a las restrinciones de nuestro proveedor a internet para que ella misma monitoree la actividad y nos corte el internet cuando ya hallamos alcanzado el limite impuesto por nuestros ISP. Por ejemplo los usuarios de modems USB 3G HSDPA con planes de datos les vienen como anillo al dedo para asi no pasarse en el consumo de datos y no pagar cargos extras.

Para instalar NTM en Ubuntu tan solo debemos descargarnos el <a href="http://sourceforge.net/projects/netramon/">paquete .deb</a> y luego instalarlo haciendo doble click o escribiendo en la terminal:

[bash] sudo dpkg -i ntm-1.2.2.deb.deb [/bash]

Para ejecutarlo tan solo debemos ir a menu Aplicaciones - Internet - NTM

Si no se ejecuta correctamente teclea en la terminal:

[bash] sudo ntm [/bash]

Saludos y espero les sirva.
