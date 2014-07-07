---
layout: post
title: "Creando imagenes Docker desde archivos dockerfile"
tags: [linux, docker, sysadmin]
---

Hace algunos meses atras escribi un articulo en el que comentaba que era la
herramienta [Docker](http://docker.io)  y [Como instalar Docker](http://blog.jam.net.ve/2014/03/01/instalando-docker-archlinux).

En **Docker** existe un archivo llamado `dockerfile` el cual es una especie de
receta que interpreta Docker y que crea a partir de ella una **Imagen Docker**
desde la cual y con un simple comando podremos nosotros crear un contenedor
Docker para alvergar alli nuestras aplicaciones o servicios.

<!-- more -->

En esta oportunidad mostrare un ejemplo sumamente sencillo de como se podria
construir una imagen docker adaptada a nuestras necesidades especificas.
En este caso creare una imagen basada en Ubuntu 14.04 LTS la cual se le
instalaran una serie de paquetes basicos y se le le realizara la configuracion
de el servidor OpenSSH para asi poder conectarnos a el contenedor de manera
remota.

## El archivo dockerfile

Vamos a crear un archivo llamado `dockerfile` el cual va a contener lo siguiente:

Nota: Este dockerfile esta disponible en mi [Repositorio Github](https://github.com/jesusangelm/dockerfile)
para una mejor lectura y seguimiento del articulo.

{% highlight bash %}
#Imagen docker de prueba.

#Origen: Ubuntu 14.04 LTS
FROM ubuntu:14.04

#Creador:
MAINTAINER Jesus Marin <jam@jam.net.ve>

#Actualizar el repositorio Ubuntu, luego descarga e instala paquetes que
#requieren actualizacion.
RUN apt-get -qq update && apt-get -qqy upgrade

#Instalar algunos paquetes bases, utiles para mi y algunas dependencias.
RUN apt-get -qqy install wget git curl dnsutils tmux zsh openssh-server pwgen vim

#Tomado de https://github.com/tutumcloud/tutum-ubuntu/blob/master/Dockerfile
#Para configurar SSHD y crear una contrasena para usuario ROOT
RUN mkdir -p /var/run/sshd && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config && sed -i "s/PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config
ADD set_root_pw.sh /set_root_pw.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

EXPOSE 22
CMD ["/run.sh"]
{% endhighlight %}

##  Un dockerfile por dentro.

Notese que el archivo esta compuesto principalmente por conjuntos de 
`INSTRUCCION` en mayusculas segido de una `sentencia` en minuscula.

El texto que esta despues de un `#` es simplemente un comentario.

## La instruccion FROM.

En la primeras lineas podemos ver la palabra `FROM`, esta nos indica que
**Imagen Base** vamos a tomar para crear nuestra imagen personalizada, en este
caso usamos `ubuntu:14.04`. Docker toma esta imagen desde el **[Docker Registry](https://registry.hub.docker.com/)** el cual contiene nuestra imagen
base **[Ubuntu 14.04 LTS](https://registry.hub.docker.com/_/ubuntu/)**.

Notese que despues del nombre de la imagen indicamos la version de Ubuntu a
usar, bueno esto en Docker se llama `TAG` y es la forma en que podemos usar una
version especifica de esa imagen, si vemos las **tags** disponibles de dicha
imagen en su repositorio podemos ver que tambien disponemos de otras versiones
de Ubuntu como la `13.10` o la `12.04`.

Si por ejemplo no queremos usar como imagen base a Ubuntu sino que queremos
crear una imagen Debian o CentOS podriamos decir:

{% highlight bash %}
FROM debian:stable
{% endhighlight %}

{% highlight bash %}
FROM centos:6.4
{% endhighlight %}

## La instruccion MAINTAINER

Esta instruccion no tiene mucha ciencia, tan solo especificamos quien es el
autor de dicho dockerfile y su correo.

## La instruccion RUN

Esta instruccion la veras en casi cualquier dockerfile ya que con ella
especificas los comandos que quieras ejecutar. En este caso indicamos que
se ejecutara el comando:

{% highlight bash %}
apt-get -qq update && apt-get -qqy upgrade
{% endhighlight %}

El cual ejecuta a `apt-get` para que actualice el listado de repositorios e
inmediatamente actualice los paquetes que dispongan de actualizacion.

Mas abajo puedes ver que se ejecuta nuevamente `apt-get` pero esta vez para 
instalar algunos paquetes basicos que no estan en la imagen base y que podrias
requerir para tu imagen personalizada.

Tambien puedes ver que ejecuta una serie de comandos concatenados que crean
carpetas en ciertas ubicaciones de la imagen base y realiza configuraciones en
archivos. En esta parte se realiza una configuracion de el servidor OpenSSH.

## La instruccion ADD

Con esta instruccion podemos hacer que se agrege a la imagen base un archivo que
nosotros queremos que contenga, indicando la ubicacion actual de dicho archivo
en nuestro sistema y la ubicacion donde dentro de la imagen donde queremos que
se aloje dicho archivo.

En este caso `set_root_pw.sh` es el archivo a agregar, no especificamos una ruta
ya que el archivo esta en la misma carpeta en la que esta el archivo dockerfile.
Esta instruccion es seguida de `/set_root_pw.sh` notese el `/` delante del 
nombre del archivo, aqui si estamos especificando una ruta y es la ruta de
destino dentro de la imagen en donde ubicaremos dicho archivo a agregar.

## La instruccion EXPOSE

Con esta instruccion le decimos a Docker que los contenedores de esta imagen
escucharan en el puerto especificado una vez que dichos contenedores se esten
ejecutando. Docker tambien puede usar esta informacion para interconectar 
contenedores usando enlaces.

En nuestro caso exponemos el puerto `22` ya que usaremos un servidor OpenSSH
para poder conectarnos al contenedor via SSH. Si por ejemplo estubiesemos
creando un contenedor que alberga un servidor Web como por ejemplo Nginx o
Apache, necesitariamos exponer su puerto de eschucha el cual es tipicamente el
puerto `80`, lo mismo va si queremos usar cualquier otro servicio.


## La instruccion CMD

Esta instruccion es un tanto similar a la instruccion `RUN` solo que `CMD` ejecuta
el comando indicado unicamente cuando arranque el contenedor y no cuando se
este construyendo el mismo, esto puede servirnos para ejecutar servicios que ya
esten instalados o para correr archivos ejecutables espeficicando su ubicacion.

Esta instruccion tiene la limitante de que solo se puede colocar una sola vez 
en un archivo dockerfile.

En nuestro caso tan solo arrancamos el ejecutable `run.sh` que ya hemos agregado
en la raiz de la imagen base.

Por supuesto estas no son todas las instrucciones, existen algunas otras mas 
en la [Dockerfile Reference](https://docs.docker.com/reference/builder).


## Construyendo la imagen

Una vez tenemos nuestro archivo dockerfile nos vamos a una terminal, nos
ubicamos en el mismo directorio donde reside nuestro dockerfile y ejecutamos:

{% highlight bash %}
docker build -t="usuariodocker/ubuntu:14.04" .
{% endhighlight %}

Docker tiene como convencion que el nombre del repositorio contenga el nombre 
de la persona u organizacion que crea la imagen seguido de una `/` y luego el
nombre de la imagen y como opcional un `tag`

Notese tambien el `.` al final, con esto indicamos que la ubicacion del archivo
dockerfile esta en el directorio actual.

Cuando ejecutes el comando veras todo el proceso de construccion de la imagen
separando cada instruccion colocada en el dockerfile como un `step` o paso
numerado. El proceso puede tomar algunos minutos ya que consistira en la
descarga de la imagen base desde internet y tambien de la actualizacion de 
repositorios y paquetes.

## Creando contenedores en el fondo a partir de nuestra imagen personalizada

Debido a que este contenedor esta creado con servicios, necesitaremos ejecutarlo
en el fondo o como un `daemon` para que de este modo pueda ejecutarse el
servicio o los servicios que pueda contener. Para esto ejecutamos en una
terminal:

{% highlight bash %}
docker run -d -P usuariodocker/ubuntu:14.04
{% endhighlight %}

Este comando nos mostrara una secuencia de numeros y letras  el cual es el `ID`
del contenedor.

El flag `-d` hace que el contenedor se ejecute en el fondo y el flag `-P`
le dice a Docker que mapee los puertos que el contenedor este exponiendo, hacia
el S.O huesped, en nuestro caso el contenedor expone el puerto `22` pero Docker
mapea este el acceso a este puerto a travez de nuestro S.O usando un puerto
distinto, como por ejemplo el `49153`.

Para saber que puerto esta mapeando docker hacia el exterior tan solo teclea 
el comando:

{% highlight bash %}
docker ps -a
{% endhighlight %}

El cual te devolvera algo como esto:

{% highlight bash %}
CONTAINER ID        IMAGE                      COMMAND             CREATED             STATUS              PORTS                   NAMES
c3032b4c1033        usuariodocker/ubuntu:14.04   /run.sh           55 seconds ago       Up 50 seconds        0.0.0.0:49153->22/tcp   goofy_archimedes
{% endhighlight %}

en la columna `port` puedes ver el puerto expuesto por el contenedor y el puerto
que docker mapea para que podamos acceder a el. Tambien puedes ver el ID del 
contenedor el cual podemos usar para obtener la clave de usuario root que el
archivo ejecutable `set_root_pw.sh` configuro.

Para ver esta clave ejecutamos en una terminal:

{% highlight bash %}
docker logs c3032b4c1033
{% endhighlight %}

y podras ver algo como esto:

{% highlight bash %}
=> Setting a random password to the root user
=> Done!
========================================================================
You can now connect to this Ubuntu container via SSH using:

 ssh -p <port> root@<host>
and enter the root password 'S3cR3Tp4SS' when prompted

Please remember to change the above password as soon as possible!
========================================================================
{% endhighlight %}

## Conectandonos al contenedor mediante SSH

Habiamos dicho que este contenedor personalizado contenia un servicio SSH para
poder acceder a el remotamente como si se tratase de un servidor dedicado o VPS,
ya sabemos que el contenedor expone el puerto `22` perteneciente al servicio OpenSSH
y que Docker mapea este puerto al exterior usando **en este caso** el puerto
`49153`.

Bien para poder conectarnos por ssh tan solo ejecutamos en una terminal:

{% highlight console %}
ssh -p 49153 root@localhost
{% endhighlight %}

usando la clave root que vimos arriba.


Con vez, no es nada del otro mundo y con solo unos pocos pasos podemos crear
imagenes docker adaptadas a nuestras necesidades, de las cuales podemos crear 
contenedores portatiles para alojar nuestras aplicaciones, servicios o un entorno de
desarrollo y todo esto aislado de nuestro sistema operativo.

