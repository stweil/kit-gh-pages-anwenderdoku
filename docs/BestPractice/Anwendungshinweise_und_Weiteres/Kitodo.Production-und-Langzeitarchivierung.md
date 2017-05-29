# Kitodo.Production und Langzeitarchivierung 
Kitodo.Production bietet keine Möglichkeit der Langzeitarchivierung (LZA). Dennoch stellt sich die Frage, wie die Digitalisate nach der erfolgreichen Bearbeitung in Kitodo.Production  archiviert werden können. Es gibt keine allgemeingültige Lösung, jedoch gibt es Entscheidungen, die getroffen werden müssen hinsichtlich folgender Fragen: 

- Welche Bilddaten werden archiviert? 
- Welche Metadaten werden archiviert? 
- Welche zusätzlichen Daten werden archiviert?  
- … 

Da es keine allgemeingültige Lösung gibt, können nur Lösungen beschrieben werden, die in einzelnen Institutionen angewendet werden.  

# SLUB
## Einleitung 
Die SLUB führt die [Content Preservation](http://www.slub-dresden.de/ueber-uns/slubarchiv/erhalt-der-interpretierbarkeit/) und nicht die [Bitstream Preservation](http://www.slub-dresden.de/ueber-uns/slubarchiv/erhalt-der-korrektheit/) durch. Dadurch bestehen hohe Qualitätsansprüche an die Dateien, weshalb nur so wenige Dateien wie nötig im LZA archiviert werden. Da die LZA auch Geld kostet, sollten nur die notwendigsten Dateien dort aufgenommen werden. Derivate, wie PDF-Dateien können ja bei Bedarf wieder hergestellt werden – unter Umständen sogar in einer besseren Qualität. 

Eine Übersicht an die Anforderung an TIFF-Dateien finden Sie unter: 
http://www.slub-dresden.de/ueber-uns/slubarchiv/technische-standards-fuer-die-ablieferung-von-digitalen-dokumenten/handreichung-tiff/

Die Informationen wurden dem Thread *[Goobi]  Meta.xml , Daten aus Goobi-Production und Langzeitarchivierung* der Goobi-Mailingliste entnommen. 

## Archiviertes Material 
Welche Daten werden archiviert? 

- TIFF-Masterdaten 
- METS/MODS-Datei des Vorgangs 
- METS/DC-Datei, die für Rosetta erstellt wird 

Welche zusätzlichen Daten werden archiviert? 

- Volltexte (ALTO-XML-Dateien), weil OCR geld- und zeitaufwändig ist, werden diese Dateien nicht wie Bildderivate behandelt 

Welche Informationen werden NICHT archiviert? 

- Alle Derivate der TIFF-Dateien (JPG, PDF, …), weil diese auf Basis der Masterdaten wieder erzeugt werden können und eine Aufbereitung aller Dateien nach den Ansprüchen der Content Preservation sehr aufwändig ist 
- Prozess-Metadaten zu den Vorgängen (Workflow, Bearbeitungsstand, etc.)  in Kitodo.Production 

## Workflow (Skizze) 
- Bearbeitung der der Digitalisate in Kitodo.Production 
- Wenn alle Arbeitsschritte erfolgreich abgeschlossen sind, werden die TIFF-Masterdaten, die METS/MODS-Dateien sowie die ALTO-Dateien an die LZA gegeben 
- Die Images werden in Kitodo.Production gelöscht und können bei Bedarf aus dem Langzeitarchiv wiederhergestellt werden 
- Nur wenn Korrekturen an den Images durchgeführt werden müssen, werden die Images wieder nach Kitodo.Production kopiert 
- Änderungen an Bild- und Metadaten-Dateien werden als neue Revision des Vorgangs angelegt 



