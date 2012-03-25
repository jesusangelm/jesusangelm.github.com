---
layout: post
title: !binary |-
  T2J0ZW4gdHUgVWJpY2FjaW9uIGRlc2RlIGxhIHRlcm1pbmFsIGVuIExpbnV4
  IC0gVWJ1bnR1
tags:
- !binary |-
  Z29vZ2xl
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  bWJy
- !binary |-
  Z2VvbG9j
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  bG9jYWxpemFjaW9u
- !binary |-
  Z3Bz
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
---
Navegando por internet me encontre con este script escrito en Bash  que nos permite obtener nuestra ubicacion con tan solo ejecutarlo en la terminal.

[bash] /bin/echo '{&quot;version&quot;: &quot;1.1.0&quot;,&quot;host&quot;: &quot;maps.google.com&quot;,&quot;request_address&quot;: true,&quot;address_language&quot;: &quot;en_GB&quot;, &quot;wifi_towers&quot;: [{&quot;mac_address&quot;: &quot;' $( iwlist wlan0 scan | grep Address | head -1 | awk '{print $5}' | sed -e 's/ //g' ) '&quot;,&quot;signal_strength&quot;: 8,&quot;age&quot;: 0}]}'  | sed -e 's/&quot; /&quot;/' -e 's/ &quot;/&quot;/g' &gt; /tmp/post.$$ &amp;&amp; curl -X POST -d @/tmp/post.$$ http://www.google.com/loc/json | sed -e 's/{/\n/g' -e 's/,/\n/g' [/bash]

Hay que tener en cuenta de que para que el script funcione correctamente se debe:

- Ejecutar como usuario Root, tecleando sudo antes del script

- Deberias estar conectado a una punto de acceso inalambrico Wi-Fi

- El adaptador de red inalambrico de tu pc debe llamarse wlan0 , si no es tu caso cambialo en el script.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-4.png"><img class="size-medium wp-image-353 alignleft" title="Pantallazo-4" src="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-4-300x93.png" alt="" width="366" height="113" /></a>

Saludos y espero les sirva...
