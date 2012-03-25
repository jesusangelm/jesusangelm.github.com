---
layout: post
title: !binary |-
  SW5zdGFsYXIgVWJ1bnR1IDguMDQvIGVuIHVuYSBNZW1vcmlhIFVTQg==
excerpt: !binary |-
  QWxnbyBxdWUgeWEgaGFiaWEgaGVjaG8gbXV4aGFzIHZlY2VzIGFudGVzIGRl
  IGluc3RhbGFyIGRlZmluaXRpdmFtZW50ZSBVYnVudHUgZW4gbWkgUEMgZnVl
  IGluc3RhbGFyIHVuYSBkaXN0cm8gTGludXggZW4gYWxndW5hcyBkZSBtaXMg
  bWVtb3JpYXMgVVNCLiAgRW4gZXN0ZSBwb3N0IGxlcyBmYWNpbGl0byB1bmEg
  dHJhZHVjY2lvbiBzZW5jaWxsYSBkZSBsYSB3ZWIgUGVuRHJpdmVMaW51eCBl
  biBsYSBxdWUgc2UgZXhwbGljYSBsb3MgcGFzb3MgcGFyYSBpbnN0YWxhciBV
  YnVudHUgOC4wNCBlbiB1biBQZW5Ecml2ZSBwb3IgbWVkaW8gZGUgbGEgY29u
  c29sYSB5L28gdGVybWluYWwu
tags:
- !binary |-
  aW5zdGFsYWNpb24=
- !binary |-
  bGludXg=
- !binary |-
  dHV0b3JpYWw=
- !binary |-
  dWJ1bnR1
- !binary |-
  dXNi
- !binary |-
  d2luZG93cw==
- !binary |-
  bWJy
- !binary |-
  c2lzdGVtYQ==
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  aW5zdGFsYXI=
- !binary |-
  YmFy
- !binary |-
  d2Vi
- !binary |-
  a3VidW50dQ==
- !binary |-
  dGVybWluYWw=
- !binary |-
  c2lzdGVtYXM=
---
Algo que ya habia hecho muxhas veces antes de instalar definitivamente Ubuntu en mi PC fue instalar una distro Linux en algunas de mis memorias USB.  En este post les facilito una traduccion sencilla de la web <a title="Pendrive Linux" href="http://www.pendrivelinux.com" target="_blank">PenDriveLinux</a> en la que se explica los pasos para instalar Ubuntu 8.04 en un PenDrive por medio de la consola y/o terminal.

1. Descargar Ubuntu 8.04 y grabarlo a un cd.
2. Reiniciar el PC desde el livecd
3. Insertar la memoria/disco USB
4. Abrir una ventana de terminal y escribir: sudo su
5. Ahora escribimos fdisk -l para ver una lista de los diferentes discos/particiones (tomar nota sobre cuál dispositivo es tu memoria/disco USB Ejemplo: /dev/sdb). A lo largo de éste tutorial debes reemplazar todas las x con la letra de tu dispositivo USB. Por ejemplo, si tu dispositivo es sdb, entonces reemplaza la x con una b.
6. Escribe umount /dev/sdx1
7. Escribe fdisk /dev/sdx
* Escribe p para que te muestre las particiones (debe haber al menos una en tu memoria/disco USB) y luego escribe d para borrarlas.
* Escribe p de nuevo para que te muestre las particiones restantes (si existen debes repetir el paso anterior)
* Tipea n para crear una nueva partición
* Tipea p para que sea una partición primaria
o Selecciona 1 para que sea la primera partición
o Presiona enter para usar el primer cilindro (inicio del disco)
o Escribe +750M para establecer el tamaño de la partición
o Tipea a para marcar la partición como activa
o Escribe 1 para seleccionar la primera partición
o Escribe t para cambiar el tipo de ficheros
o Escribe 6 para seleccionar Fat16
* Escribe n para hacer otra partición
* Tipea n para crear una nueva partición
* Tipea p para que sea una partición primaria
o Selecciona 2 para que sea la segunda partición
o Presiona enter para usar el primer cilindro (inicio del disco)
o Presiona enter para usar el espacio restante (en caso que sea sólo de 1Gb, si no es así escribe +200M) si tu pendrive es de 1Gb pasa al paso siguiente, si no repite el anterior sin establecer tamaño para que use el espacio restante
* Tipea w para escribir la nueva tabla de particiones
8. Escribe umount /dev/sdx1 para desmontar la partición
9. Escribe mkfs.vfat -F 32 -n ubuntu8 /dev/sdx1 para darle formato a la primera partición
10. Escribe umount /dev/sdx2 para asegurarte que la segunda partición no esta montada
11. Escribe mkfs.ext2 -b 4096 -L casper-rw /dev/sdx2 para darle formato a la segunda partición
12. Si create una tercer particion y deseas poder usar con windows, escribe umount /dev/sdx3 para desmontar la partición y luego escribe mkfs.vfat -F 32 -n ELNOMBREQUEQUIERAS /dev/sdx3 para darle formato a esta partición
13. Desconecta y conecta de nuevo el dispositivo.
14. Regresa a la terminal y escribe sudo apt-get install syslinux mtools
15. Luego escribes syslinux -sf /dev/sdx1
16. Presiona CTRL+D para salir del sudo
17. Escribe cd /cdrom
18. Ahora vas a escribir cp -rfv casper disctree dists install pics pool preseed .disk isolinux/* md5sum.txt README.diskdefines ubuntu.ico casper/vmlinuz /media/ubuntu8/
19. Tipea cd /media/ubuntu8
20. Escribe wget pendrivelinux.com/downloads/u8/syslinux.cfg
21. Escribe cd casper
22. Escribe rm initrd.gz
23. Escribe wget pendrivelinux.com/downloads/u8/initrd.gz
24. Reinicia tu PC y configura tu BIOS para que arranque desde la Memoria USB.

Si todo a ido bien ahora deberia de estar arrancando Ubuntu en tu PC. :-)

Si eres usuario de Ubuntu 8.10 este proceso es mucho mas facil ya que desde esta version de ubuntu se a incorporado una aplicacion que hace todo esto de manera sencilla, tan solo debes colocar tu Pendrive en la PC, luego montar el Cd de Ubuntu o tener el archivo .ISO de Ubuntu en la PC y dirigirte a<strong> Sistemas/Administracion /Create a USB Startup Disk</strong> .  Si no cuentas con Ubuntu Instalado puedes arrancar el Live Cd de Ubuntu 8.10 e instalarlo en tu PC con este asistente.

<strong>Nota:</strong> Esta instalacion solo crea una instalacion del tipo "Live" es decir solo funcionara al igual que in "Live Cd" comun o en este caso un "Live USB" y no guardara los cambios realizados durante la sesion al apagar la PC..  El metodo por la Consola y por el asistente puede funcionar tambien con Kubuntu y otras distros
