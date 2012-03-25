---
layout: post
title: !binary |-
  SW5zdGFsYXIgY29kZWMgbXVsdGltZWRpYSBlbiBVYnVudHUgOS4wNCBKYXVu
  dHk=
tags:
- !binary |-
  Y29kZWM=
- !binary |-
  amF1bnR5
- !binary |-
  bGludXg=
- !binary |-
  bXVsdGltZWRpYQ==
- !binary |-
  dWJ1bnR1
- !binary |-
  d2luZG93cw==
- !binary |-
  YXVkaW8=
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  cmVwcm9kdWN0b3I=
- !binary |-
  dmlkZW8=
- !binary |-
  dGVybWluYWw=
- !binary |-
  YXJjaGl2b3M=
---
Una de las primeras cosas que se debe hacer despues de instalar Ubuntu, es instalar los codecs multimedia restringidos para los principales formatos de audio y video.

Para hacer esto solo debemos:  Agregar las siguientes repositorios en la lista de repositorios en /etc/apt/sources.list tan solo debemos teclear:
<blockquote>sudo gedit /etc/apt/sources.list</blockquote>
y agregar estas listas:

deb http://archive.ubuntu.com/ubuntu jaunty universe multiverse
deb-src http://archive.ubuntu.com/ubuntu jaunty universe multiverse

Luego guarda los cambios, dirigete a la terminal y teclea:
<blockquote>sudo apt-get update</blockquote>
Luego de esto, tendremos la posibilidad de instalar algunos reproductores recomendados tecleando en la terminal:
<blockquote>sudo apt-get install mplayer</blockquote>
Para instalar el Mplayer

Muy Bien, Ahora vamos con los Codecs, como en Linux los formatos de audio y videos usado son tipicamente OpenSource, el uso de Codecs Privativos es algo que va un poco en contra con la filosofia OpenSource en Linux, y por lo tanto estos codecs no estan disponibles en los repositorios oficiales de Ubuntu. De modo que debemos descargarlos de otros repositorios tecleando en la terminal:
<blockquote>sudo wget http://www.medibuntu.org/sources.list.d/jaunty.list <code>--</code>output-document=/etc/apt/sources.list.d/medibuntu.list</blockquote>
luego agregamos la llave GPG con el comando:
<blockquote>sudo apt-get install medibuntu-keyring</blockquote>
y luego actualizamos la lista con:
<blockquote>sudo apt-get update</blockquote>
Bien, Ahora si vamos a instalar los Codecs, Para usuarios de i386 ( 32Bits ) teclea en la terminal:
<blockquote>sudo apt-get install w32codecs libdvdcss2</blockquote>
y para usuarios amd64 ( 64Bits ) teclea en la terminal:
<blockquote>sudo apt-get install w64codecs libdvdcss2</blockquote>
Ahora si todo a salido bien deberias poder reproducir archivos multimedia como:

MPEG 1/2/4

DivX 3/4/5

Windows <a class="iAs" style="border-bottom: medium none ! important; font-weight: bold ! important; text-decoration: none ! important; padding-bottom: 0px ! important; color: darkblue ! important; background-color: transparent ! important; cursor: pointer ! important;" href="http://www.ubuntugeek.com/install-mplayer-and-multimedia-codecs-libdvdcss2w32codecsw64codecs-in-ubuntu-904-jaunty.html#" target="_blank"></a>Media 7/8/9

RealAudio/Video up to 9

Quicktime 5/6

Vivo 1/2.

MX/SSE (2)/3Dnow(Ex)

aw/divx/mpeg4 AVI (pcm/mp3 audio)
