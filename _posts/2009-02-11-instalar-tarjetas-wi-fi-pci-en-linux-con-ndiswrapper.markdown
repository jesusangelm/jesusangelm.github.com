---
layout: post
title: !binary |-
  SW5zdGFsYXIgVGFyamV0YXMgV2ktRmkgUENJIGVuIExpbnV4IGNvbiBOZGlz
  V3JhcHBlcg==
tags:
- !binary |-
  ZHJpdmVycw==
- !binary |-
  Z3VpYQ==
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  d2lmaQ==
- !binary |-
  d2luZG93cw==
- !binary |-
  bWJy
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  cmVk
- !binary |-
  c2lzdGVtYXM=
---
Muchas tarjetas PCI Wi-Fi y/o chips Wi-Fi integrados en tu pc no tienen drivers nativos para linux, por lo que usarlos en tu distro favorita puede que sea imposible.

Pero en realidad no lo es ya que en Linux existe una aplicacion llamada <a title="NdisWrapper en el SourceForge" href="http://sourceforge.net/projects/ndiswrapper/" target="_blank">NdisWrapper</a>.  Esta aplicacion permite usar los dirvers de tu tarjeta Wi-Fi para Windows, en Linux !!!!  por lo que se traduce en instalar tus drivers Wi-Fi de Windows en Linux.

Para instalar este programa tan solo busca en tu gestor de paquetes los siguientes paquetes:

<code>ndiswrapper-common
ndiswrapper-modules-1.9
ndiswrapper-utils-1.9</code>

o simplemente teclea en la consola esta linea:
<code>$ sudo aptitude install ndiswrapper-common ndiswrapper-modules-1.9 ndiswrapper-utils-1.9</code>

Una vez instalado en tu PC busca tus drivers de la tarjeta Wi-Fi para Windows y encuentra el archivo con extencion .INF.

Abre el Programa (En Ubuntu 8.10 se alla en Sistemas/Administracion/Controladores ParaRedes Inalambricas de Windows).

Luego dale click a "Instalar Nuevo Controlador" y ubica el archivo .INF que buscamos antes y luego "Instalar".

Si todo a salido bien, ya deberias poder usar tu tarjeta Wi-Fi en Linux :-)

Para mas informacion de como instalar el programa y tus drivers visita esta <a title="Guia Instalacion de NdisWrapper en Guias-Ubuntu.org" href="http://www.guia-ubuntu.org/index.php?title=Instalar_driver_de_tarjetas_WIFI_con_Ndiswrapper" target="_blank">Guia de NdisWrapper</a>
