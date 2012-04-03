---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBOZ2lueCBjb24gc29wb3J0ZSBQSFA1IGVuIFVidW50dS4=
tags:
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  bmdpbng=
- !binary |-
  cGhw
- !binary |-
  ZmFzdGNnaQ==
---
{% include JB/setup %}

Hace unos meses atras escribi un articulo en el que explicaba como <a href="http://blog.jam.net.ve/2010/02/16/instalando-nginx-en-centos/">Instalar Nginx en CentOS</a>,  en aquellos tiempos tenia el servidor dedicado con CentOS en el que hacia las pruebas.  Ahora les paso a explicar como instalar el servicio web <a href="http://nginx.org/">Nginx</a> con soporte para PHP5 (a travez de <a href="http://php-fpm.org/">PHP-FPM</a> - Administrador de procesos FastCGI ) en <a href="http://blog.jam.net.ve/category/ubuntu/">Ubuntu</a> 10.10 y asi tener un servidor web local para hacer pruebas con PHP, instalar algun CMS, instalar alguna interfaz de administracion para <a href="http://blog.jam.net.ve/tag/mongodb/">MongoDB</a> :P , etc.

<img class="aligncenter size-medium wp-image-583" title="Nginx-logo" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Nginx-logo-300x65.png" alt="" width="300" height="65" />

Para esto lo primero que debemos hacer es instalar Nginx tecleando en la terminal:

{% highlight bash %}
sudo aptitude install nginx
{% endhighlight %}

con esto tendremos el servidor web Nginx instalado y funcionando en Ubuntu. Lo podemos comprobar escribiendo en el navegador:

{% highlight bash %}
http://localhost
{% endhighlight %}

Es probable que veas un mensaje <strong>404 Not Found </strong>y esto es porque en Ubuntu 10.10 el directorio raiz de Nginx por defecto es <strong>/var/www </strong>y alli no hay ningun <strong>index.html</strong>, sino que esta en <strong>/var/www/nginx-default</strong> .  Para solucionar esto copia el contenido de este ultimo directorio en <strong>/var/www</strong> y entra de nuevo en <strong>http://localhost</strong> Ahora si veras la pagina de Bienvenida de Nginx.

Ahora debemos instalar PHP5, PHP5-FPM y algunos extras, mas para esto teclamos en la terminal:

{% highlight bash %}
sudo aptitude install php5-cgi php5-fpm php5-dev php5-curl php5-cli php5-imagick php5-sqlite php-pear
{% endhighlight %}

Con esto ya deberiamos tener instalado PHP5 y ejecutandose PHP5-FPM (PHP5 sobre FastCGI).

Ahora nos queda configurar un poco Nginx para que pueda dar soporte PHP sobre FastCGI

Para esto debemos abrir el archivo de configuracion de sitios en Nginx y modificarlo un poco, lo abrimos con Vim teclando:

{% highlight bash %}
sudo vim /etc/nginx/sites-available/default
{% endhighlight %}

y lo modificamos para que se vea como esto:

{% highlight apache %}
# You may add here your
# server {
#    ...
# }
# statements for each of your virtual hosts

server {

 listen   80; ## listen for ipv4
 listen   [::]:80 default ipv6only=on; ## listen for ipv6

 server_name  localhost;

 access_log  /var/log/nginx/localhost.access.log;

 location / {
 root   /var/www;
 index  index.php index.html index.htm;
 }

 location /doc {
 root   /usr/share;
 autoindex on;
 allow 127.0.0.1;
 deny all;
 }

 location /images {
 root   /usr/share;
 autoindex on;
 }

 #error_page  404  /404.html;

 # redirect server error pages to the static page /50x.html
 #
 #error_page   500 502 503 504  /50x.html;
 location = /50x.html {
 root   /var/www;
 }

 # proxy the PHP scripts to Apache listening on 127.0.0.1:80
 #
 #location ~ \.php$ {
 #proxy_pass   http://127.0.0.1;
 #}

 # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
 #
 location ~ \.php$ {
 fastcgi_pass   127.0.0.1:9000;
 fastcgi_index  index.php;
 fastcgi_param  SCRIPT_FILENAME  /var/www$fastcgi_script_name;
 include fastcgi_params;
 }

 # deny access to .htaccess files, if Apache's document root
 # concurs with nginx's one
 #
 location ~ /\.ht {
 deny  all;
 }
}
{% endhighlight %}

La parte mas importante de todo es el bloque <strong>location ~ \.php$</strong> ...  en el que se especifica como Nginx va a trabajar con FastCGI.

Una vez realizado esto reiniciamos Nginx con:

{% highlight bash %}
sudo service nginx restart
{% endhighlight %}

Para comprobar que Nginx trabaja perfectamente con PHP5 nos vamos al directorio /var/www y con nano agregamos  el archivo info.php:

{% highlight bash %}
sudo vim info.php
{% endhighlight %}

en dicho archivo agregamos lo siguiente:

{% highlight php%}
<?php 
	phpinfo();
?>
{% endhighlight %}

Lo guardamos, cerramos y en el navegador escribimos:

{% highlight bash %}
http://localhost/info.php
{% endhighlight %}

si todo a ido bien veremos algo como esto:

<img class="aligncenter" title="Selección_026" src="http://blog.jam.net.ve/imagenes/uploads/2011/01/Selección_026-278x300.jpg" alt="" width="278" height="300" /></a>

Bien ya tienes instalado Nginx con soporte PHP5 mediante FastCGI (php5-fpm) :P
