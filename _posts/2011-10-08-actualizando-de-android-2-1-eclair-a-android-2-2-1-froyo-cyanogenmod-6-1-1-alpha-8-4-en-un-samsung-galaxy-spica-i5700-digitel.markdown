---
layout: post
title: "Actualizando de android 2.1 Eclair a Android 2.2.1 Froyo en un Samsung Galaxy Spica i5700 Digitel"
tags: [android, froyo, eclair, digitel]
---

Sigo aprendiendo cada vez mas sobre Android, aunque con algunos tropezones. Hace unas semanas comentaba como actualice mi <a title="Actualizar de Android 1.5 Cupcake a Android 2.1 Eclair en un Galaxy Spica I5700" href="http://blog.jam.net.ve/2011/09/17/actualizando-de-android-1-5-cupcake-a-android-2-1-eclair-en-un-samsung-galaxy-spica-i5700-digitel-venezuela/" target="_blank">Galaxy Spica I5700 de Android 1.5 Cupcake (Oficial Digitel) a Android 2.1 Eclair (Oficial Digitel)</a>, las mejoras eran ya muy notables en esa actualización pero... se puede mejorar mucho mas!!! si actualizamos a alguna de las tantas Rom personalizadas de Android 2.2 Froyo. Pues estuve leyendo sobre las ventajas de hacer una nueva actualización y a la final note que me convenía mucho.

<a href="http://imgur.com/qGAuu"><center><img src="http://i.imgur.com/qGAuu.jpg" title="Hosted by imgur.com" alt="" /></center></a>

<!-- more -->

Pues bien la room que elegí fue CyanogenMod 6.1.1 Spica Alpha 8.4 la cual esta basada en Froyo 2.2.1 e incluye mejoras interesantes como soporte 3D y soporte MultiTouch, al ser Froyo también corrige el bug en Eclair de la cámara que se queda oscura cuando se toman fotos estando conectada al Wifi. Por ser una room modificada, incluye un kernel actualizado con muchas mejoras como por ejemplo tener un <a title="Recovery Wiki en Samdroid.net" href="http://forum.samdroid.net/wiki/showwiki/Recovery" target="_blank">recovery</a> el cual es una muy buena utilidad que nos permitiria hacer cosas como por ejemplo ser root desde que enciendes el teléfono :D, hacer respaldos, aplicar actualizaciones y/o modificaciones comprimidas en .zip, instalar nuevas room, particionar la MicroSD, entre muchas otras funciones (tambien depende del kernel que instales).

**OJO estos pasos fueron realizados partiendo de un Samsung Galaxy Spica I5700 con Android 2.1 Eclair actualizado mediante Kies mini (Room oficial de samsung), si este no es tu caso NO HAGAS NADA!!!** ya que podrías tener un kernel distinto que podría no ser compatible con los que aquí se usan.

**Notas antes de comenzar, si no cumples con algunas de estas notas NO HAGAS NADA!!!**

* Tu teléfono debe estar cargado al 100%. lo mismo va en caso de que estés desde una Laptop, y muy recomendable estar conectado a un UPS, no valla a ser que **CortoElec** le de por quitarte la luz en pleno proceso de actualización.

* En el teléfono ve a <strong>“Configuración”</strong> o <strong>“Ajustes”</strong>  luego <strong>“Aplicaciones”</strong>  luego <strong>“Desarrollo”</strong> y por ultimo asegurare de que <strong>“Depuración de USB”</strong> esta marcada.

* Entra en teléfono como si fueses a marcar un numero para llamar, pero teclea <strong>*#7284#</strong> y verifica que <strong>UART</strong>  y <strong>USB</strong> <a href="http://jam.net.ve/capt/phoneutils.png" target="_blank">esten marcados en <strong>PDA</strong></a>.

* Has un <a title="respaldo" href="../tag/respaldo/">respaldo</a> de tus contactos y archivos en tu MicroSD. recomendable sincronizar los contactos con tu cuenta de Google/Gmail para que queden respaldados allí y luego puedas recuperarlos fácilmente.

* Recomendable: instalar la aplicación <a href="https://market.android.com/details?id=com.riteshsahu.APNBackupRestore&amp;feature=search_result" rel="nofollow">APN Backup &amp; Restore</a> para que respaldes tus APN la guardes en la memoria MicroSD o tu PC y las puedas restaurar luego.

* Si harás la actualización en una PC de <a title="escritorio" href="../tag/escritorio/">escritorio</a> conecta el cable USB del teléfono a un conector USB que sea directo a la Tarjeta Madre de la PC. no uses los puertos delanteros o laterales del gabinete de la PC ya que suelen ser de pobre calidad y suelen fallar mucho, tampoco uses concentradores o Hub.

* Rezar dos Padres Nuestros y tres Ave Maria. es broma, pero de seguro querrás tener a Dios de tu lado en este momento.

**Requerimientos:**

- Descargar <a title="Odin 4.03 Spica OPS" href="http://www.jam.net.ve/capt/Odin_4.03_Spica_ops.zip" target="_blank">Odin 4.03 </a>

- <a href="http://forum.samdroid.net/f53/cyanogenmod-6-1-1-spica-alpha8-4-a-4716/" target="_blank">Descargar CyanogenMod-6.1.1-Spica-alpha8.4</a>

- <a href="http://files.samdroid.net/files/2forum/i5700_LK2-08_PDA.7z" target="_blank">Descargar</a> el kernel de Leshak para <strong><a href="http://forum.samdroid.net/f55/lk2-08-original-firmwares-root-new-superuser-wifi-tether-bb-12-07-2010-a-1193/" target="_blank">Firmware Original</a></strong>.

**OJO** claramente dice Firmware original, Android 2.1 de agencia o actualizado mediante Kies Mini como en mi caso, si este no es tu situacion, **NO HAGAS NADA!!!** ya que podrías tener un kernel distinto que podría **no ser compatible** con los que aquí se usan.

- Necesitas tener instalados los drivers necesarios para conectar el teléfono a la PC, si en tu caso ya tienes instalado Samsung NPS (New PC Studio) o el Kies Mini, entonces ya tienes los drivers instalados, pero cabe aclarar un detalle debes desactivar el inicio automatico de Kies o NPS, puedes hacerlo mediante el Ccleaner. sino  lo que puedes hacer es entrar en la carpeta donde esta instalado NPS y/o Kies, debe haber por alli algun ejecutable llamado SAMSUNG_USB_Driver_for_Mobile_Phones.exe de unos 18.6Mb (Version 1.3.850) respaldalo en alguna otra ubicación, des instala el Kies y/o el NPS, limpia registros y demas con Ccleaner, reinicia la PC, luego instala los drivers que respaldaste y vuelve a reiniciar.  si no quieres hacer todo esto puedes descargar los drivers desde <a href="http://files.samdroid.net/files/drivers/SAMSUNG_USB_Driver_for_Mobile_Phones.rar" target="_blank">aqui.</a>

- Desactivar el inicio automático de tu antivirus, esto es para evitar posibles problema con los drivers.

**Procedimientos:**

Una vez que tengas instalado los drivers, ayas descargado Odin, la Room de Froyo para tu Spica, descargado el kernel de leshak **i5700_LK2-08_PDA.7z** y hayas configurado y reiniciado la PC para que NPS, Kies y tu antivirus no se inicien, entonces toca flashear para obtener root y recovery.

0- Descomprime el <strong>Odin_4.03_Spica_ops.zip</strong>, obtendrás una carpeta con el Odin y dos archivos.

1- Descomprime el kernel de leshak <strong>i5700_LK2-08_PDA.7z</strong>, deberías obtener <strong>i5700_LK2-08_PDA.tar</strong> (<strong><span style="color: #ff0000;">OJO no lo descomprimas nuevamente, déjalo así</span></strong>) de unos 15.2Mb y copíalo dentro de la carpeta donde tienes el Odin

2- Copia la room <strong>CM-6.1.1-Spica-a8.4_update.zip</strong> en la raíz de la tarjeta MicroSD, luego apaga tu teléfono, <strong>retira la tarjeta SIM y la MicroSD</strong>, luego colocalo en <strong>modo Download</strong>, presionando las teclas <strong>Volumen abajo + Camara + End o Apagar</strong> .

3- Abre el Odin (<strong>si estas en Windows Vista/Windows 7 abrelo como Administrador</strong>) Conecta el teléfono a la PC, espera un ratico que Windows reconozca el dispositivo. El Odin deberia reconocerlo marcando en la casilla de Messages Added!!! y Detected!!!, ademas deberia aparecer con fondo amarillo la casilla COM Port Mapping y un numero de puerto COM.

4-  En el Odin presiona el boton Reset Files, presiona el boton <strong>OPS</strong> y agrega el archivo <strong>spica_jc3.ops</strong>, luego presiona el boton <strong>PDA</strong> y agrega el archivo <strong>i5700_LK2-08_PDA.tar</strong>

5- Verifica que todo se vea similar a esto:

<a href="http://imgur.com/uVOwV"><img src="http://i.imgur.com/uVOwV.png" title="Hosted by imgur.com" alt="" /></a>

6- Si todo esta bien, entonces le damos al boton Start, Odin debería comenzar a Flashear el nuevo kernel en tu teléfono, el proceso no debería tardar mas que unos pocos segundos ya que el archivo es bastante pequeño.  El teléfono se reiniciara y entrara en el Recovery, (no es necesario, pero por seguridad espera al menos unos dos minutos y verifica que en el teléfono siga mostrándote el recovery) una vez dentro del recovery puedes desconectar el teléfono de la PC y Listo!!! ya tienes tu teléfono Rooteado y con Recovery :D

7- Apaga el Teléfono, quita la batería, coloca la tarjeta MicroSD (solo la MicroSD no coloques la tarjeta SIM) que en la cual copiaste la Room, coloca nuevamente la batería y entra ahora en el modo Recovery tecleando <strong>Volumen Abajo + Tecla de llamada + Tecla de terminar llamada/Apagar</strong>. Dejalo unos segundos presionado hasta que veas el menu del Recovery.

<a href="http://imgur.com/0Eqgy"><img src="http://i.imgur.com/0Eqgy.png" title="Hosted by imgur.com" alt="" /></a>

8- Este es el famoso Recovery :D se maneja usando los botones del teléfono y las confirmaciones que nos pide la hacemos seleccionando el boton de Home (no se usa tocando la pantalla). lo recomendable en este punto seria hacer un respaldo (por si las moscas) para eso ve a la opción "<strong>Samdroid 0.2.1 Backup</strong>" y de una vez comenzara a realizarse el respaldo el cual tarda unos minutos o unas 5 o 6 lineas. este respaldo luego en caso de inconvenientes podemos flashearlo mediante el Odin.

9- Ahora ve a la opcion "<strong>Wipe, Choose what</strong>" y luego aplica los 3 wipe que aparecen los cuales son "<strong>wipe data/cache</strong>", "<strong>wipe cache</strong>" y "<strong>Wipe Dalvik cache</strong>" tal como dice el recovery necesitas confirmar la opción a aplicar, presionando el botón Home (el botón de la casita)

<a href="http://imgur.com/8lqPE"><img src="http://i.imgur.com/8lqPE.png" title="Hosted by imgur.com" alt="" /></a>

10- Luego de esto vuelve al menú principal del Recovery y selecciona la opcion "Apply any zip from SD" y elegimos el archivo <strong>CM-6.1.1-Spica-a8.4_update.zip</strong> que copiamos anteriormente en la MicroSD. confirmamos la opción presionando Home, ahora se comenzara a instalar la nueva room, podrás ver el estado del proceso en la pantalla con todo lo que se esta realizando, también veras en el fondo una barra amarilla cargándose. Es posible que el teléfono se reinicie incluso unas 5 veces,  no te preocupes, pues esto es normal. Espera hasta que en la pantalla te diga algo como "<strong>Install from sd complete</strong>" y vuelva al recovery.  en este punto ya debe de haberse instalado tu nueva version de Android 2.2.1 Froyo :D tan solo reinicia el telefono en la opcion "<strong>Reboot system now</strong>" y ahora tu Spica se iniciara por primera vez con Froyo :D. no te preocupes si el primer inicio demora mas de lo normal, esto es normal. En mi caso demoro creo que como 5min aunque con el miedo y las bolas en las gargantas me parecieron como 15min LOOL

11- Una vez que tu Spica cargue Froyo por primera vez, veras que aparecerá el menú de configuración inicial. pero si hiciste los pasos tal cual aparecen aquí es probable que no tengas puesta la tarjeta <strong>SIM</strong>, por lo que debes preferiblemente cambiar el idioma a tu preferido, omitir toda la configuración inicial y apagar el teléfono. luego saca la batería, coloca la tarjeta <strong>SIM</strong>, vuelve a colocar la batería y enciende el teléfono nuevamente. Ahora si podras completar la configuración inicial y comenzar a disfrutar de Android 2.2.1 Froyo con multitouch, drivers 3D y rooteado desde el inicio :D

<a href="http://imgur.com/eau2R"><img src="http://i.imgur.com/eau2R.png" title="Hosted by imgur.com" alt="" /></a>

**Posibles problemas:**

Por suerte yo no tuve problemas graves, pero si tuve uno que me comió por varias semanas. Resulta que cuando conectaba el teléfono a la PC, el Odin me lo reconocía sin problemas, marcaba su puerto COM con fondo azul y todo lo demás como la imagen arriba. pero al hacer click en Start el Odin se quedaba sin hacer nada mas que mostrarme el mensaje "<strong>&lt;1&gt;</strong> <strong>setup connection...</strong>" en la casilla de mensajes.

Luego de unas cuantas semanas investigando, probando sugerencias que me fueron recomendadas en varios foros, etc. recibí por Twitter una recomendación por parte de <a href="http://twitter.com/IIKndyII">IIKndyII </a> (Muuuuchas gracias!!!!!) que fue la que soluciono mi problema. Cuando se quede el Odin en "<strong>&lt;1&gt;</strong> <strong>setup connection...</strong>" proceda a cerrar el Odin, luego desconecte el teléfono de la PC, apáguelo (quitando la batería y colocándosela nuevamente) inicie nuevamente en modo download, abra el Odin, cargue los archivos necesarios y conecte nuevamente el teléfono, espere unos 2 minutos  (yo me puse a ver un video de como se flasheaba un kernel al Spica :D) y luego presione el boton Start.   Y tal cual como me dijo **IIKndyII**... seguro ahora si lo reconoce y Odin comienza a flashear :D

En caso de que Odin te tenga rabia y te siga mostrando el mensaje, reintenta esta recomendación o reinicia la PC y vuelve a intentar.

**Primeras impresiones:**

Esta actualización yo la realice el Lunes de esta semana, por lo que no tengo ni una semana con la room, pero las primeras impresiones han sido muy favorables con respecto a Eclair actualizado desde Kies (oficial). lo mas destacable es que con esta room  la batería me esta durando muuuuchisimo mas que con Eclair. y como muestra les comento que la ultima vez que cargue el teléfono fue el martes en la noche, y hasta el dia de hoy sábado todavía no lo e puesto a cargar, si! lleva casi 4 dias sin cargarse!!! y todavía la bateria esta al 60%.  claro esta tengo las conexiones 2G/3G desactivadas y solo estoy usando la conexión WiFi de mi casa. no he usado mucho el teléfono, tan solo he hecho unas 4 llamadas de menos de 1min C/U, actualice unas 3 aplicaciones desde el market (este mismo se actualizo a la version 3.1.5) e instale unas 4 aplicaciones. use unos 5min el GPS con la aplicación Navitel + los mapas de mi área y todavía tengo batería!!!! :P
