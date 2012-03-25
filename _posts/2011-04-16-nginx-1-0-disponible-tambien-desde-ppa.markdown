---
layout: post
title: !binary |-
  TmdpbnggMS4wIGRpc3BvbmlibGUgLSB0YW1iaWVuIGRlc2RlIFBQQQ==
tags:
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  cHJvZ3JhbWFz
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  c29mdHdhcmU=
- !binary |-
  dWJ1bnR1
- !binary |-
  bmdpbng=
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  d2Vi
---
Nginx es un potente y ligero servidor web/proxy inverso ligero de alto rendimiento y un proxy para protocolos de correo electrónico (IMAP/POP3). El desarrollo de Nginx se inició hace aproximadamente 9 años. La primera versión pública 0.1.0 fue liberada el 4 de octubre de 2004.  Ahora y luego de cerca de 9 años se libera la versión 1.0.  Ya aquí en <a title="JamUnix Blog" href="http://blog.jam.net.ve" target="_blank">JamUnix Blog</a> les he hablado de Nginx y he publicado varios artículos sobre como instalarlo en CentOS y Ubuntu, por lo que en esta ocasión solo les mostrare como instalarlo a travez del PPA.

&nbsp;

<a href="http://blog.jam.net.ve/imagenes/uploads/2011/01/Nginx-logo.png"><img class="aligncenter size-medium wp-image-583" title="Nginx-logo" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Nginx-logo-300x65.png" alt="" width="300" height="65" /></a>

&nbsp;

<strong>Instalando Nginx Mediante PPA:</strong>

tan solo debemos agregar el siguiente repositorio, actualizar el listado de paquetes e instalando Nginx tecleando en la terminal:
<pre lang="php" line="1" escaped="true">sudo add-apt-repository ppa:nginx/stable
sudo apt-get update
sudo apt-get install nginx</pre>
Instalando desde los fuentes:

- Primero que nada debemos <a title="instalar" href="../tag/instalar/">instalar</a> (en caso de que no las tengas todavía) algunas dependencias para <strong>Nginx</strong>.
<pre lang="bash" line="1" escaped="true">sudo aptitude install  build-essential libpcre3 libpcre3-dev libssl-dev</pre>
- Luego nos movemos a la carpeta <strong>/opt</strong>, nos descargamos los fuentes, descomprimimos, compilamos e instalamos <strong>Nginx</strong>.
<pre lang="bash" line="1" escaped="true">cd /opt
sudo wget http://nginx.org/download/nginx-1.0.0.tar.gz
sudo tar -zxvf nginx-1.0.0.tar.gz
cd nginx-1.0.0/
./configure --prefix=/opt/nginx --user=nginx --group=nginx --with-http_ssl_module
sudo make
sudo make install</pre>
- Agregamos un usuario para <strong>Nginx</strong>:
<pre lang="bash" line="1" escaped="true">adduser --system --no-create-home --disabled-login --disabled-password --group nginx</pre>
<strong>Notese:</strong> que el directorio donde se encuentra instalado es <strong>/opt/<strong>nginx</strong></strong>

- Ahora necesitamos un init script para poder iniciar y detener nuestro servidor <strong>Nginx</strong>, uno muy bueno que podemos <a title="descargar" href="../tag/descargar/">descargar</a>, instalar y usar es:
<pre lang="bash" line="1" escaped="true">sudo wget https://library.linode.com/web-servers/nginx/installation/reference/init-deb.sh
sudo mv init-deb.sh /etc/init.d/nginx
sudo chmod +x /etc/init.d/nginx
/usr/sbin/update-rc.d -f nginx defaults
/etc/init.d/nginx start</pre>
&nbsp;

a partir de ahora podemos usar:
<pre lang="bash" line="1" escaped="true">sudo service nginx start
sudo service nginx stop</pre>
para iniciar y detener <strong>Nginx</strong>.

Y ya con esto tendremos instalado y funcionando la nueva versión del ligero servidor web Nginx

Para mayor información sobre configuraciones adicionales visita la <a href="http://wiki.nginx.org/" target="_blank">Wiki de Nginx</a>
