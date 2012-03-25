---
layout: post
title: !binary |-
  SW5zdGFsYSBYYW1wcCBlbiBVYnVudHUgOC4xMA==
excerpt: !binary |-
  U2kgZXJlcyBwcm9ncmFtYWRvciB3ZWIgbyAgcXVpZXJlcyBwcm9iYXIgYWxn
  dW4gQ01TIGNvbW8gSm9vbWxhIG8gV29yZHByZXNzIGVuIHR1IFBDIGFudGVz
  IGRlIGRlY2lkaXJ0ZSBhIHVzYXJsbywgbyBzaW1wbGVtZW50ZSBxdWllcmVz
  IHRlbmVyIHVuYSBjb3BpYSBleGFjdGEgZGUgdHVzIHNjcmlwdCBwaHAgY29y
  cmllbmRvIGVuIHR1IGNvbXB1dGFkb3JhIGxvIG1hcyByZWNvbWVuZGFibGUg
  ZXMgcXVlIGluc3RhbGVzIHVuIHByb2dyYW1hIHF1ZSBjb25maWd1cmUgdG9k
  byB1biBzZXJ2aWRvciB3ZWIgY29ycmllbmRvIGVuIHR1IFBDLCB5IFhhbXBw
  IGhhY2UgZXNvIHBvc2libGUu
tags:
- !binary |-
  Y29ycmVv
- !binary |-
  bGludXg=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  dWJ1bnR1
- !binary |-
  eGFtcHA=
- !binary |-
  bXlzcWw=
- !binary |-
  cGhw
- !binary |-
  cGhwbXlhZG1pbg==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFzaA==
- !binary |-
  d2Vi
- !binary |-
  dGVybWluYWw=
---
Xampp es una aplicacion que instala y configura en tu maquina todo lo necesario para tener un servidor funcional como el servidor web Apache, Lenguaje PHP, Bases de datos MySql y su interfaz web PhpMyAdmin, pero xampp va mas alla e incluye tambien lenguaje Perl, el servidor FTP ProFTPD, servidor de correos y muchos mas.

Para instalar Xampp en nuestro Ubuntu tan solo debemos ir a la web de <a title="Web Oficial Xampp" href="http://www.apachefriends.org/en/xampp-linux.html" target="_blank">ApacheFriends</a> y descargarlo (version actual 1.7 al momento de escribir esto).

Una vez descargado hay que descomprimir para instalar, debemos abrir la consola o terminal, cambiar con el comando <strong><em>CD</em></strong> al directorio donde lo guardamos y loguearnos como Root con el comando <strong><em>SU</em></strong>, o simplemente   tecleamos

[bash] sudo tar xvfz xampp-linux-1.7.tar.gz -C /opt [/bash]

Esto descomprime el archivo descargado y lo copia en el directorio <strong>/opt</strong> quedando asi <strong>/opt/lampp</strong>

Ahora solo nos resta iniciar Xampp, lo haremos tecleando en la consola

[bash] /opt/lampp/lampp start [/bash]
<blockquote><tt></tt></blockquote>
<blockquote><tt></tt></blockquote>
Si todo a ido bien nos mostrara un texto como este:

<tt></tt>

[bash]Starting XAMPP 1.7...
LAMPP: Starting Apache...
LAMPP: Starting MySQL...
LAMPP started.[/bash]

<tt></tt>

Si ves esto en la terminal, FELICITACIONES !!! tienes Xampp corriendo en tu PC, ahora solo teclea en el navegador

[bash] http://localhost [/bash]

y veras la pagina principal de Xampp.

Si deseas detener xampp tan solo teclea en la consola

[bash] /opt/lampp/lampp stop [/bash]

Si te aburriste, (aunque no lo creo) y quieres desintalar xampp solo teclea en la consola

[bash] rm -rf /opt/lampp[/bash]
<blockquote><tt></tt></blockquote>
<blockquote><tt></tt></blockquote>
Espero le sirva a alguien esta breve explicacion.  :)
