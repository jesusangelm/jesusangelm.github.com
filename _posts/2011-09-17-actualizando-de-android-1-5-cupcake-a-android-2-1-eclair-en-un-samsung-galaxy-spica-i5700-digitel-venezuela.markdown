---
layout: post
title: !binary |-
  QWN0dWFsaXphbmRvIGRlIEFuZHJvaWQgMS41IEN1cGNha2UgYSBBbmRyb2lk
  IDIuMSBFY2xhaXIgZW4gdW4gU2Ftc3VuZyBHYWxheHkgU3BpY2EgaTU3MDAg
  RGlnaXRlbA==
tags:
- !binary |-
  ZGlnaXRlbA==
- !binary |-
  aW50ZXJuZXQ=
- !binary |-
  YW5kcm9pZA==
- !binary |-
  YWN0dWFsaXphcg==
- !binary |-
  Z2FsYXh5
- !binary |-
  c3BpY2E=
- !binary |-
  aTU3MDA=
- !binary |-
  Y3VwY2FrZQ==
- !binary |-
  ZWNsYWly
- !binary |-
  a2llcw==
---
{% include JB/setup %}

Hace poco mas de una semana adquirí un teléfono con S.O Android, específicamente el Samsung Galaxy Spica I5700 de Digitel, luego de jurungarlo por unas cuantas horas viendo y probando todas sus funciones me encontré con que no podía instalar muchas de las mejores aplicaciones disponibles para Android por el simple hecho de que el teléfono viene con Android 1.5 Cupcake, el cual es ya una versión desactualizada, por lo que para exprimir mejor las funciones del equipo debería actualizar como mínimo a Android 2.1 Eclair o superiores.



Buscando en internet encontré mucha información para actualizar el Galaxy Spica i5700  a Eclair o incluso ir mas allá y actualizar a Froyo o Gingerbread, pero muchas de ellas se realizan con métodos un tanto extraños (Flasheando con Odin y/o aplicar roms con Recovery) a simple  vista para alguien como yo que apenas tenia unas horas de experiencia en Android y teléfonos inteligentes, por lo que decidí dejarlas a un lado para estudiar mejor los procedimientos e intentarlo de forma segura en un futuro cercano.

Por suerte en la pagina de <a href="http://www.samsung.com/ve/">Samsung Venezuela </a> ofrecen una actualización a Eclair (no es Froyo ni Gingerbread pero al menos es algo.) con un método un tanto mas directo, con menos pasos y podría decirse que mas seguro ya 
que en la <a href="http://www.digitel.com.ve//Secciones/Persona_Detalle.aspx?level=18&Seccion=92&Menu=A5&Control=pla_equ_03.ascx&Equ_id=623">pagina de Digitel</a> dicen que hay una actualización disponible para este equipo en la pagina de Samsung (al menos lo incitan a uno a actualizar con ese método, si algo saliera mal ellos "deberían" poder responder sin rechistar.), por lo que decidí actualizar de esta forma:

* Lo unico malo de todo esto es que hay que usar Windows :(  pero bueh no queda de otra (por ahora)... en mi caso yo use Windows 7 64bits.

**Notas antes de comenzar, si no cumples con algunas de estas notas NO HAGAS NADA!!!:**

* Tu teléfono debe estar cargado al 100%. lo mismo va en caso de que estés desde una Laptop, y muy recomendable estar conectado a un UPS, no valla a ser que <strong>CortoElec</strong> le de por quitarte la luz en pleno proceso de actualización.

* En el teléfono ve a <strong>"Configuración"</strong> o <strong>"Ajustes"</strong>  luego <strong>"Aplicaciones"</strong>  luego <strong>"Desarrollo"</strong> y por ultimo asegurare de que <strong>"Depuración de USB"</strong> esta marcada.

* Has un respaldo de tus contactos, recomendable sincronizar los contactos con tu cuenta de Google/Gmail para que queden respaldados allí y luego puedas recuperarlos fácilmente.

* Recomendable: instalar la aplicación <a href="https://market.android.com/details?id=com.riteshsahu.APNBackupRestore&amp;feature=search_result">APN Backup &amp; Restore</a> para que respaldes tus APN la guardes en la memoria MicroSD o tu PC y las puedas restaurar luego.

* Estar conectado a internet con una conexión rápida y estable.  ya que Kies se descargara los archivos necesarios y son como 115Mb Aprox. yo me conecte desde un módem USB Movistar que es muy rápido en mi zona, pero sospecho que este fue la causa de  un error que explicare mas adelante, si cuentas con un internet Wifi o cableado de alta velocidad usalo en vez del módem para estar mas seguro.

* Si harás la actualización en una PC de escritorio conecta el cable USB del teléfono a un conector USB que sea directo a la Tarjeta Madre de la PC. no uses los puertos delanteros o laterales del gabinete de la PC ya que suelen ser de pobre calidad y suelen fallar mucho, tampoco uses concentradores o Hub.

* Rezar dos Padres Nuestros y tres Ave Maria.  :P es broma, pero de seguro querrás tener a Dios de tu lado en este momento :D

**Procedimiento:**

- Primero que todo debemos descargar la aplicación  <a href="http://org.downloadcenter.samsung.com/downloadfile/ContentsFile.aspx?CDSite=UNI_VE&amp;CttFileID=4050765&amp;CDCttType=SW&amp;ModelType=N&amp;ModelName=GT-I5700L&amp;VPath=SW/201107/20110727165853433/Kiesmini_1.0.0.11074_2.exe">Kies Mini</a> desde la pagina de Samsung Venezuela.

- la instalamos, en la ventana donde pregunta el país elige España e idioma Español ya que Venezuela no aparece por ningún lado :S

- Si por casualidad tienes instalado NPS (Samsung New PC Studio) cierralo por completo, que no haya procesos de el ejecutándose (verifica en la bandeja de sistema y en el administrador de tareas).

- Abre el Kies Mini, y en el menú elige "Instalar controladores" para que se instalen los drivers y reinicia la PC.

**Nota:** a pesar de que en alguno otros tutoriales de flasheo con Odin y similares recomiendan quitar la MicroSD y la SIM, en este método no es necesario. en mi caso yo no se lo quite.

- Abre nuevamente el Kies, conecta el teléfono a la PC y espera que lo reconozca, al cabo de unos segundos debería marcarte que hay una actualización. una vez te diga que existe una, comienza el proceso de actualización.

* El proceso comienza descargando los archivos necesarios (Roms y demás)  de internet, por lo que el tiempo depende de que tan rápida y estable sea tu conexión. (en mi caso demoro como 10min).

**Nota:** en caso de que estando en el proceso de descargas estés se cancele y te muestre error, desconecta el teléfono apagalo quita la pila, colocala nuevamente y enciendelo, cierra el Kies, abrelo nuevamente , conecta el teléfono e intenta de nuevo. en mi caso completo la descarga al tercer intento. :S

* una vez termine la descarga el teléfono se reiniciara para entrar en "modo download" (pantalla negra con logo y letras de fondo azul) y el Kies comenzara a copiar los archivos descargados al teléfono, veras el proceso de copiado en el teléfono mediante una barra azul que se va llenando.

* una vez terminado, el teléfono se reiniciara nuevamente y ahora mostrara una pantalla negra con un logo de una cajita con una barra abajo que se va llenando (en mi caso no se lleno mucho), supongo que en este paso se instalan y aplican los archivos descargados. En este paso es probable que el Kies te diga que ya ha sido completada la actualización, pero Espera!!! no le hagas caso que el teléfono sigue haciendo algo, mantenlo conectado a la PC.

* cuando termine la instalación, (no demora mucho) el teléfono se reiniciara, cargara Android 2.1 Eclair, entraras en tu escritorio (el del teléfono) y eso sera todo :D


**Posibles problemas:**

Bueno a pesar de que este método parece mas directo, corto y sencillo no es a prueba de errores.  en mi caso cuando termino la descarga de los archivos desde internet, y luego de que el teléfono se reiniciara para entrar en <strong>"Modo download"</strong>  Windows comenzó a instalar unos drivers para reconocer el dispositivos y para remate me pidió reiniciar (ni loco iba yo a reiniciar en pleno proceso de actualización), luego de instalado el drivers y detectado el dispositivo el modem USB se desconecto (eyecto) al igual que el teléfono (quedándose este con el logo de Samsung en la pantalla) y el Kies me mostró un mensaje en el que decía que la actualización no podo ser completada y sugiriendo hacer una recuperación de emergencia. :O  en ese momento tenia las bolas en la garganta!!!!.

En ese momento lo único que se me ocurrió fue terminar de desconectar el teléfono a la laptop, quitar la pila, volverla a colocar y encender el teléfono. Para mi alivio inicio normalmente y sin problemas a Android Cupcake  (si allí se bajaron las que te conté a su lugar LOOL ).  al cabo de un rato decidí volver a intentarlo, pero para mi sorpresa al  abrir el Kies este  me mostraba que había un intento de actualización que no se completo y me pedía que hiciera una <strong>"recuperación de emergencia"</strong>  y me paso a mostrar los pasos para realizarla los cuales son simplemente colocar el teléfono uno mismo en <strong>"modo Download"</strong> presionando las teclas Volumen abajo + Camara + End o Apagar estando apagado el teléfono y luego conectarlo a la PC y darle a "Recuperación de emergencia" en el Kies. Esto lo que hizo fue copiar al teléfono los archivos descargados, pero esta vez si los instalo y los aplico por lo que al cabo de unos segundos el teléfono se reinicio y entro a Android 2.1 Eclair :D
