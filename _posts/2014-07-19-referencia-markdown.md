---
layout: post
title: "Referencia Markdown"
tags: [linux, markdown]
---

Segun la Wikipedia:

> Markdown es un lenguaje de marcado ligero creado originalmente por John Gruber y Aaron Swartz que trata de conseguir la máxima legibilidad y "publicabilidad" tanto en sus forma de entrada como de salida, inspirándose en muchas convenciones existentes para marcar mensajes de correo electrónico usando texto plano. Markdown convierte el texto marcado en documentos XHTML bien formados, reemplazando el signo 'menor que' ('<') y los et por sus correspondientes referencias de entidad de caracteres. Markdown fue implementado originariamente en Perl por Gruber, pero desde entonces ha sido traducido a multitud de lenguajes de programación, incluyendo PHP, Python, Ruby, Java y Common Lisp. Se distribuye bajo licencia BSD y se distribuye como plugin (o al menos está disponible) en diferentes sistemas de gestión de contenidos (CMS).

<!-- more -->

Hago este articulo a modo de referencia debido a que por lo general cuando tengo
que formatear texto para algun comentario o algun articulo de este blog, lo hago
en **Markdown** y siempre se me olvidan la sintaxis por lo que tengo que correr
a a buscar un sitio para referencias. Con esto ya sabre que lo unico que tengo 
que buscar es mi propio blog xD.

Cuando escribes un comentario, un articulo, un correo por lo general lo haces
en texto plano y sin formato o con un formato muy pobre que podria perderse al
publicar dicho texto, con un comentario en algun foro o un articulo en un blog
es probable que le quieras dar algo de formato, como por ejemplo resaltar un
texto, agregar un enlace o crear una lista simple. En un correo o un articulo
de uhn blog por ejemplo la solucion seria escribir el contenido en HTML, pero
escribir HTML para formatear un texto podria ser un suplicio ya que necesitarias
escribir muchas etiquetas y muy probablemente necesitaras agregar estilos CSS
para ayudar al formateado del texto. Es aqui donde **Markdown** te ayuda ya que
al tener una sintaxis sencilla y basica te sera mas facil escirbir y formatear
el texto. 

Hay que tener en cuenta que markdown no es un reemplazo de HTML y
muchas de las etiquetas existentes en HTML no estan disponibles para Markdown,
para estos casos lo que se debe hacer es simplemente usar la forma HTML.

# Cabeceras:

Markdown soporta dos estilos de cabeceras, el estilo [Setex](http://docutils.sourceforge.net/mirror/setext.html)
y el estilo [Atx](http://www.aaronsw.com/2002/atx/)

### Estilo Atx:

En HTML necesitarias escribir una cabecera con las etiquetas `<h1>` y `</h1>` 
pero en markdown basta con solo escribir el simbolo `#` para obtener una 
cabecera `<h1>`. Este estilo acepta los 6 niveles tal cual lo hace las etiquetas
`<h1>`.

Teniendo esto en cuenta y para obtener algo como esto:

# Texto con cabecera h1

## Texto con cabecera h2

### Text con cabecera h3

Necesitariamos escribir algo como esto: 

{% highlight markdown %}
# Texto con cabecera h1

## Texto con cabecera h2

### Text con cabecera h3
{% endhighlight %}

### Estilo Setex:

Este estilo acepta unicamente dos niveles de la etiqueta `<h1>`

Si quieres obtener algo como esto:

Texto con nivel h1
==================

Texto con estilo h2
-------------------

Debes escribir algo como esto:

{% highlight markdown %}
Texto con nivel h1
==================

Texto con estilo h2
-------------------

{% endhighlight %}


# Parrafos:

En HTML si quieres indicar que escribes un parrafo debes usar la etiqueta `<p>`
y `</p>`. Pero en Markdown no es necesario esto, de hecho no es necesario nada,
 simplemente escribes una lineas de texto continuas y sin espacio y markdown 
 tomara esta linea como un parrafo. Por ejemplo este parrafo explicativo se
 obtiene tan solo con escribir algo como esto:

 {% highlight markdown %}
En HTML si quieres indicar que escribes un parrafo debes usar la etiqueta `<p>`
y `</p>`. Pero en Markdown no es necesario esto, de hecho no es necesario nada,
 simplemente escribes una lineas de texto continuas y sin espacio y markdown 
 tomara esta linea como un parrafo. Por ejemplo este parrafo explicativo se
 obtiene tan solo con escribir algo como esto:
 {% endhighlight %}

No tiene ningun misterio...

# Citas:

En HTML probablemente has escrito citas con las etiquetas `<blockquote>`, pero
en Markdown es tan facil como colocar un `>` al inicio del texto de la cita.

Por ejemplo el extracto de Wikipedia que ves arriba es una **cita** que se
obtubo escribiendo algo como esto:

{% highlight markdown %}
> Markdown es un lenguaje de marcado ligero creado originalmente por John Gruber y Aaron Swartz que trata de conseguir la máxima legibilidad y "publicabilidad" tanto en sus forma de entrada como de salida, inspirándose en muchas convenciones existentes para marcar mensajes de correo electrónico usando texto plano. Markdown convierte el texto marcado en documentos XHTML bien formados, reemplazando el signo 'menor que' ('<') y los et por sus correspondientes referencias de entidad de caracteres. Markdown fue implementado originariamente en Perl por Gruber, pero desde entonces ha sido traducido a multitud de lenguajes de programación, incluyendo PHP, Python, Ruby, Java y Common Lisp. Se distribuye bajo licencia BSD y se distribuye como plugin (o al menos está disponible) en diferentes sistemas de gestión de contenidos (CMS).
{% endhighlight %}

### Cita anidada:

Puedes anidar una cita dentro de otra como por ejemplo esta:

> Una cita principal.
>
> > Una cita anidada.
>

La cual se lograria con algo como:

{% highlight markdown%}
> Una cita principal.
>
> > Una cita anidada.
>
{% endhighlight %}

Tambien puedes formatear las citas agregandole elementos markdown dentro de
ellas.

# Listas:

En HTML tu creas una lista con etiquetas como `<ol>` y `<li>`.
Markdown soporta listas tanto ordenadas como no-ordenadas.

### Listas no-ordenadas:

Las listas no-ordenadas las puedes escribir con los simbolos `+`, `-` o `*`
como marcador de lista, por lo que si quieres hacer algo como esto:

* ArchLinux.
* Ubuntu.
* Debian.

Se usaria algo como esto:

{% highlight markdown %}
* ArchLinux.
* Ubuntu.
* Debian.

es igual a

- ArchLinux.
- Ubuntu.
- Debian.

y es igual a

+ ArchLinux.
+ Ubuntu.
+ Debian.
{% endhighlight %}

### Listas ordenadas:

Las listas ordenadas las escribes simplemente con numeros seguidos de un punto.
Asi que si quieres crear algo como esto:

1. ArchLinux.
2. Ubuntu.
3. Debian.

Escribiras algo como:

{% highlight markdown %}
1. ArchLinux.
2. Ubuntu.
3. Debian.
{% endhighlight %}

Un detalle a tener en cuenta es que el orden de los numeros que coloques para
marcar una lista ordenada no tiene efectos al ser convertido a HTML por lo que
si escribes algo como:

{% highlight markdown %}
1. ArchLinux.
1. Ubuntu.
1. Debian.

o escribes algo como

1. ArchLinux.
3. Ubuntu.
5. Debian.
{% endhighlight %}

siempre obtendras una lista ordenada similar al ejemplo de arriba.

# Bloques de codigo:

Puedes escribir codigo fuente con bloques de codigo pre-formateados, HTML hace
esto usando las etiquetas `<pre>` y `<code>`, pero en Markdown tu escribes
los bloques de codigo identando el mismo codigo con 4 espacios o un tab.

Por ejemplo si queremos mostrar un bloque de codigo fuente como este:

    def metodo_ruby
      puts "Hola mundo"
    end

Deberas escribir algo como esto:

~~~ ruby
    def metodo_ruby
      puts "Hola mundo"
    end
~~~

Notese los 4 espacios antes de la palabra clave `def` de la funcion los cuales 
van consecutivos hasta la palabra clave `end` que cierra la funcion.

# Reglas horizontales:

En HTML tu crearias una linea o regla horizontal usando la etiqueta `<hr>`,
pero en markdown las puedes hacer repitiendo los simbolos `*` y `-`

Para conseguir las siguientes cuatros reglas (si, probale que no las veas bien):

* * *


***


*****


- - -


-----------------


Necesitaras escribir algo como esto:

{% highlight markdown %}
* * *


***


*****


- - -


-----------------
{% endhighlight %}

# Enlaces:

En HTML los enlaces se escriben usando la etiquetas `<a>` pero en markdown
se hace tan solo con rodeando el texto del enlace con `[]` y justo al lado 
colocas la url del enlace rodeada con `()`.

Por ejemplo el siguiente enlace:

[Jam Blog](http://blog.jam.net.ve)

lo logramos escribiendo algo como:

{% highlight markdown %}
[Jam Blog](http://blog.jam.net.ve)
{% endhighlight %}

Tambien se puede agregar identificadores a los enlaces para luego agrupar estos
todos juntos en cualquier parte del documento, esto como una forma de tenerlos
ordenados para facil edicion.

Por ejemplo los siguientes grupos de enlaces:

[Ubuntu][1]
[Arch Linux][2]
[Debian][3]

[1]: http://ubuntu.com "Linux para seres humanos."
[2]: https://archlinux.org
[3]: http://debian.org

Se obtienen escribiendo lo siguiente:

{% highlight markdown %}
[Ubuntu][1]
[Arch Linux][2]
[Debian][3]

[1]: http://ubuntu.com "Linux para seres humanos."
[2]: https://archlinux.org
[3]: http://debian.org
{% endhighlight %}

Notese el texto opcional que se muestra al colocar el cursor sobre el enlace
de _Ubuntu._

# Enfasis:

En HTML si quieres hacer notar un texto negritas o haciendolo cursivo usas las 
etiquetas `<strong>` y `<em>` respectivamente, pero en markdown logras el mismo
efecto usando `*` y `_`.

Por ejemplo:

*Pablito* clavo un _clavito_ y el **clavito** __clavo__ a Pablito.

lo puedes lograr escribiendo:

{% highlight markdown %}
*Pablito* clavo un _clavito_ y el **clavito** __clavo__ a Pablito.
{% endhighlight %}

Como puedes notar se puede lograr el texto negrita usando solo un `_` o un `*` 
y el texto cursivo se puede lograr usando dos `**` o dos `__` al inicio y al 
final de la palabra.

# Codigo simple:

Ya habiamos visto como escribir **bloques de codigo** mas arriba, pero esta vez
veremos como escribir codigo fuente de una sola linea.

En HTML lo escribes usando la etiqueta `<code>`, usando markdown se logra con
el `` ` ``

Por ejemplo:

`puts "Hola Markdown" if Markdown.include?`

`` `mosca` `` que el simbolo es `` ` `` y no `'`.

Le hace escribiendo:

{% highlight markdown %}
`puts "Hola Markdown" if Markdown.include?`

`` `mosca` `` que el simbolo es `` ` `` y no `'`.
{% endhighlight %}

Notese que si se quiere incluir un texto con que contiene el mismo simbolo `` ` ``
debes rodear el contenido con un doble `` ` ``

# Imagenes:

En HTML agregas imagenes al documento usando la etiqueta `<img>`, con markdown
se hace de una forma muy similar a como se hacen con los enlaces, con la unica
diferencia de que se usa un simbolo `!` al inicio de los `[]` y en los `()` se
coloca la ruta de la imagen.

Por ejemplo:

![Markdown](https://i.imgur.com/Mz0i3G8.png "Logo Markdown")

Se puede lograr escribiendo:

{% highlight markdown %}
![Markdown](https://i.imgur.com/Mz0i3G8.png "Logo Markdown")
{% endhighlight %}

Notese que a pesar de que se puede colocar el texto `alt` y el `title`
existentes en la etiqueta `<img>` HTML, no podemos controlar la dimension de la
imagen ni la posicion. Asi que asegurate de que la imagen ya este en las 
dimensiones deseadas o usa solo la etiqueta HTML `<img>` y codigo CSS.

De la misma forma que hicimos con los enlaces, podemos agrupar imagenes
con un identificador.


# Miselaneos:


### Enlaces automaticos:

Cuando vimos como formatear enlaces en Markdown lo hicimos con algo como
`[texto enlace](http://url.tld)`, pero markdown de hecho tiene una forma
simple de convertir una url escrita en un enlace basico:

<http://blog.jam.net.ve>

<correo@dominio.tld>

Se logra simplemente escribiendo:

{% highlight markdown %}
<http://blog.jam.net.ve>

<correo@dominio.tld>
{% endhighlight %}

### Quiebre de linea:

Si por ejemplo quieres escribir una linea  
y romperla en un punto especifico tan solo  
debes agregar dos o masespacios en el  punto  
donde quieres que se haga el salto de linea.

Como puedes notar el parrafo explicativo de arriba no es tan largo, pues se
incluyo en el el quiebre de linea el cual se obtubo escribiendo:

~~~
Si por ejemplo quieres escribir una linea  
y romperla en un punto especifico tan solo  
debes agregar dos espacios en el  punto donde  
quieres que se haga el salto de linea.
~~~

Notese los dos espacios al final de cada linea para marcar el quiebre o salto.

### Escape:

Markdown nos da una forma para escribir simbolos que el mismo usa en su sintaxis
como por ejemplo el `*`, `-`, `_`, etc.

\*Texto rodeado con `*`\*

\_Texto rodeado con `_`\_

Esto se logra escribiendo:

{% highlight markdown %}
\*Texto rodeado con `*`\*

\_Texto rodeado con `_`\_
{% endhighlight %}

Tambien hay caracteres de escape para los siguientes simbolos:

    \   backslash
    `   backtick
    *   asterisk
    _   underscore
    {}  curly braces
    []  square brackets
    ()  parentheses
    #   hash mark
    +   plus sign
    -   minus sign (hyphen)
    .   dot
    !   exclamation mark

Como ven, markdown es sumamente sencillo y basico con una sintaxis facil de
escribir. Existen algunas reglas especificas para cada algunos elementos que no
se describen aqui, si deseas  puedes visitar la [referencia oficial](http://daringfireball.net/projects/markdown/syntax)
