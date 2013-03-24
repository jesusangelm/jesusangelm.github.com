---
layout: post
title: "Entendiendo la notacion octal de los permisos de sistemas en Linux"
tags: [linux, seguridad, tutorial]
---
# Entendiendo la notacion octal de los permisos de sistemas en Linux

{% include post_header.html %}

Si administras un servidor, una cuenta de hosting o usas una distro Linux es muy probable que en algun momento hayas tenido que cambiar los permisos a alguna carpeta o archivo. En sistemas Linux comunmente se usa el comando chmod seguido de un conjunto de letras y simbolos (notacion simbolica) o seguido de una cifra de 3 digitos (notacion octal), pero en ocasiones usamos estos permisos sin saber que significan o que estan haciendo realmente ya que copiamos el comando de alguna guia o pagina.

Bien en esta ocasion explicare un poco como es el funcionamiento de la notacion octal y como saber el significado de esos numeros que colocamos.

En primer lugar la notacion octal consiste en un conjunto de valores de 3 o 4 digitos en base 8. cuando escribimos un permiso en notacion octal de 3 digitos, cada numero representa un un componente de permisos a establecer.

Para saber que permisos le estamos asignando a un archivo o carpeta podemos valernos del significado de cada numero. por ejemplo:

4 - <span style="color: #00ff00;">Lectura</span>

2 - <span style="color: #3366ff;">Escritura</span>

1 - <span style="color: #ff0000;">Ejecucion</span>

La posicion de estos numeros en la cifra tambien tiene un significado, por ejemplo:

{% highlight text %}
7 x x
{% endhighlight %}

La primera posicion en la cifra significa que ese permiso sera valido para el usuario (propietario del archivo o carpeta).

{% highlight text %}
x 7 x
{% endhighlight %}

La segunda posicion en la cifra significa que ese permiso sera valido para el grupo.

{% highlight bash %}
x x 7
{% endhighlight %}

La tercera posicion en la cifra significa que ese permiso sera valido para el publico.

Si por ejemplo escribimos un comando como este:

{% highlight bash %}
chmod 421 archivo.txt
{% endhighlight %}

Lo que estariamos haciendo es:

- Permitirle al dueño <span style="color: #00ff00;">leer</span> (abrir/ver) el archivo.txt

- Permitirle al grupo <span style="color: #3366ff;">escribir</span> (editar) el archivo.txt

- Permitirle al resto de los usuarios o el publico <span style="color: #ff0000;">ejecutar</span> el archivo.txt

Hasta aqui todo se entiende a simple vista, pero de seguro te estaras preguntando ¿como hacer si quiero que el usuario tenga permisos de lectura-escritura y permisos de solo lectura a los grupos y el publico? Pues bien muy facil, los valores octales pueden conbinarse (sumarse), veamos este ejemplo:

{% highlight bash %}
chmod 644 archivo.txt
{% endhighlight %}

Aqui estariamos combinando (sumando) el valor octal para el permiso de <span style="color: #00ff00;">lectura</span> y el valor octal para el permiso de<span style="color: #00ffff;"> <span style="color: #3366ff;">escritura</span></span>, los que nos daria como resultado 6 que seria igual a el permiso <span style="color: #00ff00;">Lectura</span>-<span style="color: #3366ff;">Escritura</span>.  Al grupo y al publico se le asigna el valor octal 4 que seria el equivalente al permiso de solo <span style="color: #00ff00;">lectura</span>.

Otro caso podria ser este ejemplo:

{% highlight bash %}
chmod 750 archivo.txt
{% endhighlight %}

En este caso estariamos:

- Asignandole permisos de <span style="color: #00ff00;">lectura</span>-<span style="color: #3366ff;">escritura</span>-<span style="color: #ff0000;">ejecucion</span> al usuario.

- Asignandole permisos de <span style="color: #00ff00;">lectura</span>-<span style="color: #ff0000;">ejecucion</span> al grupo.

- Quitandole todo los permisos al publico.

En este caso al la posicion correspondiente al publico se le asigna el valor "0" lo que significa que no se le esta dando ningun tipo de permisos, es decir el publico no puede ver/abrir archivo.txt, no puede escribir/editar en archivo.txt ni tampoco puede ejecutar archivo.txt.

Despues de ver esto ya no seria problemas leer o asignar permisos a un archivo o una carpeta tanto en tu pc con  linux como en un servidor remoto o un hosting accesandi via FTP.

Espero les sirva tanto como a mi.
