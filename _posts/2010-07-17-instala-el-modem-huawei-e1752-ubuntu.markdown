---
layout: post
title: !binary |-
  SW5zdGFsYSBlbCBNb2RlbSBIdWF3ZWkgRTE3NTIgZW4gVWJ1bnR1
tags:
- !binary |-
  YmxvZw==
- !binary |-
  ZGlnaXRlbA==
- !binary |-
  ZHJpdmVycw==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  bW9kZW0=
- !binary |-
  dWJ1bnR1
- !binary |-
  dXNi
- !binary |-
  d2luZG93cw==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  ZXNjcml0b3Jpbw==
- !binary |-
  b3BlcmE=
- !binary |-
  aHVhd2Vp
- !binary |-
  YmFzaA==
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
---
He vuelto a mi querido Ubuntu! :-)

Como muchos de los que leen este blog sabe (-0.000001 lectores y bajando) tenia un <a href="http://blog.jam.net.ve/2009/08/09/%c2%bfproblemas-para-conectar-tu-modem-zte-mf626-en-ubuntu-prueba-este-metodo/" target="_blank">modem ZTE MF626</a> de Digitel el cual usaba en Ubuntu, pero este mismo me comenzo a fallar este domingo ya que no detectaba las redes 3G de ninguna operadora.  Luego de dias de esperar respuestas por parte de Digitel y gracias a la gente de <a href="http://www.con-cafe.com/" target="_blank">Con-Cafe</a> quien me ayudo a escalar mi caso con Digitel, porfin solucionaron mi inconveniente y me reemplazaron el modem por un Huawei E1752 (el ZTE al parecer habia muerto).

Bien ahora que tengo un nuevo modem llego la hora de hacerlo funcionar en Ubuntu. Unas de las complicaciones que tenia el modem ZTE MF626 era que para usarlo en Ubuntu necesitaba hacer unas cuantas configuraciones (he leido que algunas personas les funcionaba tan solo conectar, pero este nunca fue mi caso) las cuales si corria con suerte funcionarian y harian que el modem trabajara sin problemas; bueno casi sin problemas pues a mi se me desconectaba cada hora debido a que el demonio PPP se pegaba dos tiros el mismo :-S

El Huawei E1752 no requiere de tantas maromas con la terminal y otras configuraciones ya que para poderlo usar basta con instalar un paquete requerido, conectar el modem, expulsar el dispositivo de almacenamiento incluido en el y conectarse con NetworkManager a internet :-D

Bien para hacer esto y poner a trabajar el modem en Ubuntu les detallo mas los pasos:

- instalamos USB_Modeswitch tecleando en la terminal

[bash] sudo apt-get install usb-modeswitch [/bash]

Si tienes problemas para descargarlo o no aparece en tu lista de paquetes puedes bajarlo desde la web del desarrollador haciendo click <a href="http://www.draisberghof.de/usb_modeswitch/#download" target="_blank">aqui</a>.

- una vez instalado el paquete conectamos el modem a la pc, nos aparecera un icono en el escritorio el cual es la unidad de almacenamiento del modem donde estan los drivers para Windows. Le damos click derecho y le damos a Expulsr de manera segura.

- Luego de esto ve al icono de redes de NetworkManager y haz click izquierdo en el, aparecera "Digitel Tim Predeterminado" dale click alli y comenzara a conectarse a internet.

Si todo a ido bien ya deberias poder navegar usando redes 3G HSDPA con el Modem.

No lo e probado en otras distribuciones todavia, pero viendo lo sencillo de la instacion y puesta en funcionamiento es probable que funcione para otras distros siempre y cuando tengas instalado el paquete usb-modeswitch.

Saludos y espero les sirva.
