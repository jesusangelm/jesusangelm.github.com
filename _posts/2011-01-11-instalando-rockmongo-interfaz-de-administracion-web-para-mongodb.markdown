---
layout: post
title: "Instalando RockMongo interfaz de administracion web para MongoDB"
tags: [mongodb, nosql, sysadmin]
---
# Instalando RockMongo interfaz de administracion web para MongoDB

{% include post_header.html %}

En el mundo de las bases de datos relacionales, una de las formas mas usadas para administrar una base de datos es usando una interfaz web, esto sobretodo si el usuario no cuenta con un acceso shell a su cuenta de hosting. En las bases de datos relacionales por lo general se usa aplicaciones escritas en PHP como phpMyAdmin para MySQL y phpPgAdmin para PostgreSQL.

<a href="http://imgur.com/ZgBVN"><img src="http://i.imgur.com/ZgBVNl.jpg" title="Hosted by imgur.com" alt="" /></a>

Bien en el mundo de las bases de datos NoSQL hay aplicaciones web similares, una de ellas es <a href="https://code.google.com/p/rock-php/">RockMongo</a> la cual esta escrita en PHP y posee una interfaz bastante intuitiva y un tanto similar a phpMyAdmin. Instalar RockMongo es sumamente sencillo y al estar escrita en PHP lo unico que requerimos es tener instalado y corriendo un servicio web como Nginx, Apache o similares, el lenguaje PHP y el driver correspondiente para accesar a MongoDB desde PHP.

Bien por suerte hace unos dias explique <a href="http://blog.jam.net.ve/2011/01/04/instalando-nginx-con-soporte-php5-en-ubuntu/">como instalar Nginx con soporte PHP5 en Ubuntu</a>, por lo que siguiendo dicho articulo tendremos mas de medio camino listo! (¡Todos mis articulos estan friamente calculados! jajajaja :P ). Nos queda nada mas instalar el driver PHP para MongoDB y descargar e instalar RockMongo.

**Instalando el Driver MongoDB y PHP:** Bien para instalar este driver tan solo abrimos una terminal y escribimos en ella:

{% highlight bash %}
sudo pecl install mongo
{% endhighlight %}

esto nos instalara el driver para poder acceder a MongoDB desde PHP, ahora debemos configurar nuestro archivo <strong>php.ini </strong>y agregar la siguiente linea:

{% highlight bash %}
extension=mongo.so
{% endhighlight %}

**Nota:** si seguiste mi articulo sobre <a href="blog.jam.net.ve/2011/01/04/instalando-nginx-con-soporte-php5-en-ubuntu/">como instalar Nginx con soporte PHP5 en Ubuntu</a>, en la carpeta <strong>/etc/php5</strong> encontraras varios archivos <strong>php.ini</strong>, el que debemos editar sera aquel que se encuentre dentro de la carpeta <strong>fpm</strong>, es decir la ruta del archivo seria algo como <strong>/etc/php5/fpm/php.ini</strong> ¿porque editamos especificamente este archivo? pues simple, porque siguiendo ese tutorial estamos corriendo PHP mediante <strong>FastCGI</strong> usando PHP5-FPM, de todos modos y si asi lo deseas, puedes agregar la linea en las demas archivos php.ini sin problemas.

luego de editar el archivo php.ini debemos reiniciar PHP5-FPM para que los cambios tengan efecto:

{% highlight bash %}
sudo service php5-fpm restart
{% endhighlight %}

Ahora nos queda instalar RockMongo, para esto tan solo debemos <a href="https://code.google.com/p/rock-php/downloads/list">descargar</a> la ultima version desde la pagina oficial. Al momento de escirbir esto la ultima version es la 1.0.11 con buenas mejoras como traduccion al Español, insertar y modificar documentos en formato JSON (en versiones anteriores habia que escribir los documentos en arrays PHP).

una ves descargardo, lo descomprimimos y obtendremos una carpeta llamada <strong>rockmongo</strong> la cual debemos copiar en la raiz de nuestro servidor web, en nustro caso debemos copiar dicha carpeta en <strong>/var/www</strong>

<strong>Nota:</strong> recuerda que el directorio <strong>/var/www</strong> por lo general pertenece a root (administrador) por lo que necesitaras privilegios de administrador para copiar la carpeta rockmongo dicho directorio.

si lo deseas puedes abrir con tu editor favorito y ver el archivo config.php, encontraremos algo como esto:

{% highlight php %}
$MONGO["servers"] = array(
 array(
 "host" => "localhost", // Replace your MongoDB host ip or domain name here
 "port" => "27017", // MongoDB connection port
 "username" => null, // MongoDB connection username
 "password" => null, // MongoDB connection password
 "auth_enabled" => true,//Enable authentication, set to "false" to disable authentication
 "admins" => array(
 "admin" => "admin", // Administrator's USERNAME => PASSWORD
 //"iwind" => "123456",
 ),
{% endhighlight %}

como ves, RockMongo nos permite configurarlo para conectarse a instancias locales o remotas de MongoDB, asi como tambien ver y cambiar los datos de usuario y contraseña del admin para iniciar sesion en Rockmongo. Si dejamos el archivo tal como esta, rockmongo se conectara a nuestra instancia local de mongodb y usaremos para iniciar sesion em rockmongo el nombre de usuario "admin"  y contraseña "admin".

Bien ya tenemos instalado y configurado RockMongo y ya podemos comenzar a usarlo, tan solo debemos ingresar en nuestro navegador y escirbir en la barra de direcciones:

{% highlight bash %}
http://localhost/rockmongo
{% endhighlight %}

luego de loguearte como admin veras algo como esto:

<a href="http://imgur.com/gMehz"><img src="http://i.imgur.com/gMehzs.jpg" title="Hosted by imgur.com" alt="" /></a>

**Nota:** es probable que al teclear esta direccion en el navegador no veas nada o veas un error, es posible que requieras darle los permisos de lectura-escritura-ejecucion necesarios a la carpeta rockmongo y sus archivos.

tecleando el comando estando ubicado en <strong>/var/www</strong>:

{% highlight bash %}
sudo chmod 777 rockmongo/*
{% endhighlight %}


te podria sacar del apuro, pero ojo no es lo mas recomendable en un servidor.

Bien ya con esto tienes instalado y funcionando RockMongo por lo que ya puedes usarlo para "jugar" con MongoDB. Por supuesto este no es la unica interfaz de administracion para MongoDB, existen muchas otras como FangOfMongo la cual esta programada en Python y Django, pero en mis pruebas no me convencio mucho. Existen tambien phpMoAdmin la cual es bastante liviana y viene escrita en tan solo 1 archivo .php, pero la interfaz no me parece muy intuitiva, ademas de ser extremadamente simple. Si conocer las demas Gui de Administarcion ta solo visita la documentacion oficial de <a href="http://www.mongodb.org/display/DOCS/Admin+UIs">MongoDB</a>.

Saludos y espero les sirva :D
