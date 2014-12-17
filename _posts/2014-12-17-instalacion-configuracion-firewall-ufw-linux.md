---
layout: post
title: "Configuracion basica de UFW Firewall en Linux."
tags: [linux, firewall, servidor]
---

Al administrar servidores, una de las primeras cosas que se deben configurar para
aumentar la seguridad de los mismos es configurar un Firewall, Por suerte en Linux
se incluye uno por defecto llamado Iptables pero este firewall muchos lo ven un poco
complejo de configurar y administrar. Existen alternativas mas sencillas de usar 
como por ejemplo **UFW**.

UFW es en realidad es una CLI o intefaz de linea de comandos para el Firewall Iptables
que incluye Linux, esta interfaz nos proporciona una manera un poco mas sencilla de 
administrar y configurar Iptables. para UFW incluso existe una GUI o interfaz
grafica llamada **GUFW** el cual podriamos usar en una PC de escritorio o Laptop
para administrar y configurar el firewall.

<!-- more -->

# Instalacion de UFW en el servidor:

para instalarlo basta con escribir en una terminal el comando

{% highlight bash %}
$ sudo apt-get install ufw
{% endhighlight %}

Por defecto UFW esta desactivado luego de la instalacion, por lo que podemos ver
su estado con el comando:

{% highlight bash %}
$ sudo ufw status verbose
{% endhighlight %}

# Configuraciones basicas de UFW:

Algunas de las configuraciones basicas que podemos usar en UFW para asegurar nuestros
servidores son.


### Reglas por defecto:

Las reglas por defecto o **default rules** son, como su nombre lo indica, una serie
de reglas standar que nos facilita la configuracion de el Firewall, estas reglas nos
permiten especificar si queremos permitir `allow` o denegar `deny` el trafico entrante
`incoming` o el trafico saliente `outgoing`, ademas de algunas otras reglas.

Una configuracion muy buena que de hecho usa GUFW apenas es instalado en una PC, 
es la de denegar `deny` todo el trafico entrante y permitir `allow` el trafico saliente.

Esto lo podemos ajustar con los siguientes comandos:

{% highlight bash %}
$ sudo ufw default deny incoming
{% endhighlight %}

Para denegar todo el trafico entrante.

{% highlight bash %}
$ sudo ufw default allow outgoing
{% endhighlight %}

Con estas dos configuraciones una PC esta bastante protegida al igual que un servidor,
pero si queremos aumentar la seguridad podriamos tambien denegar el trafico saliente
para una mayor seguridad, claro esta con la desventaja de que tendras que estar 
pendiente de que aplicaciones requieren alguna regla de trafico saliente para poder
funcionar correctamente.

### Permitir conexiones:

Supongamos que estamos configurando el firewall en nuestro servidor y denegamos 
todo el trafico entrante, como vamos a conectarnos remotamente a el mediante **SSH**?. 
Necesitamos aplicar una regla que nos permita conectarnos al puerto `22`.

Para esto usamos la opcion `allow` y le especificamos el puerto al que queremos
permitir el trafico entrante y el protocolo TCP que este use:

{% highlight bash %}
$ sudo ufw allow 22/tcp
{% endhighlight %}

UFW viene con algun conjunto de reglas prestablecidas que podemos usar mediante su nombre,
por ejemplo el comando anterior trata de abrir el puerto `22` que es conocido por 
ser el puerto usado para conexiones **SSH**, esta regla podriamos tambien habilitarla
con el comando:

{% highlight bash %}
$ sudo ufw allow ssh
{% endhighlight %}

De la misma forma podriamos usar otras reglas preestablecidas para servicios conocidos
como por ejemplo **HTTP** que usa el puerto `80`, **HTTPS** que usa el puerto `443`, etc.

### Rangos de puertos:

Es posible tambien que quieras permitir el trafico entrante no solo a un puerto sino
a un rango de estos, un ejemnplo de esto podria ser con la aplicacion **Mosh** 
que requiere sea abierto el rango de puertos que van del `60000` al `61000` por el 
protocolo `udp`.

Esto lo podriamos aplicar escribiendo algo como:

{% highlight bash %}
$ sudo ufw allow 60000:61000/udp
{% endhighlight %}

### Denegar conexiones:

De la misma forma en la que permitimos conexiones entrantes, podemos denegar dichas
conexiones.

Supongamos que tenemos una regla por defecto en la que se permite todo el trafico 
entrante (NO se recomienda), pero nosotros queremos denegar el trafico entrante
solo en un puerto determinado, podriamos aplicar dicha configuracion con algo como:

{% highlight bash %}
$ sudo ufw deny 22/tcp
{% endhighlight %}

De la misma forma podriamos hacerlo para denegar un rango de puerto.

{% highlight bash %}
$ sudo ufw deny 60000:61000/udp
{% endhighlight %}


### Eliminar reglas:

Supongamos que hemos configurado el servidor SSH para usar el puerto `2222` en lugar
del puerto `22` anteriormente abierto, deberiamos eliminar la regla anterior en 
la que se permitia la entrada al puerto `22`. Esto podriamos realizarlo con el 
siguiente comando:

{% highlight bash %}
$ sudo ufw delete allow 22/tcp
{% endhighlight %}

De forma similar podriamos hacerlo si se trata de un rango de puertos:

{% highlight bash %}
$ sudo ufw delete allow 60000:61000/udp
{% endhighlight %}

Si por ejemplo tenemos un conjunto de reglas establecidas con UFW de las cuales 
queremos eliminar algunas pero no conocemos como realizar dicha eliminacion por ser
algun tipo de regla compleja, podriamos listarlas con el comando:

{% highlight bash %}
$ sudo ufw status numbered
{% endhighlight %}

Lo que nos devolveria un conjunto de reglas numeradas como estas:

~~~
     To                         Action      From
     --                         ------      ----
[ 1] 22                         ALLOW IN    Anywhere
[ 2] 80                         ALLOW IN    Anywhere
[ 3] 443                        ALLOW IN    Anywhere
[ 4] 60000:61000/udp            ALLOW IN    Anywhere
[ 5] 22000/tcp                  ALLOW IN    Anywhere
~~~

Como se nota arriba, las reglas estan numeradas, por lo que podriamos usar ese 
numero para eliminar una regla en especifico:

{% highlight bash %}
$ sudo ufw delete 5
{% endhighlight %}

Lo que nos eliminara la ultima regla listada.

# Activando y desactivando UFW:

Una vez configurada todas las reglas y asegurarnos de que todo esta correcto,
procedemos a activar el firewall con el comando:

{% highlight bash %}
$ sudo ufw enable
{% endhighlight %}

Con esto ya tendremos UFW activo y protegiendo las conexiones con las reglas que
hemos especificado.

En caso de que queramos desactivar UFW tecleamos el comando:

{% highlight bash %}
$ sudo ufw disable
{% endhighlight %}

Si por alguna razon requieres que se eliminen todas las reglas aplicadas

{% highlight bash %}
$ sudo ufw reset
{% endhighlight %}

Estas son solo algunas de las configuraciones basicas de UFW con las que podemos
agregar una buena capa de seguridad a nuestras PC y servidores, logicamente existen
configuraciones avanzadas que se pueden usar para mejorar todavia mas la seguridad
o para realizar algun tipo de tarea espeficica.


