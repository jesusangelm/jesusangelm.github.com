---
layout: post
title: "Instalando Docker en ArchLinux"
tags: [linux, archlinux, docker]
---

Cuando se esta desarrollando una aplicacion y llega el momento de implementarla
en produccion siempre se busca que este proceso sea lo mas sencillo, rapido y
confiable tanto como sea posible, hoy en dia existe varias herramientas que nos
facilitan el trabajo como por ejemplo las PaaS como Heroku que no permiten por
ejemplo colocar nuestra aplicaciones Rails y tenerla funcionando en pocos
minutos, o las IaaS como las AWS de Amazon que nos permiten crear instancias de
VM para colocar alli nuestras aplicaciones y sus dependencias, u otras
herramientas un tanto mas sencillas como Chef. En esta ocasion hablaremos de una
nueva herramienta conocida como [Docker](https://www.docker.io/) que nos puede ayudar igualmente pero de
la forma mas sencilla posible.

<center><img src="http://i.imgur.com/JVyF5bi.png" title="Hosted by imgur.com" /></center>

<!-- more -->

# Docker.

Docker es una herramienta de codigo abierto que nos permite automatizar el
despliegue de cualquier aplicacion en un contenedor ligero, portatil,
autosuficiente y que se pueda ejecutar practicamente en cualquier lugar.

Los contenedores de Docker pueden encapsular cualquier carga que se ejecutaran
consistentemente en practicamente cualquier servidor. El mismo contenedor en el
que se desarrolla, contruye y prueba la aplicacion puede correr a escala en un
servidor en produccion, en una maquina virtual, en un cluster, en OpenStack, en
una instancia publica o en cualquier combinacion de estas mismas.

Los usos comunes de Docker pueden ser:

- Automatizacion de el empaquetado y despliegue de aplicaciones.
- Creacion de entornos PaaS ligeros y privados.
- Pruebas a automatizadas y de integracion continua.
- Implementar y escalar aplicaiones web, Bases de datos y servicios backend.

En una forma simple se podria pensar que Docker funciona como una herramienta
como **VirtualBox** junto a **Vagrant**, pero los contenedores Docker no son **Maquinas
Virtuales (VM)** ya que estos no reservan espacio en memoria o procesos, ademas los
contenedores en Docker y su contenido se ejecutan mucho mas rapido que en una
VM, y son mucho mas ligeros. Muchos dicen que Docker es como un **chroot** con
esteroides. 

# Instalacion:

En **ArchLinux** el proceso es muy sencillo ya que se cuenta con el respectivo
paquete en los repositorios, tambien puede ser instalado desde AUR. en este caso
optare por instalar Docker desde el repositorio ArchLinux.

{% highlight bash %}
$ sudo pacman -S docker
{% endhighlight %}

# Configuracion y ejecucion:

Para usar Docker sin ser root tan solo debemos agregar nuestro usuario al grupo
**docker**

{% highlight bash %}
$ sudo gpasswd -a USUARIO docker
{% endhighlight %}

NOTA: Cambie **USUARIO** por el usuario que quiera usar.


Luego tan solo habilitamos sus servicio y lo ejecutamos:

{% highlight bash linenos %}
$ sudo systemctl enable docker
$ sudo systemctl start docker
{% endhighlight %}


# Pruebas:

Para ver una lista de comandos disponible podemos simplemente ejecutar `docker`
en la terminal. Tambien podemos ejecutar el comando `docker info` y veremos algo
como esto:

{% highlight bash %}
$ docker info
Containers: 5
Images: 4
Driver: devicemapper
 Pool Name: docker-8:17-1706253-pool
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.1 Mb
 Data Space Total: 102400.0 Mb
 Metadata Space Used: 1.0 Mb
 Metadata Space Total: 2048.0 Mb
Username: jesusangelm
Registry: [https://index.docker.io/v1/]
WARNING: No swap limit support
{% endhighlight %}

Ahora que vemos que funciona todo correctamente podemos descargar una **imagen
base** pre-construida para Docker, las imagenes de Docker son sistemas que
usaran los contenedores como base para correr nuestras aplicaciones. Estas
imagenes son Sistemas Operativos como Ubuntu, Fedora, ArchLinux, etc y en el
[Docker Index](https://index.docker.io/) puedes encontrar un listado de imagenes
disponibles para descargar o tambien puedes subir y comparti una imagen creada
por ti.

En este caso usare la imagen de [BusyBox](https://index.docker.io/_/busybox/),
para esto tan solo ejecutamos en la terminal:

{% highlight bash %}
$ docker pull busybox
{% endhighlight %}

Una vez descargada la imagen podemos meternos en su terminal y comenzar a
trabajar en ella:

{% highlight bash %}
$ docker run -i -t busybox:latest sh
{% endhighlight %}

Con esto entraremos en su entorno como si de un **chroot** se tratase, para
salir tan solo ejecuta el comando `exit`.

Con todo esto podremos tener instalado y funcionando Docker para comenzar a
usarlo, crear nuestros entornos de desarrollo o crear contenedores con
aplicaciones que puedan ser implementada en produccion muy rapido y sin
problemas. Este tutorial es una explicacion muy basica para el sin fin de
usos que podemos darle a Docker, recomiendo leer la [Tutorial Interactivo](https://www.docker.io/gettingstarted/) y la [Documentacion](http://docs.docker.io/) de Docker para conocerlo en mas detalles.

Un ejemplo de uso puede ser por ejemplo crear un contenedor Docker en el cual se
desarrolla y alberga una aplicacion Rails y otro contenedor que ejecute un 
servicio PostgreSQL, para luego interconectar estos dos contenedores y hacer que
nuestra aplicacion Rails pueda conectarse y usar la Base de datos Postgresql en
el segundo contenedor. Logicamente podrias colocar estos dos contenedores ne un
servidor de produccion y se ejecutaran se inmediato y sin problemas tal cual
estubiesen en entorno de desarrollo, Ejemplos como estos son los que hacen
interesante el uso de Docker.


