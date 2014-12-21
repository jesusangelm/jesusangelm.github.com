---
layout: post
title: "Configuracion basica de Fail2Ban en Linux."
tags: [linux, fail2ban, servidor, ssh]
---

Segun la Wikipedia:

> Fail2ban es una aplicación escrita en Python para la prevención de intrusos 
en un sistema, que actúa penalizando o bloqueando las conexiones remotas que 
intentan accesos por fuerza bruta.

**Fail2ban** nos sirve de ayuda para proteger servidores y vps contra ataques de fuerza
bruta sobre determinados servicios que estos ofrescan, la manera en que trabaja es
analizando los archivos de logs que los diversos servicios generan, y busca en ellos
registros de comportamientos no tipicos (por lo general basado en alguna regla ya
    especificada) para luego determinar la ip del origen del ataque y proceder a 
**banearla** o **bloquearla** mediante el Firewall o algun sistema de control de paquetes.

<!-- more -->

# Instalacion de Fail2ban:

Para instalar Fail2ban basta con teclear en una terminal:

{% highlight bash %}
$ sudo apt-get install fail2ban iptables-persistent
{% endhighlight %}

Aqui el paquete iptables-persistent lo instalamos para que las reglas de baneo
agregadas al firewall iptables esten disponibles y sean persistentes luego de un
reinicio.

# Configuracion basica de Fail2ban:

Una vez instalado, procedemos a realizar alguna configuracion basica requerida 
para comenzar a proteger ciertos servicios en el servidor, en este caso se pasa a
configurar fail2ban para proteger el servicio **SSH**.

Fail2ban viene con un archivo de configuracion `jail.conf` que nos sirve de ejemplo
y que por lo general en las actualizaciones puede cambiar, por lo que es recomendable
copiarlo y renombrarlo a `jail.local` para luego alli editar y colocar las configuraciones
a nuestro gusto:

{% highlight bash %}
$ sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
{% endhighlight %}

una vez copiado el archivo, podemos proceder a configurarlo de acuerdo a nuestras
necesidades:

### bantime:

  Al abrir el archivo `jail.local` una de las primeras cosas que podemos editar es
la linea referente al `bantime` el cual hace referencia al tiempo (en segundos) 
  en la que una IP sera baneada o bloqueada. Por lo general viene con un tiempo
  algo corto como `600` segundos, que seria algo asi como 10 minutos.

  Este valor podriamos cambiarlo a por ejemplo a `3600` que seria algo asi como 1 hora.

{% highlight bash %}
bantime = 3600
{% endhighlight %}

### maxretry:

La cantidad maxima de intentos fallidos que se pueden permitir se especifica con
`maxretry`, si una IP alcanza este numero, pasara a ser baneada o bloqueada.
Por lo general viene configurada a 3, pero podriamos ser super exigentes y cambiarlo
a 2.

{% highlight bash %}
maxretry = 2
{% endhighlight %}

### findtime:

Una IP puede alcanzar el limite de intentos fallidos (especificado con maxretry)
  de forma muy rapida, o puede que haga los intentos en ciclos de varios minutos o horas,
  ese tiempo limite podriamos especificarlo con `findtime`, si una IP alcanza
  los intentos fallidos dentro de ese periodo de tiempo, pasara a ser baneada.

  Por lo general viene con un valor bajo como `600` segundos, pero podemos cambiarlo
  a nuestro gusto por un valor mas alto.

{% highlight bash %}
findtime = 1000
{% endhighlight %}

### destemail:

Fail2ban nos permite especificar una direccion de correos para que este nos envie
notificaciones con informacion sobre una IP recientemente bloqueada. Con 
`destemail` espeficificamos ese correo.

{% highlight bash %}
destemail = correo@dominio.tld
{% endhighlight %}

### mta:

Fail2ban es capaz de usar algun agente de transferencia de correos instalado en
el servidor para el envio de notificaciones, por default viene configurado para usar
`sendmail`, pero podriamos cambiarlo a `mail` para luego usar servicios como Postfix
para que este realice el envio de los correos.

{% highlight bash %}
mta = mail
{% endhighlight %}

### action:

Con esto configuramos la accion que fail2ban tomara para realizar un baneo,
    estas acciones estan tambien especificadas en el archivo, nosotros solo tendremos
    que elegir una:

{% highlight bash %}
action = %(action_mwl)s
{% endhighlight %}


# Configuraciones de baneo por servicios:

Fail2ban viene con un conjunto de reglas de bloqueo predefinida de acuerdo a determinados
servicios, culminando en archivo `jail.local` podemos ver algunas de estas reglas,
muchas de ellas estan desactivadas, por lo que tan solo debemos buscar la que necesitamos 
y activarla:

{% highlight bash %}
[ssh]

enabled  = true
port     = ssh
filter   = sshd
logpath  = /var/log/auth.log
maxretry = 3
{% endhighlight %}

Esta regla arriba nos permite proteger el servicio SSH contra ataques de fuerza bruta
 y demas intentos de acceso, notese que se especifica con `logpath` la ruta del
 archivo log de dicho servicio, este archivo es el que Fail2ban analizara en busqueda
 de potenciales atacantes para ser bloqueados.
 
Notese tambien que podemos espeficicar el puerto con `port` el cual usa dicho servicio,
si por ejemplo hemos cambiado el puerto de escucha para SSH a `2222` o similar, debemos
indicarlo tambien alli.

Tambien podemos ver que se especifica tambien el `maxretry` esto nos permite ajustar 
el maximo numero de intento fallidos para cada regla o servicio.


Una vez realizada la configuracion basica, ya tenemos listo fail2ban para comenzar
a trabajar y proteger, para aplicar las reglas tan solo necesitamos reiniciarlo:

{% highlight bash %}
$ sudo service fail2ban stop
$ sudo service fail2ban start
{% endhighlight %}


Ya con esto podemos estar un poco mas tranquilos de haber agregado una capa mas 
de seguridad a nuestra PC o servidor. Logicamente es posible activar mas reglas 
o agregar nuestras propias reglas personalizadas, ademas de completar la configuracion
para el envio de notificaciones por correos.

