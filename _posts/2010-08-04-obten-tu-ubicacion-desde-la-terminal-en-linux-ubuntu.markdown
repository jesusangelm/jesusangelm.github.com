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
{% include JB/setup %}

Navegando por internet me encontre con este script escrito en Bash  que nos permite obtener nuestra ubicacion con tan solo ejecutarlo en la terminal.

{% highlight bash %}
/bin/echo '{"version": "1.1.0","host": "maps.<a title="google" href="http://blog.jam.net.ve/tag/google/">google</a>.com","request_address": true,"address_language": "en_GB", "wifi_towers": [{"mac_address": "' $( iwlist wlan0 scan | grep Address | head -1 | awk '{print $5}' | sed -e 's/ //g' ) '","signal_strength": 8,"age": 0}]}'  | sed -e 's/" /"/' -e 's/ "/"/g' > /tmp/post.$$ && curl -X POST -d @/tmp/post.$$ http://www.google.com/loc/json | sed -e 's/{/n/g' -e 's/,/n/g'
{% endhighlight %}

Hay que tener en cuenta de que para que el script funcione correctamente se debe:

- Ejecutar como usuario Root, tecleando sudo antes del script

- Deberias estar conectado a una punto de acceso inalambrico Wi-Fi

- El adaptador de red inalambrico de tu pc debe llamarse wlan0 si no es tu caso cambialo en el script.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-4.png"><img class="aligncenter" src="http://blog.jam.net.ve/imagenes/uploads/2010/08/Pantallazo-4-300x93.png" alt="" width="366" height="113" /></a>

Saludos y espero les sirva...
