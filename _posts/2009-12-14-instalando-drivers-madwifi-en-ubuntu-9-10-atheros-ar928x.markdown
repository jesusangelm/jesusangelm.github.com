---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBEcml2ZXJzIE1hZHdpZmkgZW4gVWJ1bnR1IDkuMTAgKEF0
  aGVyb3MgQXI5MjhYKQ==
tags:
- !binary |-
  ZHJpdmVycw==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  d2lmaQ==
- !binary |-
  bWFudWFs
- !binary |-
  bWJy
- !binary |-
  aGFjaw==
- !binary |-
  bW9uaXRvcg==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFy
- !binary |-
  YmFzaA==
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
- !binary |-
  bGFwdG9w
---
{% include JB/setup %}

Hace unas semanas atras estaba comentando que habia instalado Ubuntu 9.10 en mi laptop y que estaba intentando colocar el chip inalambrico en modo monitor para hacer auditorias wifi (contra mi router), Por fin e logrado instalar los drivers Madwifi para mi tarjeta inalambrica la cual es una Atheros AR5009 o como en la web de Madwifi se conoce como AR928X.

Despues de buscar un manual o explicacion para instalarlos, la verdad encontre demasiadas formas de hacerlo, ademas de 3 drivers distintos que podia usar (compat-wireless-2.6.31-rc7, madwifi-hal-0.10.5.6-r4100-20090929 y el madwifi-0.9.4-current) me fui por la explicacion de la pagina <a title="Drivers para Ath9k" href="http://linuxwireless.org/en/users/Drivers/ath9k" target="_blank">LinuxWireless</a> e instale el driver madwifi-hal-0.10.5.6-r4100-20090929  ya que me parecio el mas completo de los tres (en realidad es el mas pesado 4.2Mb).

Para instalarlo solo:

- Descague el Drivers desde el <a href="http://snapshots.madwifi-project.org/" target="_blank">Snapshot de Madwifi</a>

- Luego Descomprimimos y abrimos la carpeta en la terminal

{% highlight bash %}
cd madwifi-hal-0.10.5.6-r4100-20090929
{% endhighlight %}

-Ahora  compilamos.

{% highlight bash %}
$ sudo make
{% endhighlight %}

y ahora instalamos

{% highlight bash %}
$ sudo make install
{% endhighlight %}

con esto ya deberia de tener corrctamente instalado los drivers.

pero como ando buscando es colocarlo en modo monitor entonces instale el Aircrack-ng:

{% highlight bash %}
$ sudo apt-get install aircrack-ng
{% endhighlight %}

y configure la inalambrica en modo monitor en la terminal:

{% highlight bash %}
airmon-ng start wlan0
{% endhighlight %}

con esto deberia de haber activado el modo monitor, para comprobarlo teclee en la terminal:

{% highlight bash %}
iwconfig
{% endhighlight %}

el cual me devolvio algo como esto:

{% highlight bash session %}
lo        no wireless extensions.
eth0      no wireless extensions.
wlan0     IEEE 802.11abgn  ESSID:&quot;Mi Router&quot;
 Mode:Managed  Frequency:2.437 GHz  Access Point: XX:XX:XX:XX:XX:XX
 Bit Rate=54 Mb/s   Tx-Power=20 dBm
 Retry  long limit:7   RTS thr:off   Fragment thr:off
 Power Management:on
 Link Quality=70/70  Signal level=-31 dBm
 Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
 Tx excessive retries:0  Invalid misc:0   Missed beacon:0

mon0      IEEE 802.11abgn  Mode:Monitor  Frequency:2.437 GHz  Tx-Power=20 dBm
 Retry  long limit:7   RTS thr:off   Fragment thr:off
 Power Management:on
{% endhighlight %}

notese que se agrego una nueva interfaz el cual se llama "mon0"  esta es la interfaz que se utilizara para trabajar en modo monitor, capturar e inyectar paquetes.

solo resta ahora instalar algunas otras herramientas al gusto de cada quien, en mi caso aparte de Aircrack instale Kismet el cual me instalo a la vez el WireShark. Con este ultimo puedo usar la interfaz mon0 como interfaz de captura para (valga la rebusnancia ) capturar paquetes.

Espero que les sirva esta info tanto como a mi.

Saludos.
