---
layout: post
title: "Exportar tus contrasenas de lastpass a keepassx"
tags: [contrasenas, linux, seguridad]
---

Para los que no conocen [LastPass](http://lastpass.com) es un servicio online gratuito que nos permite guardar las
contraseñas de todas las paginas a las cuales estamos registrados y nos facilita la tarea de loguearnos o
registrarnos en dichas paginas autorellenando los formularios. Y para los que no conoscan [KeePassX](http://www.keepassx.org/)
es una aplicacion con caracteristicas similares a LastPass solo que este se ejecuta como aplicacion
de escritorio y guarda las contraseñas en tu PC.

<!-- more -->

Para muchos paranoicos no les agrada mucho la idea de usar LastPass ya que este al ser un servicio gratuito y online esta
propenso a ataques o a que los mismos creadores escudriñen en nuestras contraseñas (a fin de cuentas ellos son
los que tienen acceso a esos datos). Por lo que si tu ya tienes unas cuantas contraseñas almacenadas en
LastPass y deseas almacenarlas en tu PC podemos valernos del Script
[LastPass2KeePass](http://github.com/nazariuskappertaal/lastpass2keepass) que nos permite importarlas en .XML y
exportarlas en KeePassX para administrarlas desde este ultimo y no desde LastPass.

- Para hacer esto tan solo debemos descargarnos el Script haciendo click [Aqui](http://github.com/nazariuskappertaal/lastpass2keepass/raw/master/lastpass2keepass.py)

**Nota: articulo Actualizado el 22-02-2011, Salte al final para saber mas y luego continué a partir de aqui**

- Una vez descargado el script le damos permiso de ejecucion tecleando en la terminal:

{% highlight bash %}
sudo chmod +x lastpass2keepass.py
{% endhighlight %}

- Ahora solo necesitamos exportar las contraseñas almacenadas en LastPast en un archivo, si por ejemplo usas
el plugins de LastPass en tu navegador basta con hacer click en el icono Herramientas  Exportar a  Archivo CVS LastPass.
Le colocas un nombre al archivo y lo guardas en la misma carpeta donde tengas el script LastPass2KeePass

- Ahora nos vamos a la terminal y ejecutamos el script de importacion tecleando en la terminal:

{% highlight bash %}
sudo python lastpass2keepass.py contraseñasLastPass contraseñaskeepass.xml
{% endhighlight %}

Donde:

* contraseñasLastPass : Es el nombre del archivo donde estan las contraseñas exportadas desde LastPass.

* contraseñaskeepass.xml :  Es el nombre que quieres que tenga el archivo con tus contraseñas convertidas a formato XML de KeePassX.

- Ahora tan solo debemos Importar las contraseñas en KeePassX, para esto solo abrimos la aplicacion y nos vamos
a Fichero - Importar desde... - KeePassX XML (*.xml)  Y elegimos nuestro archivo exportado que en nuestro
caso se llama contraseñaskeepass.xml

Ya con esto tendras tus contraseñas de LastPass almacenadas en KeePassX y desde ahora podras administrarla
desde este ultimo teniendo la seguridad de que solo tu eres el que las puedes ver y tocar :-)

**Actualizacion: 22-02-2011:**

El repositorio en Github donde se encontraba la aplicacion lastpass2keepass.py ya no esta disponible a la fecha, por tal motivo copio a continuacion el codigo que compone la aplicacion:

{% highlight python %}
# lastpass2keepass
# Supports:
# Keepass XML - keepassxml
# USAGE: python lastpass2keepass.py exportedTextFile
# The LastPass Export format;
# url,username,password,1extra,name,grouping(\ delimited),last_touch,launch_count,fav

import sys, csv, time, datetime, itertools, re # Toolkit
import xml.etree.ElementTree as ET # Saves data, easier to type

# Strings

fileError = "You either need more permissions or the file does not exist.""
lineBreak = "____________________________________________________________\n"

def formattedPrint(string):
 print lineBreak
 print string
 print lineBreak

# Files
# Check for existence/read/write.

try:
 inputFile = sys.argv[1]
except:
 formattedPrint("USAGE: python lastpass2keepass.py exportedTextFile")
 sys.exit()

try:
 f = open(inputFile)
except IOError:
 formattedPrint("Cannot read file: '%s' Error: '%s'"" % (inputFile, fileError) )
 sys.exit()

# Create XML file.
outputFile = inputFile + ".export.xml:

try:
 open(outputFile, "w").close() # Clean.
 w = open(outputFile, "aw")
except IOError:
 formattedPrint("Cannot write to disk... exiting. Error: '%s'"% (fileError) )
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
w.write("<!DOCTYPE KEEPASSX_DATABASE>")

# Generate Creation date
# Form current time expression.
now = datetime.datetime.now()
formattedNow = now.strftime("%Y-%m-%dT%H:%M")

# Initialize tree
# build a tree structure
page = ET.Element('database')
doc = ET.ElementTree(page)

# Dictionary of failed entries
failed = {}

formattedPrint("DEBUG of '%s' file conversion to the KeePassXML format, outputing to the '%s' file."" %(inputFile,outputFile))

# A dictionary, organising the categories.
resultant = {}

# Parses allEntries into a resultant.
for entry in allEntries:
 try:
 categories = re.split(r"[/\\]",entry[5]) # Grab final category.
 for x in categories:
 resultant.setdefault(categories.pop(), []).append(entry) # Sort by categories.
 except:
 # Catch illformed entries
 # Grab entryElement position
 p = allEntries.index(entry) + 2
 failed[p] = [",".join(entry)]
 print "Failed to format entryElement at line %s" % (p)

# Initilize and loop through all entries
for category, categoryEntries in resultant.iteritems():

 # Create head of group elements
 headElement = ET.SubElement(page, "group")
 ET.SubElement(headElement, "title").text = str(category)
 ET.SubElement(headElement, "icon").text = "0" # Lastpass does not retain icons.

 for entry in categoryEntries:
 # entryElement information
 try:
 # Each entryElement
 entryElement = ET.SubElement(headElement, "entry")
 # entryElement tree
 ET.SubElement(entryElement, 'title').text = str(entry[4])
 ET.SubElement(entryElement, 'username').text = str(entry[1])
 ET.SubElement(entryElement, 'password').text = str(entry[2])
 ET.SubElement(entryElement, 'url').text = str(entry[0])
 ET.SubElement(entryElement, 'comment').text = str(entry[3])
 ET.SubElement(entryElement, 'icon').text = "0"
 ET.SubElement(entryElement, 'creation').text = formattedNow
 ET.SubElement(entryElement, 'lastaccess').text = str(entry[6])
 ET.SubElement(entryElement, 'lastmod').text = str(entry[7])
 ET.SubElement(entryElement, 'expire').text = "Never"
 except:
 # Catch illformed entries
 # Grab entry position
 p = allEntries.index(entry) + 2
 failed[p] = [",".join(entry)]
 print "Failed to format entry at line %d" %(p)

# Check if it was a clean conversion.
if len(failed) != 0:
 # Create a failed list.
 failedList = ["%d : %s" %(p, str(e[0]).decode("utf-8")) for p, e in failed.items()]
 formattedPrint("The conversion was not clean.")
 print "You need to manually import the below entries from the '%s' file, as listed by below." %(inputFile)
 formattedPrint("Line Number : entryElement")
 for x in failedList:
 print x

# Write out tree
# wrap it in an ElementTree instance, and save as XML
doc.write(w)
w.close()

print lineBreak
print "\n'%s' has been succesfully converted to the KeePassXML format." %(inputFile)
print "Converted data can be found in the '%s' file.\n" %(outputFile)
print lineBreak
{% endhighlight %}

Guardelo con el nombre **lastpass2keepass.py** y continue con el articulo debajo de la nota.

Existen dos fork en Github, el de [harisdsv](https://github.com/haridsv/lastpass2keepass) y el
de [anirudhjoshi](https://github.com/anirudhjoshi/lastpass2keepass), pero en las pruebas que
realice, estos no me funcionaron a la perfección.

Saludos y Espero les sirva...
