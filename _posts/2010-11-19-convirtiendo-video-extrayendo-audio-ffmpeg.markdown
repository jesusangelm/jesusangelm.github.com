---
layout: post
title: !binary |-
  Q29udmlydGllbmRvIHZpZGVvIHkgZXh0cmF5ZW5kbyBlbCBhdWRpbyBjb24g
  RkZtcGVn
tags:
- !binary |-
  Y29kZWM=
- !binary |-
  Z29vZ2xl
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  YXVkaW8=
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  dmlkZW8=
- !binary |-
  YmFzaA==
- !binary |-
  dGVybWluYWw=
- !binary |-
  Y29udmVyc2lvbg==
- !binary |-
  ZmZtcGVn
- !binary |-
  eW91dHViZQ==
---
Viendo un video de youtube en donde me gusto el audio mas que el mismo video me dio por buscar la manera de extraer ese audio. luego de una simple pregunta a San Google  este me ilumino con la respuesta de que podia usar FFmpeg para convertir el video y luego extraer el audio del mismo  y lo mejor de todo es que lo puedo hacer desde la terminal!!!

Para instalar FFmpeg tan solo tecleamos:
<pre lang="bash" line="1" escaped="true">sudo aptitude install ffmpeg</pre>
Ahora para convertir el video de youtube a otro formato tan solo debemos teclear en la terminal:
<pre lang="bash" line="1" escaped="true">ffmpeg -i videoyoutube -ab 256k convertidoa.avi</pre>
Como el fin de esta explicacion es extraer el audio, agregue el flag "-ab 256k" para que FFmpeg ajuste el bitrate de audio a 256kbps en lugar de los 64kbps que se usaria por defecto si no hago esta especificacion.

Para extraer el audio que esta en el video que se acaba de convertir lo podemos hacer tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">ffmpeg -i convertidoa.avi -vn -acodec copy extraido.mp3</pre>
con esto tendremos el archivo de audio extraido.mp3 el cual contiene solo el sonido del video de youtube.
