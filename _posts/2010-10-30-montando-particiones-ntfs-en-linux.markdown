---
layout: post
title: "Montando particiones NTFS en Linux"
tags: [linux, tutorial]
---
# Montando particiones NTFS en Linux

{% include post_header.html %}

Esto es algo que ya hay en muchos blogs, foros, etc...  pero lo coloco aqui en <a href="http://blog.jam.net.ve/" target="_blank">JamUnix Blog</a> a modo de respaldo para tenerlo a mano cuando lo necesite ya que cuando instalo una nueva version de <a href="http://blog.jam.net.ve/category/ubuntu/" target="_blank">Ubuntu</a> u otra distro como Debian o Arch <a href="http://blog.jam.net.ve/category/linux/">Linux</a>, siempre ando buscando como automontar mis particiones NTFS.

Bien comencemos, para automontar particiones usaremos la aplicacion ntfs-3g la cual nos facilitara mucho la tarea, por lo que lo primero que haremos sera instalarla tecleando en una terminal:

{% highlight bash %}
sudo aptitude install ntfs-3g
{% endhighlight %}

Luego de esto creamos una carpeta llamada "JamNTFS"en /media en la cual montaremos la particion NTFS.  Por supuesto podemos colocarle el nombre que queramos a la carpeta.

{% highlight bash %}
mkdir /media/jamunixNTFS
{% endhighlight %}

Ahora debemos averiguar en donde se encuentra nuestra particion NTFS a montar, para ver esto tecleamos en la terminal:

{% highlight bash %}
sudo fdisk -l
{% endhighlight %}

Esto nos mostrara un listado de las particiones que tenemos, es algo similar a esto:

{% highlight bash %}
Dispositivo Inicio    Comienzo      Fin      Bloques  Id  Sistema
/dev/sda1   *           1          13      102400    7  HPFS/NTFS
La partición 1 no termina en un límite de cilindro.
/dev/sda2              13       25843   207478784    7  HPFS/NTFS
/dev/sda3           25843       31984    49324032   83  Linux
/dev/sda4           31984       38914    55663617    5  Extendida
/dev/sda5           31984       32233     1998848   82  Linux swap / Solaris
/dev/sda6           32233       38914    53663744   83  Linux
{% endhighlight %}

Como podemos ver tenemos 2 particiones NTFS sda1 y sda2, y la que yo configurare para que se automonte sera la sda2.

Para hacer dicho montaje de la particion /dev/sda2 en la carpeta /media/JamNTFS que ya creamos mas arriba, tecleamos en la terminal:

{% highlight bash %}
mount -t ntfs-3g /dev/sda2 /media/JamNTFS
{% endhighlight %}

Ya con esto tendremos montada nuestra particion NTFS.

Ahora haremos una configuracion mas para que se automonte la particion cada vez que iniciemos el S.O para esto editaremos el archivo fstab tecleando en la terminal:

{% highlight bash %}
sudo gedit /etc/fstab
{% endhighlight %}

y agregamos la siguiente linea al final del archivo:

{% highlight bash %}
/dev/sda2 /media/JamNTFS ntfs-3g defaults,locale=es_ES.UTF8 0 0
{% endhighlight %}

guardamos, cerramos y reiniciamos para ver al siguiente inicio nuestra particion NTFS montada de manera automatica.

Saludos y espero les sirva tanto como a mi.
