---
layout: post
title: "Crea tu propia nube con Syncthing, alternativa a BTSync y AeroFS"
tags: [linux, sincronizacion, servidor, respaldo]
---

Syncthing es una aplicacion opensource de sincronizacion de archivos escrita en Golang
la cual implementa su propio protocolo de Block Exchange.

Syncthing es de codigo abierto y viene a ser una alternativa a BittorrentSync
 y AeroFS, la cual son dos conocidas aplicaciones para sincronizar archivos usando 
 el protocolo P2P y conectando los nodos (PC, Laptop, Servidor) de forma directa,
 sin usar ningun servidor como intermediario y encriptando todas las comunicaciones
 entre ellos.

Con Syncthing tu eres propietario de tu propia **nube** y de tus datos, tu ideas
la infrastructura a usar y como la vas a usar, tu decides que se va a respaldar
y cuantas replicas quieres tener ademas de decidir que tanto espacio de almacenamiento
quieres o necesitas. Esta aplicacion es tambien multiplataforma por lo que puedes
correr un nodo en Linux, BSD, Windows y mac.

<!-- more -->

# Instalacion:

En el Servidor uno descargamos los binarios de Syncthing desde su repositorio 
[Github](https://github.com/syncthing/syncthing/releases)

Para el momento de escribir este articulo la ultima version es la `v0.10.18`.
En mi caso descargo la version de 32bits para Linux, pero en la misma pagina 
puede descargarse las versiones 64bits y las versiones para plataformas como
BSD, Windows y mac.

{% highlight bash %}
$ wget https://github.com/syncthing/syncthing/releases/download/v0.10.18/syncthing-linux-386-v0.10.18.tar.gz
{% endhighlight %}

Descomprimir el paquete de binarios

{% highlight bash %}
$ tar xzvf syncthing-linux-386-v0.10.18.tar.gz
{% endhighlight %}

y luego copiamos el binario **syncthing** ubicado en la carpeta que se crea al
descomprimir el paquete al directorio `/usr/local/bin/`

{% highlight bash %}
$ sudo cp syncthing-linux-386-v0.10.18/syncthing /usr/local/bin/
{% endhighlight %}

una vez copiado el binario podemos eliminar la carpeta extraida pues ya no
la necesitamos.


# Servicio upstart para Debian/Ubuntu:

Con esto tenemos Syncthing instalado y listo para usar, pero seria un poco
incomodo ejecutarlo pues tendriamos que iniciarlo desde esa carpeta, en este caso
usaremos un script upstart para poder arrancar y detener syncthing mas facil.

Creamos un archivo en `/etc/init/` con el nombre `syncthing.conf` y colocamos
el siguiente contenido:

{% highlight bash %}
description "Syncthing P2P sync service"

start on (local-filesystems and net-device-up IFACE!=lo)
  stop on runlevel [!2345]

  env STNORESTART=yes
  env HOME=/home/tu_usuario
  setuid "tu_usuario"
  setgid "tu_grupo"

  exec /usr/local/bin/syncthing

  respawn
{% endhighlight %}

Notese que se ajusta el directorio `HOME` de tu usuario y se agrega tu nombre de
usuario y grupo en `setuid` y `setgid`.

Con esto ya podemos arrancar el servicio de Syncthing con un simple:

{% highlight bash %}
$ sudo initctl start syncthing
{% endhighlight %}

o con un simple:

{% highlight bash %}
$ sudo service syncthing start
{% endhighlight %}


# Configuracion basica en servidores:

Ya en este punto deberiamos tener corriendo syncthing, por default la interfaz web
escucha en el puerto `8080` y como medida de seguridad lo hace solo en localhost,
lo que quiere decir que por defecto no puedes acceder de forma remota.

Syncthing en el primer arranque crea un archivo `config.xml` de Configuracion en 
la ruta `~/.config/syncthing/`. Si abrimos este archivo en un editor podemos
editarlo para que pueda recibir conexiones desde el exterior y poder administrar
Syncthing de forma remota.

Buscamos las siguientes lineas:

{% highlight xml %}
<gui enabled="true" tls="false">
    <address>127.0.0.1:8080</address>
</gui>
{% endhighlight %}

y reemplazamos la IP `127.0.0.1` por `0.0.0.0`

**NOTA:** De seguro estas utilizando un **Firewall** en tu servidor, por lo que es
necesario que abras el puerto `8080` para poder recibir conexiones entrantes.

{% highlight bash %}
$ sudo ufw allow 8080
$ sudo ufw allow 22000
{% endhighlight %}

Syncthing usa por defecto el puerto `22000` para el protocolo de sincronizacion
por lo que este tambien debe abrirse para conexiones entrantes.

Con esto ya puedes acceder a tu servidor desde el navegador y configurar Syncthing
desde la interfaz web incluida. `http://servidor.tld:8080`

En la parte superior derecha podemos ver un engranaje desee el cual podemos acceder
a la seccion de configuracion:

![Syncthing Config](http://i.imgur.com/tSCQSir.png "Configuracion Syncthing")

Como se puede notar, es posible configurar el nombre del dispositivo (nodo), la
ip y puerto de escucha para la interfaz web, y lo mas importante, la asignacion de
un nombre de usuario y clave para proteger el acceso a interfaz web, asi como el 
uso de `HTTPS` para proteger la comunicacion en dicha interfaz.

De esta misma forma es posible instalar y configurar multiples servidores (nodos)
en internet para sincronizacion y respaldo de archivos.

# Conexion entre dos nodos y comparticion de archivos:

La forma en la que Syncthing se comunica entre los demas nodos es usando un **ID**
unico. En el primer arranque, Syncthing genera este ID para identificar el nodo.

Un ID identificador de nodo es similar a esto:

![Node ID](http://i.imgur.com/isdQLam.png)

y es posible obtenerlo desde el boton de engranaje antes mencionado, haciendo click
en **"Mostrar ID"**

Notese que tambien se visualiza un codigo QR, esto es debido a que esta en desarrollo
una version para telefonos celulares en la que podemos agregar los nodos de 
sincronizacion usando su codigo QR.

Para agregar un nodo al cual nuestro servidor puede comunicarse para sincronizar
archivos y carpetas basta con hacer click en **"Agregar Dispositivo"** en la pagina
principal de la interfaz web, a continuacion nos aparece un formulario en donde nos
solicita unicamente el **ID** del nodo y el nombre del mismo.

![New Node](http://i.imgur.com/Qm3ZExA.png)

Tambien nos permite elegir que carpetas queremos sincronizar con ese nodo en 
especifico.

Esta tarea se debe hacer de la misma forma en el nodo receptor, en el cual se debe
crear y compartir la carpeta con el mismo nombre que en el nodo de origen.


# Creando Repositorios (carpetas):

En Syncthing los repositorios son simples carpetas las cuales contienen los archivos
a sincronizar y compartir con los nodos que tu elijas. Para crear una tan solo
has click en el boton **"Agregar Repositorio"** y acontinuacion aparecera una 
ventana como esta:

![New repo](http://i.imgur.com/o6vSZob.png)

En dicho formulario se puede colocar el **ID del repositorio** el cual sera el nombre
unico que tendra la carpeta en el nodo actual. Tambien es posible indicar la ruta
del repositorio o carpeta, si esta no existe en el servidor syncthing la creara
de forma automatica.

De igual forma puedes indicar aqui con cuales nodos deseas compartir dicho repositorio.

Nuevamente: si deseas compartir y sincronizar este reporitorio con otro nodo, el
repositorio debe ser creado con el mismo ID y nombre de carpeta en el nodo receptor

Con todo esto en mente tenemos el conocimiento necesario para armasr nuestra propia
**Nube** privada, solo tu tienes acceso a ella, solo tu la controlas y decides que 
tanto espacio de almacenamiento quieres que esta tenga. Al mismo tiempo tienes la 
capacidad de agregar mas nodos a esta **Nube** a modo de replicas de seguridad.

Syncthing es una herramienta que a pesar de estar todavia en desarrollo se comporta
de una manera muy estable y nos brinda un gran potencial para proteger nuestros
datos mas preciados.
