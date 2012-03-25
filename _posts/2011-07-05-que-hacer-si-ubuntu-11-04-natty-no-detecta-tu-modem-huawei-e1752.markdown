---
layout: post
title: !binary |-
  UXVlIGhhY2VyIHNpIFVidW50dSAxMS4wNCBOYXR0eSBubyBkZXRlY3RhIHR1
  IE1vZGVtIEh1YXdlaSBFMTc1Mg==
tags:
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
  aHVhd2Vp
- !binary |-
  bmF0dHk=
- !binary |-
  bWF2ZXJpY2s=
- !binary |-
  dXNiX21vZGVzd2l0Y2g=
---
Anoche me puse a instalar Ubuntu 11.04 Natty 64bits en mi PC de escritorio que resucito hace como dos semanas luego de estar mas de un año sin usar. Luego de haber terminado la instalación de Ubuntu, (unos 15min o menos desde un LiveUSB) hice lo primero que siempre hago al instalar una distro: Conectarla a internet, para esto en mi caso uso son modem USB, tome mi Modem Huawei E1752 y lo conecte, pero a los pocos segundos Oh! :O note que algo no estaba bien, no veía la interfaz de red en la lista de NetworkManager :(

Tras un simple <strong>lsusb</strong> en la terminal, confirmo lo que imaginaba, no se me estaba detectando el Modem USB como eso: Modem USB, sino que estaba siendo reconocido simplemente como unidad de almacenamiento. como se que el encargado de cambiar el dispositivo de almacenamiento a Modem USB es <strong>usb-modeswitch</strong> me di una vuelta por Synaptycs para ver si estaba instalado el programa y que version. El sinaptycs me confirmo lo siguiente: efectivamente tenia usb-modeswitch instalado en la version 1.1.7.  revisando mi laptop con Ubuntu 10.10 64bits en donde el modem Huawei E1752 si se reconoce sin problemas veo que tengo instalado usb-modeswitch 1.1.4.

Bien esto me dio una idea, si desinstalo usb-modeswitch 1.1.7 e instalo la versión 1.1.4 en Ubuntu 11.04 Natty 64bits ¿lo reconocerá?. bueno la unica manera de saberlo es haciendolo, asi que desinstale usb-modeswitch 1.1.7 en Natty con un simple:
<pre lang="bash" line="1" escaped="true">sudo aptitude purge usb-modeswitch usb-modeswitch-data</pre>
una vez desinstalados me di a la tarea de instalar la version 1.1.4, en mi caso ya tenia un DVD de Ubuntu 10.10 Maverick 64bits por lo que solo tube que copiar el paquete usb-modeswitch y usb-modeswitch-data en la PC de escritorio e instalarlo con un simple:
<pre lang="bash" line="1" escaped="true">sudo dpkg -i usb-modeswitch-data_20100826-1_all.deb usb-modeswitch_1.1.4-1_amd64.deb</pre>
&nbsp;

Si en tu caso no tienes un DVD o CD donde esten los paquetes <a href="http://mirror.pnl.gov/ubuntu//pool/main/u/usb-modeswitch-data/usb-modeswitch-data_20100826-1_all.deb" target="_blank">usb-modeswitch-data</a> y <a href="http://mirror.pnl.gov/ubuntu//pool/main/u/usb-modeswitch/usb-modeswitch_1.1.4-1_amd64.deb" target="_blank">usb-modeswitch</a> lo puedes encontrar en <a href="http://packages.ubuntu.com/" target="_blank">Packages.ubuntu.com</a>

Una vez instalado los paquetes, reinicie la PC, y al volver a entrar a Ubuntu conecte el Modem Huawei E1752 y al cabo de unos segundos :D Ubuntu Natty reconoció y monto el dispositivo como modem USB,  despues de eso tan solo use el asistente de NetworkManager para configurar la conexión y en menos de unos minutos :D ya estaba navegando en Internet con el modem.
