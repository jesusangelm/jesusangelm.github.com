---
layout: post
title: !binary |-
  RXhwb3J0YXIgdHVzIGNvbnRyYXNlw7FhcyBkZSBMYXN0UGFzcyBhIEtlZVBh
  c3NYIC0gQWN0dWFsaXphZG8=
tags:
- !binary |-
  bmF2ZWdhZG9y
- !binary |-
  cGx1Z2lucw==
- !binary |-
  bWJy
- !binary |-
  ZGVzY2FyZ2Fy
- !binary |-
  ZXNjcml0b3Jpbw==
- !binary |-
  YmFzaA==
- !binary |-
  c2NyaXB0
- !binary |-
  c2VndXJpZGFk
- !binary |-
  Y29udHJhc2XDsWE=
- !binary |-
  aW1wb3J0YXI=
- !binary |-
  ZXhwb3J0YXI=
- !binary |-
  bGFzdHBhc3M=
- !binary |-
  a2VlcGFzc3g=
- !binary |-
  dGVybWluYWw=
---
Para los que no conocen <a href="http://lastpass.com/">LastPass </a>es un servicio online gratuito que nos permite guardar las contraseñas de todas las paginas a las cuales estamos registrados y nos facilita la tarea de loguearnos/registrarnos en dichas paginas autorellenando los formularios. Y para los que no conoscan <a href="http://www.keepassx.org/">KeePassX</a> es una aplicacion con caracteristicas similares a LastPass solo que este se ejecuta como aplicacion de escritorio y guarda las contraseñas en tu PC.
<p style="text-align: center;"><strong>De</strong></p>
<p style="text-align: center;"><a href="http://blog.jam.net.ve/imagenes/uploads/2010/09/logo_lastpass.png"><img class="aligncenter size-full wp-image-400" title="logo_lastpass" src="http://blog.jam.net.ve/imagenes/uploads/2010/09/logo_lastpass.png" alt="" width="164" height="20" /></a><strong>A</strong></p>
<a href="http://blog.jam.net.ve/imagenes/uploads/2010/09/kp_logo_main.png"><img class="aligncenter size-full wp-image-401" title="kp_logo_main" src="http://blog.jam.net.ve/imagenes/uploads/2010/09/kp_logo_main.png" alt="" width="170" height="170" /></a>

Para muchos paranoicos no les agrada mucho la idea de usar LastPast ya que este al ser un servicio gratuito y online esta propenso a ataques o a que los mismos creadores escudriñen en nuestras contraseñas (a fin de cuentas ellos son los que tienen acceso a esos datos). Por lo que si tu ya tienes unas cuantas contraseñas almacenadas en LastPass y deseas almacenarlas en tu PC podemos valernos del Script <span style="text-decoration: line-through;"><a href="http://github.com/nazariuskappertaal/lastpass2keepass">LastPass2KeePass</a></span> que nos permite importarlas en .XML y Exportarlas en KeePassX para administrarlas desde este ultimo y no desde LastPass.

- <span style="text-decoration: line-through;">Para hacer esto tan solo debemos descargarnos el Script haciendo click  <a href="http://github.com/nazariuskappertaal/lastpass2keepass/raw/master/lastpass2keepass.py">Aqui</a>.</span>

<span style="text-decoration: line-through;">
</span>

<strong>Nota: articulo Actualizado el 22-02-2011, Salte al final para saber mas y luego continué a partir de aquí.</strong>

- Una vez descargado/guardado el script le damos permiso de ejecucion tecleando en la terminal:

[bash] sudo chmod +x lastpass2keepass.py [/bash]

- Ahora solo necesitamos exportar las contraseñas almacenadas en LastPast en un archivo, Si por ejemplo usas el Plugins de LastPast en tu navegador basta con hacer click en el icono &gt; Herramientas &gt; Exportar a &gt; Archivo CVS LastPass. Le colocas un nombre al archivo y lo guardas en la misma carpeta donde tengas el script <a href="http://github.com/nazariuskappertaal/lastpass2keepass">LastPass2KeePass.</a>

- Ahora nos vamos a la terminal y ejecutamos el script de importacion tecleando en la terminal:

[bash] sudo python lastpass2keepass.py contraseñasLastPass contraseñaskeepass.xml [/bash]

Donde:

* contraseñasLastPass : Es el nombre del archivo donde estan las contraseñas exportadas desde LastPass.

* contraseñaskeepass.xml :  Es el nombre que quieres que tenga el archivo con tus contraseñas convertidas a formato XML de KeePassX.

- Ahora tan solo debemos Importar las contraseñas en KeePassX, para esto solo abrimos la aplicacion y nos vamos a Fichero &gt; Importar desde... &gt; KeePassX XML (*.xml)  Y elegimos nuestro archivo exportado que en nuestro caso se llama contraseñaskeepass.xml

Ya con esto tendras tus contraseñas de LastPass almacenadas en KeePassX y desde ahora podras administrarla desde este ultimo teniendo la seguridad de que solo tu eres el que las puedes ver y tocar :-)

<strong>Actualizacion: 22-02-2011:</strong>

El repositorio en Github donde se encontraba la aplicacion lastpass2keepass.py ya no esta disponible a la fecha, por tal motivo copio a continuacion el codigo que compone la aplicacion:

[python]# lastpass2keepass
# Supports:
# Keepass XML - keepassxml
# USAGE: python lastpass2keepass.py exportedTextFile
# The LastPass Export format;
# url,username,password,1extra,name,grouping(\ delimited),last_touch,launch_count,fav

import sys, csv, time, datetime, itertools, re # Toolkit
import xml.etree.ElementTree as ET # Saves data, easier to type

# Strings

fileError = &quot;You either need more permissions or the file does not exist.&quot;
lineBreak = &quot;____________________________________________________________\n&quot;

def formattedPrint(string):
 print lineBreak
 print string
 print lineBreak

# Files
# Check for existence/read/write.

try:
 inputFile = sys.argv[1]
except:
 formattedPrint(&quot;USAGE: python lastpass2keepass.py exportedTextFile&quot;)
 sys.exit()

try:
 f = open(inputFile)
except IOError:
 formattedPrint(&quot;Cannot read file: '%s' Error: '%s'&quot; % (inputFile, fileError) )
 sys.exit()

# Create XML file.
outputFile = inputFile + &quot;.export.xml&quot;

try:
 open(outputFile, &quot;w&quot;).close() # Clean.
 w = open(outputFile, &quot;aw&quot;)
except IOError:
 formattedPrint(&quot;Cannot write to disk... exiting. Error: '%s'&quot; % (fileError) )
 sys.exit()

# Parser
# Create a csv dialect and extract the data to a reader object.
dialect = csv.Sniffer().sniff(f.read(1024))
f.seek(0)
reader = csv.reader(f, dialect)

# Create a list of the entries, allow us to manipulate it.
# Can't be done with reader object.

allEntries = []

for x in reader:
 allEntries.append(x)
allEntries.pop(0) # Remove LP format string.

f.close() # Close the read file.

# Keepass XML generator

# Add doctype to head, clear file.
w.write(&quot;&lt;!DOCTYPE KEEPASSX_DATABASE&gt;&quot;)

# Generate Creation date
# Form current time expression.
now = datetime.datetime.now()
formattedNow = now.strftime(&quot;%Y-%m-%dT%H:%M&quot;)

# Initialize tree
# build a tree structure
page = ET.Element('database')
doc = ET.ElementTree(page)

# Dictionary of failed entries
failed = {}

formattedPrint(&quot;DEBUG of '%s' file conversion to the KeePassXML format, outputing to the '%s' file.&quot; %(inputFile,outputFile))

# A dictionary, organising the categories.
resultant = {}

# Parses allEntries into a resultant.
for entry in allEntries:
 try:
 categories = re.split(r&quot;[/\\]&quot;,entry[5]) # Grab final category.
 for x in categories:
 resultant.setdefault(categories.pop(), []).append(entry) # Sort by categories.
 except:
 # Catch illformed entries
 # Grab entryElement position
 p = allEntries.index(entry) + 2
 failed[p] = [&quot;,&quot;.join(entry)]
 print &quot;Failed to format entryElement at line %s&quot; % (p)

# Initilize and loop through all entries
for category, categoryEntries in resultant.iteritems():

 # Create head of group elements
 headElement = ET.SubElement(page, &quot;group&quot;)
 ET.SubElement(headElement, &quot;title&quot;).text = str(category)
 ET.SubElement(headElement, &quot;icon&quot;).text = &quot;0&quot; # Lastpass does not retain icons.

 for entry in categoryEntries:
 # entryElement information
 try:
 # Each entryElement
 entryElement = ET.SubElement(headElement, &quot;entry&quot;)
 # entryElement tree
 ET.SubElement(entryElement, 'title').text = str(entry[4])
 ET.SubElement(entryElement, 'username').text = str(entry[1])
 ET.SubElement(entryElement, 'password').text = str(entry[2])
 ET.SubElement(entryElement, 'url').text = str(entry[0])
 ET.SubElement(entryElement, 'comment').text = str(entry[3])
 ET.SubElement(entryElement, 'icon').text = &quot;0&quot;
 ET.SubElement(entryElement, 'creation').text = formattedNow
 ET.SubElement(entryElement, 'lastaccess').text = str(entry[6])
 ET.SubElement(entryElement, 'lastmod').text = str(entry[7])
 ET.SubElement(entryElement, 'expire').text = &quot;Never&quot;
 except:
 # Catch illformed entries
 # Grab entry position
 p = allEntries.index(entry) + 2
 failed[p] = [&quot;,&quot;.join(entry)]
 print &quot;Failed to format entry at line %d&quot; %(p)

# Check if it was a clean conversion.
if len(failed) != 0:
 # Create a failed list.
 failedList = [&quot;%d : %s&quot; %(p, str(e[0]).decode(&quot;utf-8&quot;)) for p, e in failed.items()]
 formattedPrint(&quot;The conversion was not clean.&quot;)
 print &quot;You need to manually import the below entries from the '%s' file, as listed by below.&quot; %(inputFile)
 formattedPrint(&quot;Line Number : entryElement&quot;)
 for x in failedList:
 print x

# Write out tree
# wrap it in an ElementTree instance, and save as XML
doc.write(w)
w.close()

print lineBreak
print &quot;\n'%s' has been succesfully converted to the KeePassXML format.&quot; %(inputFile)
print &quot;Converted data can be found in the '%s' file.\n&quot; %(outputFile)
print lineBreak[/python]

Guardelo con el nombre <strong>lastpass2keepass.py</strong> y continué con el articulo debajo de la nota.

Existen dos fork en Github, el de <a href="https://github.com/haridsv/lastpass2keepass">harisdsv</a> y el de <a href="https://github.com/anirudhjoshi/lastpass2keepass">anirudhjoshi</a>, pero en las pruebas que realice, estos no me funcionaron a la perfección.

Saludos y Espero les sirva...
