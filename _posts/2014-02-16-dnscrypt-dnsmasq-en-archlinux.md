---
layout: post
title: "DNSCrypt + DNSMasq en ArchLinux - Encripta tus peticiones DNS y saltate
cualquier restrincion de tu ISP."
tags: [dnsmasq, dnscrypt, venezuela, linux, censura, archlinux]
---

Hace [algo de tiempo](http://blog.jam.net.ve/2010/08/20/vuela-en-internet-usando-una-cache-dns-dnsmasq-en-ubuntu/) ya escribi un articulo de como acelerar un poco el internet
usando DNSMasq como una cache DNS, en esta ocasion vamos a mejorar un poco la
seguridad de nuestra conexion a internet con la ayuda de [DNSCrypt](http://dnscrypt.org/).

DNSCrypt nos provee un servicio local que puede ser usado directamente como
resolvedor o redireccionador DNS, encriptando y autenticando las peticiones DNS
usando el protocolo DNSCrypt y pasandolos a un servidor superior. Estas
propiedades de DNSCrypt nos permite entonces encriptar las peticiones DNS de
forma que ningun proxy o ISP pueda capturarlas y/o modificarlas para espiarte o
bloquearte determinadas paginas.

En este ejemplo yo usare ArchLinux ya que es la distro que uso actualmente, pero
la informacion es facilmente aplicable a otras distros como Ubuntu o Debian, en
estas dos ultimas distros linux se requiere compilar e instalar aparte
[Libsodium](https://github.com/jedisct1/libsodium) ya que si mal no recuerdo
hasta la fecha no existen paquetes en sus repositorios.

<!-- more -->

#Instalando DNSCript y DNSMasq.

Para instalarlos en ArchLinux tan solo ejecutamos en la terminal:

{% highlight console %}
$ sudo pacman -S dnsmasq dnscrypt-proxy
{% endhighlight %}

NOTA: En los repos de ArchLinux cuenta con el paquete libsodium el cual debe
instalarse para poder usar DNSCrypt, aqui es instalado automaticamente como
dependencia, pero si estas en alguna otra distro como Debian o Ubuntu deberas
descargar [Libsodium](https://github.com/jedisct1/libsodium) compilarlo e
instalarlo.

#Configurando Dnsmasq para que trabaje junto a Dnscrypt.

Para que Dnsmasq trabaje con Dnscrypt y asi cachear las peticiones dns de
dnscrypt tan solo debemos agregar o descomentar las siguientes lineas en su
archivo de configuracion que deberia estar en **/etc/dnsmasq.conf** 

{% highlight bash linenos %}
# Configuration file for dnsmasq.
#
# Format is one option per line, legal options are the same as the
# long options legal on the command line. See
# "/usr/sbin/dnsmasq --help" or "man 8 dnsmasq" for details.
 
# Don't read the hostnames in /etc/hosts.
no-hosts
 
# Do not go into the background at startup but otherwise run as
# normal.
keep-in-foreground
 
# Do not provide DHCP or TFTP on the loopback interface.
no-dhcp-interface=lo
 
# Only listen on the loopback interface.
listen-address=127.0.0.1
 
# Only bind to interfaces dnsmasq is listening on.
bind-interfaces
 
# Never forward addresses in the non-routed address spaces.
bogus-priv
 
# Don't read /etc/resolv.conf.
no-resolv
 
# Reject (and log) addresses from upstream nameservers which are in
# the private IP ranges. This blocks an attack where a browser behind
# a firewall is used to probe machines on the local network.
stop-dns-rebind
 
# Exempt 127.0.0.0/8 from rebinding checks. This address range is
# returned by realtime black hole servers, so blocking it may disable
# these services.
rebind-localhost-ok
 
# Never forward plain names (without a dot or domain part).
domain-needed
 
# Upstream server is dnscrypt-proxy on local machine.
server=127.0.0.2
 
# Set the cache size here. If you don't use spam blocking add-ons such
# Adblock Plus or Ghostery, you may want to increase this value as you
# will be resolving more domain names.
cache-size=1000
 
# Pass through DNSSEC validation results from dnscrypt-proxy.
proxy-dnssec
{% endhighlight %}


Si se fijan en la configuracion indicamos una IP de escucha en
**listen-address=127.0.0.1** esta IP sera la que luego colocaremos en nuestra
interfaz de red como servidor DNS para asi redireccionar todas las peticiones
DNS hacia Dnsmasq. Tambien podemos notar que especificamos un servidor en
**server=127.0.0.2** esta sera la direccion IP en la que DNScrypt esta
escuchando peticiones.

#Configurando Dnscrypt.

Bien si de casualidad no lo has notado, hay que hacer un pequeno ajuste para
correjir un conflicto, y es que por defecto tanto DNSMasq como Dnscrypt escuchan
usando la misma direccion IP local, lo cual no deberia ser. Para corregir esto y
adaptarlo a la configuracion que ya tenemos hecha para Dnsmasq editaremos el
archivo **/etc/conf.d/dnscrypt-proxy** el cual probablemente contenga esto:

{% highlight bash linenos %}
DNSCRYPT_LOCALIP=127.0.0.1
DNSCRYPT_LOCALPORT=53
DNSCRYPT_USER=nobody
DNSCRYPT_PROVIDER_NAME=2.dnscrypt-cert.opendns.com
DNSCRYPT_PROVIDER_KEY=B735:1140:206F:225D:3E2B:D822:D7FD:691E:A1C3:3CC8:D666:8D0C:BE04:BFAB:CA43:FB79
DNSCRYPT_RESOLVERIP=208.67.220.220
DNSCRYPT_RESOLVERPORT=443
{% endhighlight %}

Aqui solo cambiaremos el contenido de la linea que dice
**DNSCRYPT_LOCALIP=127.0.0.1** y cambiaremos la IP por ADIVINEN!!!
**127.0.0.2**.

#Configurando nuestra interfaz de red:

Una vez realizada la configuracion de Dnsmasq y Dnscrypt tan solo resta adaptar
nuestra interfaz de red de internet y ajustarla para que use como unico servidor
DNS la IP **127.0.0.1** esta es la IP local de nuestra PC y la misma IP a la
cual esta escuchando Dnsmasq. es probable que requieras reiniciar tu interfaz de
red para que los cambios tengan efecto.

#Ejecutando los servicios y primera prueba:

Con todo esto ya tenemos listo nuestro encriptado de peticiones DNS y chacheado
de las mismas para una mayor seguridad, evitar la vigilancia y saltar la censura
de tu ISP o Gobierno.

En ArchLinux basta con ejecutar:

{% highlight console %}
$ sudo systemctl enable dnscrypt-proxy.service
$ sudo systemctl enable dnsmasq.service
{% endhighlight %}

Para habilitar los servicios y luego para arrancar:

{% highlight console %}
$ sudo systemctl start dnscrypt-proxy.service
$ sudo systemctl start dnsmasq.service
{% endhighlight %}

Bien, para esta prueba podemos hacer una simple consulta DNS con el comando
**dig** a alguna URL que sepamos esta censurada por nuestro Proveedor de
internet, en mi caso mi proveedor es **CANTV** el cual pertenece al Gobierno
Venezolano y una de las paginas muy conocidas que esta siendo censuradas desde
hace tiempo por el Gobierno de Venezuela es [DolarToday](http://dolartoday.com/).

Si yo realizo una consulta dig a **dolartoday.com** seguro obtendre algo como
esto:

{% highlight console %}
 <<>> DiG 9.9.2-P2 <<>> dolartoday.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34898
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;dolartoday.com.			IN	A

;; ANSWER SECTION:
dolartoday.com.		299	IN	A	

;; Query time: 316 msec
;; SERVER: 200.44.32.12#53(200.44.32.12)
;; WHEN: Sun Feb 16 12:36:53 2014
;; MSG SIZE  rcvd: 59
{% endhighlight %}

Notese que en la columna de registros **A** no tenemos absolutamente nada, es
decir no nos estan dando la IP del servidor de DolarToday.com  para poder
conectar y cargar la pagina. Notese tambien la IP **200.44.32.12**  esta es la
IP de uno de los servidores DNS de CANTV los cuales se agregan automaticamente
cuando conectas a internet con dicho proveedor.

Con Dnsmasq, Dnscrypt ejecutandose y la interfaz de red configurada y lista, al
realizar la misma consulta DNS con **dig** obtendriamos algo como esto:

{% highlight console %}
 <<>> DiG 9.9.2-P2 <<>> dolartoday.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34898
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;dolartoday.com.			IN	A

;; ANSWER SECTION:
dolartoday.com.		299	IN	A	108.162.207.195

;; Query time: 316 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Sun Feb 16 12:36:53 2014
;; MSG SIZE  rcvd: 59
{% endhighlight %}


Ahora si!!! puedes notarse como se nos entrega un valor en la columna **A** la
cual es la IP del servidor donde esta alojada la web a la que intentamos acceder
y que esta bloqueada por nuestro ISP. Notese tambien que el servidor al que se
envia la consulta DNS es la IP **127.0.0.1** el cual es nuestra misma PC y la IP
es en donde esta escuchando Dnsmasq por las peticiones DNS que le solicitemos
para que este a su vez se las solicite a Dnscrypt y este a su vez realice una
consulta **SEGURA** y **ENCRIPTADA** a un servidor DNS confiable y libre de
censuras.

Probablemente te preguntaras a que servidor **Confiable** esta Dnscrypt
realizando las consultas DNS, pues arriba en la configuracion de Dnscrypt esta
una pista: **DNSCRYPT_RESOLVERIP=208.67.220.220** y
**DNSCRYPT_PROVIDER_NAME=2.dnscrypt-cert.opendns.com**. Esta direccion IP
pertenece al servicio [OpenDNS](http://www.opendns.com) el cual es el servicio
con el que viene configurado por defecto Dnscrypt.

Opendns sirve muy bien para realizar el trabajo que deseamos el cual es
saltarnos restrinciones, pero si lo deseas puedes cambiarlo por algun otro, en
la pagina de [Dnscrypt](http://dnscrypt.org/) puedes encontrar una lista de
actuales proveedores de servicios DNS con Dnscrypt activado como por ejemplo
[CloudNS](https://cloudns.com.au/) de Australia, [OpenNIC](http://www.opennicproject.org/) con servidores en varias partes del mundo, [DnsCrypt.eu](http://dnscrypt.eu/) con servidores en Holanda y Dinamarca y [Soltysiak.com](http://dc1.soltysiak.com/) con servidores en Polonia.


