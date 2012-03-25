---
layout: post
title: !binary |-
  TW9udGFuZG8gUGFydGljaW9uZXMgTlRGUyBlbiBMaW51eA==
tags:
- !binary |-
  YmxvZw==
- !binary |-
  ZGViaWFu
- !binary |-
  amFtdW5peA==
- !binary |-
  bGludXg=
- !binary |-
  cmVzcGFsZG8=
- !binary |-
  dWJ1bnR1
- !binary |-
  dW5peA==
- !binary |-
  bWJy
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  dGVybWluYWw=
- !binary |-
  bG9ncw==
- !binary |-
  bnRmcw==
- !binary |-
  cGFydGljaW9u
---
Esto es algo que ya hay en muchos blogs, foros, etc...  pero lo coloco aqui en <a href="http://blog.jam.net.ve/" target="_blank">JamUnix Blog</a> a modo de respaldo para tenerlo a mano cuando lo necesite ya que cuando instalo una nueva version de <a href="http://blog.jam.net.ve/category/ubuntu/" target="_blank">Ubuntu</a> u otra distro como Debian o Arch <a href="http://blog.jam.net.ve/category/linux/">Linux</a>, siempre ando buscando como automontar mis particiones NTFS.

Bien comencemos, para automontar particiones usaremos la aplicacion ntfs-3g la cual nos facilitara mucho la tarea, por lo que lo primero que haremos sera instalarla tecleando en una terminal:
<pre lang="bash" line="1" escaped="true">sudo aptitude install ntfs-3g</pre>
Luego de esto creamos una carpeta llamada "jamunixNTFS"en /media en la cual montaremos la particion NTFS.  Por supuesto podemos colocarle el nombre que queramos a la carpeta.
<pre lang="bash" line="1" escaped="true">mkdir /media/jamunixNTFS</pre>
Ahora debemos averiguar en donde se encuentra nuestra particion NTFS a montar, para ver esto tecleamos en la terminal:
<pre lang="bash" line="1" escaped="true">sudo fdisk -l</pre>
Esto nos mostrara un listado de las particiones que tenemos, es algo similar a esto:
<pre lang="text" line="1" escaped="true">Dispositivo Inicio    Comienzo      Fin      Bloques  Id  Sistema
/dev/sda1   *           1          13      102400    7  HPFS/NTFS
La partición 1 no termina en un límite de cilindro.
/dev/sda2              13       25843   207478784    7  HPFS/NTFS
/dev/sda3           25843       31984    49324032   83  Linux
/dev/sda4           31984       38914    55663617    5  Extendida
/dev/sda5           31984       32233     1998848   82  Linux swap / Solaris
/dev/sda6           32233       38914    53663744   83  Linux</pre>
Como podemos ver tenemos 2 particiones NTFS sda1 y sda2, y la que yo configurare para que se automonte sera la sda2.

Para hacer dicho montaje de la particion /dev/sda2 en la carpeta /media/jamunixNTFS que ya creamos mas arriba, tecleamos en la terminal:
<pre lang="bash" line="1" escaped="true">mount -t ntfs-3g /dev/sda2 /media/jamunixNTFS</pre>
Ya con esto tendremos montada nuestra particion NTFS.

Ahora haremos una configuracion mas para que se automonte la particion cada vez que iniciemos el S.O para esto editaremos el archivo fstab tecleando en la terminal:
<pre lang="bash" line="1" escaped="true">sudo gedit /etc/fstab</pre>
y agregamos la siguiente linea al final del archivo:
<pre lang="bash" line="1" escaped="true">/dev/sda2 /media/jamunixNTFS ntfs-3g defaults,locale=es_ES.UTF8 0 0</pre>
guardamos, cerramos y reiniciamos para ver al siguiente inicio nuestra particion NTFS montada de manera automatica.

Saludos y espero les sirva tanto como a mi.
