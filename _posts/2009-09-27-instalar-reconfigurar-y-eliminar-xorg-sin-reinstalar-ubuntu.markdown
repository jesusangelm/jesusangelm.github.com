---
layout: post
category: Ubuntu
title: !binary |-
  SW5zdGFsYXIsIFJlY29uZmlndXJhciB5IEVsaW1pbmFyIFhvcmcgc2luIFJl
  aW5zdGFsYXIgVWJ1bnR1Lg==
tags:
- !binary |-
  dWJ1bnR1
- !binary |-
  d2luZG93cw==
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  cmVzdGF1cmFjaW9u
- !binary |-
  eG9yZw==
---
X.Org es una implementación de código abierto del sistema X Windows System.   Para instalar, configurar o eliminar xorg sin reinstalar Ubuntu tan solo abre la consola y teclea el comando segun sea tu caso:

-  Instalar Xorg

{% highlight bash %}
$ sudo apt-get install xserver-xorg
{% endhighlight %}

- Configurar Xorg

{% highlight bash %}
$ sudo dpkg-reconfigure xserver-xorg
{% endhighlight %}

- Eliminar Xorg

{% highlight bash %}
$ sudo apt-get remove --purge xserver-xorg
{% endhighlight %}

Espero les sea de utilidad.

Fuente: <a href="http://www.ubuntugeek.com/ubuntu-tiphow-to-removeinstall-and-reconfigure-xorg-without-reinstalling-ubuntu.html" target="_blank">UbuntuGeek</a>
