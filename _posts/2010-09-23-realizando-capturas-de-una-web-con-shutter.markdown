---
layout: post
title: !binary |-
  UmVhbGl6YW5kbyBjYXB0dXJhcyBkZSB1bmEgd2ViIGNvbiBTaHV0dGVy
tags:
- !binary |-
  YmxvZw==
- !binary |-
  Z25vbWU=
- !binary |-
  bGludXg=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  dWJ1bnR1
- !binary |-
  Y2FwdHVyYXM=
- !binary |-
  bW9uaXRvcg==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  ZXNjcml0b3Jpbw==
- !binary |-
  YmFzaA==
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
---
{% include JB/setup %}

Shutter es una de las mejores herreamientas que hay en Linux para realizar capturas por sus cantidad de caracteristicas y facilidad de uso. Con Shutter podemos realizar capturas de pantalla del escritorio completo, solo una seleccion, una ventana, secciones de una ventana, un menu, textos de ayuda y capturas de sitios web entre otras caracteristicas.

Primero que nada debemos instalar Shutter si no lo tenemos, por lo que debemos teclear en la terminal:

{% highlight bash %}
sudo apt-get install shutter
{% endhighlight %}

Con esto tendremos instalado Shutter, pero si se fijan, la opcion de capturas de sitios web esta desabilitada y nos dice que tenemos que instalar un paquete gnome-web-photo. Pues bien lo instalamos tecleando en la terminal:

{% highlight bash %}
sudo apt-get install gnome-web-photo
{% endhighlight %}

y con esto tendremos habilitada la opcion de capturas web.

Bien para realizar la captura a un sitio web abrimos Shutter:

Aplicaciones > Accesorios > Shutter

Nota: Antes que nada deberiamos configurar el ancho del navegador virtual que usara Shutter para realizar una correcta captura. Por lo que luego de abrir Shutter nos vamos a:

Editar > Preferencias. y seleccionamos la pestaña "Avanzado"

Al final de la ventana esta la opcion "ancho del navegador virtual" en ella podremos seleccionar el ancho de nuestro monitor.

Continuamos, para realizar la captura hacemos click en la opcion respectiva (icono del planeta tierra)

Una vez seleccionada la opcion se nos abrira una ventana que nos pide la URL de la pagina web a capturar, bien colocamos la direccion de la pagina que deseamos capturar como por ejemplo:

{% highlight bash %}
http://blog.jam.net.ve
{% endhighlight %}

y le damos a "Capturar"

Ya con esto Shutter procesara la pagina y realizara la captura respectiva.  y lo que nos devolvera seria algo como esto:

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/09/blog-jamunix.jpg"><img class="aligncenter size-medium wp-image-425" title="blog-jamunix" src="http://blog.jam.net.ve/imagenes/uploads/2010/09/blog-jamunix-63x300.jpg" alt="" width="63" height="300" /></a>

Saludos y espero les sirva!
