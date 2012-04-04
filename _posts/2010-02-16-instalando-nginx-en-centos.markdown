---
layout: post
title: !binary |-
  SW5zdGFsYW5kbyBOZ2lueCBlbiBDZW50T1M=
tags:
- !binary |-
  Y29ycmVv
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  c2Vydmlkb3I=
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  Y2VudG9z
- !binary |-
  cGFuZWw=
- !binary |-
  bmdpbng=
- !binary |-
  dnBz
- !binary |-
  bXlzcWw=
- !binary |-
  cGhw
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  b3BlcmE=
- !binary |-
  d2VibQ==
- !binary |-
  YmFzaA==
- !binary |-
  ZG5z
- !binary |-
  aW1wb3J0YXI=
- !binary |-
  d2Vi
- !binary |-
  cmVsZWFzZQ==
- !binary |-
  dGVybWluYWw=
- !binary |-
  cmVk
---
{% include JB/setup %}

En mi anterior post  les explicaba como <a href="http://blog.jam.net.ve/2010/02/16/instalando-webmin-en-centos-debian/" target="_blank">instalar el panel de control Webmin</a> y les comentaba que me habia hecho con un VPS para pruebas y aprendizaje  el cual tiene CentOS como Sistema Operativo. Bueno este VPS que me fue ofrecido es Unmanaged, es decir "No Administrado" lo que significa que el proveedor no me ofrece soporte tecnico completo.  en pocas palabras:  "que yo debo hacer absolutamente todo".  Bien eso es lo que me gusta puesto que la idea principal es aprender.

Uno de los principales problemas con lo que me tope apenas tube los datos de acceso en mis manos fue que el VPS tiene poca memoria Ram, unos 128Mb para ser exactos. Esto me pone el trabajo un poco mas dificil pues no es memoria suficientes como para instalar y poner a funcionar simultaneamente y sin muchas configuraciones el Apache, MySQL, PHP, Bind, FTP, Webmin, correos POP3/SMTP/IMAP, etc....   Bien ya con esto entendi que no podia hacer ni exigirle mucho al VPS, pero algo tenia que hacer, al menos deberia poder lograr agregarle un dominio para accesar por medio de ese dominio  y no por la ip, y poder montar por lo menos una pagina estatica y quitar la que estaba por defecto.

Una de las cosas en la que me fije es que el servicio web Apache consume considerablemente la poca memoria ram disponible y junto al servicio DNS Bind y el servicio de Webmin se tiraban los 128Mb de ram poniendo el VPS en riesgo de que se reinicie o cuelgue.  Bien el servicio Webmin solo se ejecuta cuando quiero accesar al panel, asi que el resto del tiempo esta detenido y sin consumir ni un solo kb de la ram. El servicio Bind, por los momentos no e hallado manera de hacer que consuma menos ram pero es de vital importancia tenerlo ejecutandose para que pueda resolver los dominios y demas configuraciones DNS que le tengo.

Asi que esto de momento me deja con Apache en la mira, pues bien le tengo un sustituto que consume muy poca memoria ram y se ejecuta en tan solo dos procesos contra los nueve que me muestra el Apache. El servidor web que les menciono se llama <a href="http://www.nginx.org/" target="_blank">Nginx</a> y es un servidor web gratuito cuyas principales ventajas es que es super rapido, estable y lo mas importante, muy ligero.

Para instalarlo en CentOS primero debemos instalar los Repositorios EPEL tecleando en la terminal:

- Para versiones de 64Bits

{% highlight bash %}
$ sudo rpm -Uvh http://download.fedora.redhat.com/pub/epel/5Server/x86_64/epel-release-5-3.noarch.rpm
{% endhighlight %}

- Para versiones de 32Bits

{% highlight bash %}
$ sudo rpm -Uvh http://download.fedora.redhat.com/pub/epel/5Server/i386/epel-release-5-3.noarch.rpm
{% endhighlight %}


Instalado dichos repositorios ahora podremos instalar Nginx usando el comando Yum, para esto tecleamos en la terminal:

{% highlight bash %}
$ sudo yum install nginx
{% endhighlight %}

Durante el proceso se te preguntara si deseas importar la llave GPG de EPEL y te aparecera algo como esto:

{% highlight bash %}
warning: rpmts_HdrFromFdno: Header V3 DSA signature: NOKEY, key ID 217521f6 Importing GPG key 0x217521F6 Fedora EPEL epel@fedoraproject.org from /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL Is this ok [y/N]:
{% endhighlight %}

Presionamos la tecla "Y"  para aceptar y finalizar con la instalacion.

Ahora ya deberiamos tener instalado nuestro servidor web de bajo consumo en el servidor, tan solo nos falta iniciarlo tecleando en la terminal:

{% highlight bash session%}
service nginx start
{% endhighlight %}

y nos vamos a nuestro navegador ingresamos nuestra ip o dominio si el servidor esta online, o "localhost" si es una instalacion local en nuestra pc.

con esto veremos la pagina por defecto de Nginx la cual es algo como esto

<a href="http://imgur.com/N3UNu"><img src="http://i.imgur.com/N3UNul.png" title="Hosted by imgur.com" alt="" /></a>

Bien a mi este cambio de Apache a Nginx me a ido como anillo al dedo pues e podido ahorrar algo de memoria ram y procesos en el cpu que puedo invertir para ejecutar otras aplicaciones que necesite o para no quedarme tan corto en cuanto a memoria ram disponible.

Aqui podemos ver el consumo de memoria y procesos en ejecucion teniendo Apache ejecutandose como servidor web.

<a href="http://imgur.com/z4TUu"><img src="http://i.imgur.com/z4TUu.png" title="Hosted by imgur.com" alt="" /></a>

y aqui vemos como nos a quedado el VPS ejecutando Nginx como servidor web.

<a href="http://imgur.com/VRgUx"><img src="http://i.imgur.com/VRgUx.png" title="Hosted by imgur.com" alt="" /></a>

Un ahorro de aproximadamente 15Mb de memoria Ram y un ahorro de 7 procesos menos en ejecucion!!!!!

Saludos y espero les sirva tanto como a mi.
