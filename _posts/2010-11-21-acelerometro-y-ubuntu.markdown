---
layout: post
title: !binary |-
  QWNlbGVyb21ldHJvIHkgVWJ1bnR1
tags:
- !binary |-
  Z29vZ2xl
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  bGludXg=
- !binary |-
  c29mdHdhcmU=
- !binary |-
  dWJ1bnR1
- !binary |-
  d2luZG93cw==
- !binary |-
  bW9uaXRvcg==
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  ZXNjcml0b3Jpbw==
- !binary |-
  YmFy
- !binary |-
  dmlkZW8=
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  Z21haWw=
- !binary |-
  cmVsZWFzZQ==
- !binary |-
  dGVybWluYWw=
- !binary |-
  YXJjaGl2b3M=
- !binary |-
  cmVtb3Rv
- !binary |-
  YWNlbGVyb21ldHJv
- !binary |-
  bGFwdG9w
---
{% include JB/setup %}


Hasta hace unas horas no sabia que podia usar el Acelerometro (lis3lv02d) que tiene mi laptop en Linux, tan solo sabia que lo usa en Windows la aplicacion HP 3D DriveGuard para proteger el disco duro en casos de una posible caida  y golpe contra el suelo. Pero en Linux es posible sacarle provecho al acelerometro para algo mas que proteger el disco duro.

<img class="aligncenter size-medium wp-image-504" title="3757_8721" src="http://blog.jam.net.ve/imagenes/uploads/2010/11/3757_8721-300x200.jpg" alt="" width="300" height="200" />

Una manera de saber que nuestra laptop posee un acelerometro es tecleando en la terminal:

{% highlight bash %}
cat /sys/devices/platform/lis3lv02d/position
{% endhighlight %}

si nos devuelve algo como:

{% highlight bash %}
(18,36,936)
{% endhighlight %}

entonces quiere decir que tenermos un acelerometro correctamente reconocido por Linux, el valor en (18,36,936) representa el eje X,Y,Z .

Buscando en google me encontre con un script en Bash el cual usa el acelerometro de la laptop para rotar las caras del cubo de escritorio de Compiz. el script en cuestion se encuentra en los <a href="https://bbs.archlinux.org/viewtopic.php?id=78031">foros de ArchLinux</a> y fue escrito por el usuario <a href="https://bbs.archlinux.org/viewtopic.php?id=78031">SamoTurk</a>.

Este script requiere que tengamos instalado el paquete wmctrl, por lo que si no lo tienes aun tendras que instalarlo tecleando en la terminal:

{% highlight bash %}
sudo aptitude install wmctrl
{% endhighlight %}

En realidad son dos script:

{% highlight bash %}
#!/bin/bash
# lis3lv02d-rotate
#
# Author: Samo Turk
#
# Released under GPLv3
COUNTER=0
while [  $COUNTER -lt 100 ]; do
sleep 2
POS=`cat /sys/devices/platform/lis3lv02d/position | awk -F , '{print$1}' | awk -F "(" '{print$2}'`
echo $POS
if [ $POS -ge 350 ]; then
./compiz-rotate-wmctrl left
elif [ $POS -le -350 ]; then
./compiz-rotate-wmctrl right
fi
let COUNTER=COUNTER+1
done
{% endhighlight %}

Este script lo guardaremos en un archivo llamado "lis3lv02d-rotate"

{% highlight bash %}
#!/bin/bash
#
# compiz-rotate-wmctrl - Rotate the cube using wmctrl
#
# Author: Shang-Feng Yang
# Released under GPLv3
VER="1.0"
function rotate() {
# The target face number (begins with 0)
TVPN=$(( $1 % ${NF} ))
# The X coordinate of the target viewport
TVPX=$(( ${TVPN} * ${WW} ))
# Change to the target viewport
wmctrl -o ${TVPX},0
}
function usage() {
echo -e "$(basename $0) v${VER}\n"
echo -e "Usage:\n"
echo -e "\t$(basename $0) {left|right|#}\n"
echo -e "\tWhere:\n"
echo -e "\t\tleft - rotate the cube to the left"
echo -e "\t\tright - rotate the cube to the right"
echo -e "\t\t# - rotate to #th face (begins with 0)\n\n"
echo -e "Author: Shang-Feng Yang "
echo -e "Released under GPLv3"
}
# The action to be performed. $ACT could be 'left' or 'right' to rotate
# left or right, accordingly. $ACT could also be the number of the face
# to rotate into.
ACT=$(echo $1 |tr '[A-Z]' '[a-z]')
[ "x$ACT" == "x" ] && { usage; exit 1; } || {
case $ACT in
left|right|[0-9]|[0-9][0-9])
;;
*)
usage
exit 1
;;
esac
}
# The informations about the desktop
INFO=$(wmctrl -d)
# The width of the desktop
DW=$(echo "${INFO}"| awk '{sub(/x[0-9]+/, "", $4); print $4}')
# The width of the workarea
WW=$(echo "${INFO}"| awk '{sub(/x[0-9]+/, "", $9); print $9}')
# The number of faces on the cube
NF=$(($DW/$WW))
# The X coordinate of the viewport
CVPX=$(echo "${INFO}" |awk '{sub(/,[0-9]+/, "", $6); print $6}')
# Current number of the face in all faces (begins with 0)
CVPN=$(( ${CVPX} / ${WW} ))
[ "$ACT" == "right" ] && {
ACT=$(( ${CVPN} + 1 ))
} || {
[ "$ACT" == "left" ] && {
ACT=$(( ${CVPN} - 1 ))
}
}
rotate ${ACT}
{% endhighlight %}

Y este segundo script lo guardaremos en un archivo llamado "compiz-rotate-wmctrl" en la misma carpeta donde esta el primer script luego le agregamos permisos de ejecucion a ambos archivos.

Para probar este script ejecutamos desde la terminal tecleando:

{% highlight bash %}
sh ./lis3lv02d-rotate
{% endhighlight %}

Ahora solo nos queda inclinar la laptop a la izquierda o derecha y el cubo de escritorio deberia cambiar  en ese sentido similar a como lo muestra este <a href="http://www.youtube.com/watch?v=CtWywn1zbjA">video</a>.

Otras de las utilidades que le posemos dar a el acelerometro es en los juegos NeverBall en el que podemos mover la esfera inclinando la laptop hacia los lados como se ve en este <a href="http://www.youtube.com/watch?v=a92VXK-mURk">video.</a>

Una tercera utilidad que encontre para el acelerometro es unirse al proyecto <a href="http://qcn.stanford.edu/">Quake-Catcher</a> Network en el cual se usan las laptops con acelerometros como una especie de sismografos conectados a internet y asi detectar posibles temblores y terremotos en tu localidad, lamentablemente  no todo el software que se necesita es soportado en Linux  y al parecer solo esta disponible para Mac y Windows.

Por ultimo siempre podremos volver a la utilidad principal para la que el fabricante coloco el acelerometro en las laptops, es decir Proteger nuestro disco duro. En linux podemos usar  el software HPfall el cual usara el acelerometro para detectar movimientos bruscos o caidas y proteger el disco duro en esas situaciones para asi evitar daños o perdida de datos.

Para instalar HPfall debemos agregar el repositorio del autor tecleando en la terminal:

{% highlight bash %}
sudo apt-add-repository ppa:pmjdebruijn/ppa
{% endhighlight %}

actualizamos la lista de paquetes

{% highlight bash %}
sudo aptitude update
{% endhighlight %}

ahora instalamos HPFALL

{% highlight bash %}
sudo aptitude install hpfall
{% endhighlight %}

Esto nos ejecutara un demonio en cada inicio el cual estara monitoreando junto con el acelerometro los movimientos para asi proteger el disco en caso de una caida.

Este software no tiene ninguna interfaz de configuracion, asi que no te sorprendas si estas buscando un icono en el menu aplicaciones y no encuentras nada, a fin de cuentas el HP 3D DriveGuard tampoco trae mucha cosa que se diga.

Me gustaria probar alguna otra utilidad pero de momento no encuentro mas, me gustaria un software en el que pueda ver en tiempo real los valores de X,Y,Z mientras muevo la laptop pero por ahora no e encontrado nada parecido mas que usar el comando cat /sys/devices/platform/lis3lv02d/position
