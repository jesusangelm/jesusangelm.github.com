---
layout: post
title: "Autenticacion SSH basada en llaves publicas y privadas."
tags: [linux, ssh, servidor]
---

Por lo general cuando uno va a administrar un servidor o VPS de forma remota,
lo hace mediante una conexion SSH y por lo general inicias sesion usando un nombre
de usuario y clave. A pesar de que estas conexiones SSH son seguras, la forma de
autenticarse con usuario y clave no lo es del todo ya que esta expuestas a posibles
ataques mediante fuerza bruta. Para tener un poco mas a segurado nuestros servidores 
o VPS es aconsejable la autenticacion pero usando llaves SSH y desactivando la
autenticacion con claves.

<!-- more -->

Para realizar esto tan solo debemos realizar unos pocos pasos:

# Subiendo tu llave SSH publica al servidor:

Para poder autenticarnos en un servidor usando llaves SSH lo primero que podemos
hacer es subir nuestra llave publica, estas, cuando las creas, por defecto son 
un archivo llamado `id_rsa.pub` ubicado en la carpeta `~/.ssh/` en tu **PC**.

El contenido de esta llave publica SSH `id_rsa.pub` debemos colocarlo en el
**servidor**, en un archivo llamado `authorized_keys` ubicado en la carpeta `~/.ssh`
en el servidor.

# Configurando el servidor OpenSSH para autenticacion con llaves:

Una vez subida al servidor la llave publica, toca realizar algunas configuraciones
para autenticarnos usando dicha llave. Es probable de que si en este punto intentas
autenticarte en el servidor, puedas realizarlo sin problemas usando la llave SSH
pero la idea es que solo se permitan los accesos y autenticacion solo con llaves 
y no con claves.

Para realizar esto necesitamos editar en el **servidor** el archivo 
`/etc/ssh/sshd_config` y cambiar o agregar las siguientes lineas de modo que 
queden como esta:


{% highlight bash %}
PubkeyAuthentication yes
PasswordAuthentication no
ChallengeResponseAuthentication no¬
UsePAM no
{% endhighlight %}


La primera y la segunda linea son las mas importantes, `PubkeyAuthentication yes`
permite la autenticacion mediante llaves SSH, y `PasswordAuthentication no` 
deshabilita la autenticacion mediante claves.

Con esto ya puedes conectarte a tu servidor o VPS usando tu llave publica SSH
y estar un poco mas tranquilo ya que con esto le agregas un poco mas de seguridad
a tu servidor. 

Pero ya que estamos, podriamos mejorar un poco mas la seguridad del servidor
haciendo algunos ajustes extras:

# Desactivando la autenticacion para el usuario root:

El usuario **root** es el usuario con los mayores permisos en el sistema, iniciar
sesion en el servidor con este usuario es arriesgado ya que con el mas minimo error
en un comando es posible que produscas fallas irreparables en el sistema operativo.

Desactivar la autenticacion del usuario root tambien nos permite agregar una capa
mas de seguridad al impedir que inicien sesion como root algun atacante que haya
logrado conseguir la clave del usuario root o su llave ssh.

Para realizar esto necesitamos editar en el **servidor** el archivo 
`/etc/ssh/sshd_config` y cambiar o agregar las siguientes lineas de modo que 
queden como esta:

{% highlight bash %}
PermitRootLogin no
{% endhighlight %}

**Nota** Recuerda habilitar esta opcion solo despues de darle permisos de
administrador a algun usuario standar. por ejemplo agregando tu usuario al archivo
en `/etc/sudoers`

# Permitir acceso solo a ciertos usuarios:

Otra forma de aumentar la seguridad es permitir el acceso solo a determinados 
usuarios. Para realizar esto necesitamos editar en el **servidor** el archivo 
`/etc/ssh/sshd_config` y cambiar o agregar las siguientes lineas de modo que 
queden como esta:

{% highlight bash %}
AllowUsers mi-usuario pepito fulanito
{% endhighlight %}

De la misma forma podrias usar la directiva `AllowGroup` para permitir unicamente
a cierto grupo autenticarse en el servidor.

Una vez terminado tan solo necesitamos reiniciar OpenSSH y tendremos activa todas
estas configuraciones.

Con esto ya aumentamos un poco mas la seguridad en nuestro servidor, logicamente
se podrian realizar mas ajustes o agregar por ejemplo un sistema que utilice el 
firewall para bloquear el acceso a las IP que hayan tenido una cierta cantidad
de intentos fallidos de autenticacion. Esto ultimo lo explicare un poco mas adelante.

