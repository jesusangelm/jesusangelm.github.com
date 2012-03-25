---
layout: post
title: !binary |-
  Q29uZmlndXJhciBNb2RlbSAzRyBIdWF3ZWkgRTE2MEUgRGlnaXRlbCBlbiBM
  aW51eA==
tags:
- !binary |-
  YmFt
- !binary |-
  ZGlnaXRlbA==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  bW9kZW0=
- !binary |-
  dXNi
- !binary |-
  bWF5bw==
- !binary |-
  aHVhd2Vp
- !binary |-
  cmVk
---
Bueno navegando por alli encontre este post para realizar la configuracion de la conexion a internet con los famosos Modems 3.5G  del servicio Bam de Digitel.

Tan solo debes conectar el Modem a tu Pc con Linux y

Al conectarlo veremos algo así:
<blockquote><code>USB Serial support registered for GSM modem (1-port)
option 1-5:1.0: GSM modem (1-port) converter detected
usb 1-5: GSM modem (1-port) converter now attached to ttyUSB0
option 1-5:1.1: GSM modem (1-port) converter detected
usb 1-5: GSM modem (1-port) converter now attached to ttyUSB1
usbcore: registered new interface driver option
option: v0.7.2:USB Driver for GSM modems</code></blockquote>
Luego, teniendo instalado wvdial, tenemos que configurar los datos para conectar, escribimos:
<blockquote><code>wvdialconf</code></blockquote>
Esto detectara el modem, y creará un archivo: <strong><em>/etc/wvdial.conf</em></strong>

Lo editamos solo un poco, acá un ejemplo:
<blockquote><code>[Dialer Defaults]
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &amp;C1 &amp;D2 +FCLASS=0
Phone = *99#
;ISDN = 0
Username = digitel
Password = 0000
Modem = /dev/ttyUSB0</code></blockquote>
Guardamos y listo, escribimos <strong><em>wvdial</em></strong> para conectar.

Segun el autor esta configuracion se hizo usando kernel 2.6.28 en archlinux, pero en las demás distros no debería existir mayor problema.

Fuente:  <a href="http://jhuss.com/2009/03/31/digitel-3g-con-huawei-e160e/" target="_blank">jhuss.com</a>
