---
layout: post
title: !binary |-
  Q291Y2hEQiAxLjAuMiBMaWJlcmFkbw==
tags:
- !binary |-
  bGludXg=
- !binary |-
  dWJ1bnR1
- !binary |-
  bm9zcWw=
- !binary |-
  Y291Y2hkYg==
---
Esta noticia la coloco como un par de dias tarde... pero ¡bueh! como nadie lee esto ¡que mas da! ¿Verdad?.

<a href="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_011.jpeg"><img class="aligncenter size-full wp-image-523" title="Selección_011" src="http://blog.jam.net.ve/imagenes/uploads/2010/12/Selección_011.jpeg" alt="" width="192" height="167" /></a>

Hace unos dias fue liberada una nueva version de <a href="http://blog.jam.net.ve/tag/couchdb/">CouchDB</a>, especificamente CouchDB 1.0.2 la cual trae los siguientes cambios:

- Lectura y escritura significativamente mas altos contra los indices de archivos y vistas de las bases de datos.

- Test Suite funciona correctamente en navegadores Safari y Chrome (Ya me preguntaba yo porque Chromium se pegaba cuando ejecutaba el test suite de 1.0.1).

- Reparado las bases de datos perdian su funciones de validacion luego de una compactacion.

- Reparado los errores de tiempo de espera ocasionales que se mostraban luego de compactar con exito bases de datos grandes.

- Reparado los errores ocacionales que aparecian al escribir en una base de datos que habia sido recientemente compactada.

- Reparado los errores de tiempo de espera ocacionales que aparecian en sistemas lentos o con alta carga de IO (E/S).

- Permitido el registro de tipos nativos

- Actualizado la libreria ibrowse a la version 2.1.2 que repara numerosos problemas de replicacion.

- Se asegura que la replicacion respete la configuracion HTTP definido en el config.

- No se fuerza la actualizacion de vistas cuando se solicita: _desing/doc/_info.

Entre otras mejoras...

Para ver una lista completa de cambios y bajarte la ultima version ve la la seccion de <a href="http://couchdb.apache.org/downloads.html">Descargas</a> de CouchDB.
