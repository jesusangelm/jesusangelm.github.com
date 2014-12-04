---
layout: post
title: "Administrando multiples llaves SSH y repositorios Git"
tags: [linux, ssh, git]
---

Hay ocasiones en la que te encuentras con que tienes que usar multiples cuentas
GitHub, Bitbuket, Heroku o mas especifico, multiples cuentas en diversos
repositorios git. Esto puede deberse a que por ejemplo ya tengas cuenta personal 
en Github y alguna empresa para la que estes trabajando te pida crearte una nueva
cuenta GitHub usando una direccion de correo de dicha empresa. En estos casos y
si usas autenticacion via llaves SSH, puedes encontrarte con el inconveniente de 
que al hacer un `git pull`, `git push` o similares, git use la llave SSH que no 
corresponde a la cuenta que debes usar en ese servicio especifico. 

<!-- more -->

Para corregir esto y poder usar multiples llaves SSH y multiples cuentas de 
repositorios Git, podemos crear un archivo `config` de configuracion dentro de la carpeta
`~/.ssh` en la que espeficiquemos como trabajaremos con las multiples cuentas y 
llaves SSH en un mismo servicio o reporisorio Git.

{% highlight bash %}
#############################
# CONFIGURACION PARA GITHUB.#
#############################
#Cuenta GitHub Personal.
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa
  IdentitiesOnly yes

#Cuenta GitHub segundaria
Host segundaria.github.com
  HostName github.com
  User git
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_segundaria
  IdentitiesOnly yes
{% endhighlight %}


En este ejemplo podemos ver que tenemos dos cuentas GitHub a las cuales se acceden
desde una URL personalizada que especificamos con `Host`. 
Esta a su vez se le indica la llave SSH a usar mediante `IdentityFile` y el servidor
en donde se encuentra dicho servicio se especifica con `HostName`

Notese que en este ejemplo logicamente la URL **segundaria.github.com** no existe, 
esta URL tan solo la usamos para poder indicar la cuenta GitHub y su respectiva 
llave SSH que debera usar Git para identificarnos en GitHub.


De la misma forma podemos hacer algo muy similar con multiples cuentas en servicios
como Bitbucket o Heroku como podemos ver a continuacion en el siguiente archivo.

{% highlight bash %}
################################
# CONFIGURACION PARA BITBUCKET.#
################################
#Cuenta BitBucket Personal.
Host bitbucket.com
  HostName bitbucket.com
  User git
  IdentityFile ~/.ssh/id_rsa
  IdentitiesOnly yes

#Cuenta BitBucket segundaria
Host segundaria.bitbucket.com
  HostName bitbucket.com
  User git
  IdentityFile ~/.ssh/id_rsa_segundaria
  IdentitiesOnly yes

#############################
# CONFIGURACION PARA HEROKU.#
#############################
#Cuenta Heroku Personal.
Host heroku.com
  HostName heroku.com
  User git
  IdentityFile ~/.ssh/id_rsa
  IdentitiesOnly yes

#Cuenta Heroku segundaria
Host segundaria.heroku.com
  HostName heroku.com
  User git
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_segundaria
  IdentitiesOnly yes

{% endhighlight %}

Hay ocasiones en la que solo tienes una cuenta en algun servidor Git, pero igual
necesitas espeficicar que use una llave SSH especifica para poder autenticarnos
correctamente en dicho servidor. En esos casos podemos escribir algo como esto:

{% highlight bash %}
############################################
# CONFIGURACION PARA SERVIDOR GIT PERSONAL.#
############################################
#Cuenta Git Personal.
Host git.miservidor.net
  HostName git.miservidor.net
  User git
  IdentityFile ~/.ssh/id_rsa_gitpersonal
  IdentitiesOnly yes
{% endhighlight %}

Con esto hecho ya podemos comenzar a clonar repositorios usando el el comando:

{% highlight bash %}
$ git clone git@segundaria.github.com:jesusangelm/ConfVim.git
{% endhighlight %}

Con esto clonaremos dicho repo usando la cuenta **segundaria** en GitHub y su 
respectiva llave SSH.

Notese que pueden haber ocasiones en donde para hacer un `git pull` o `git push` 
necesitaras especificar manualmente la URL personalizada o alias dentro de la 
carpeta `.git/` en el archivo `config` en la carpeta principal de tu proyecto Git:

Cambiamos:

{% highlight bash %}
url = git@github.com:jesusangelm/jesusangelm.github.com.git
{% endhighlight %}

por:

{% highlight bash %}
url = git@segundaria.github.com:jesusangelm/jesusangelm.github.com.git
{% endhighlight %}
