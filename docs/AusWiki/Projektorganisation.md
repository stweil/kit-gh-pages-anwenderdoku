# Einleitung

Um ein Digitalisierungsprojekt in Kitodo.Production erfolgreich durchführen zu können, sind einige Vorüberlegungen, beziehungsweise Vorbereitungen notwendig. Je nach Institution unterscheiden sich diese. Trotzdem werden hier Beispiele und Hilfen bereitgestellt.  

# Allgemein
## DFG-Praxisregeln
Dieses Dokument enthält grundlegende Standards und Anforderungen an Digitalisierungsprojekte: 
* http://www.dfg.de/formulare/12_151/12_151_de.pdf 

## Checkliste 
Dieses Dokument wurde in der SLUB entwickelt, um den Workflow eines Projekts zu planen. Nicht alle Schritte müsen bei jedem Projekt beachtet werden: 
* [Beispiel Checkliste](images/Checkliste_leer-neu.xls)


# Kitodo.Production
## Projekt

Es muss entschieden werden, ob in Kitodo.Production ein neues Projekt angelegt werden soll. Dies ist unter anderem sinnvoll, beziehungsweise notwendig, wenn Nutzerbeschränkungen eingeführt werden sollen und wenn projektbezogene, statistische Auswertungen geplant sind. 

Es ist jedoch darauf zu achten, dass nicht zu viele Projekte angelegt werden, da dies den Verwaltungaufwand in Kitodo.Production erhöht. Hier muss beachtet werden, dass ein Projekt in der *[goobi_digitalCollections.xml](https://github.com/kitodo/kitodo-production/blob/1.11.x/Goobi/config/goobi_digitalCollections.xml)* eingetragen ist, da ansonsten keine digitalen Kollektionen vergeben werden können. 

Wenn projektspezifische Einstellungen vorgenommen werden, muss dies zusätzlich in der _[goobi_projects.xml](https://github.com/kitodo/kitodo-production/blob/1.11.x/Goobi/config/goobi_projects.xml)_ eingetragen werden. 

Projekte können zum Beispiel in Anlehnung von Drittmittelprojekten angelegt werden.

Angaben, die notwendig sind (Beispiel SLUB):

* Projektname 
* Zugelassene Benutzer 
* Fußleisteninhalt 
* Förderer
* OCR-fähig -> "FULLTEXT"-FileGroup muss angelegt werden

Hinweis:

In der Regel können die Feldinhalte aus bestehenden Projekten übernommen werden. 

# Produktionsvorlage

Wenn eine Produktionsvorlage erstellt wird, muss ein Projekt angegeben werden. Dieses Projekt wird allen Vorgängen zugeordnet, die mit dieser Vorlage angelegt werden. In der Produktionsvorlage müssen alle Aufgaben, die für das Projekt notwendig sind, benannt und in der korrekten Reihenfolge angelegt werden. Es ist darauf zu achten, dass keine unnötigen Arbeitsschritte eingefügt werden.

Angaben, die notwendig sind:

* Titel der [Produktionsvorlage](Produktionsvorlage)
* [Aufgaben](Aufgaben) und deren Reihenfolge 
* [Projekt](Projekt)
* [Regelsatz](Regelsatz)
* [Laufzettel](Laufzettel)


# Digitale Kollektion

Bevor ein neues Projekt erstellt wird, müssen die [Digitalen Kollektionen](Digitale-Kollektionen) benannt und gegebenenfalls erstellt werden, die den Vorgängen des Projekts zugewiesen werden sollen. Wenn eine neue Digitale Kollektion angelegt wird, sind auch Einstellungen außerhalb von Kitodo.Production notwendig, weshalb hier je nach Einrichtung die IT-Administratoren tätig werden müssen.

Angaben, die notwendig sind:

* Titel der Kollektion
* Die Kollektion muss in der Datei *[goobi_digitalCollections.xml](https://github.com/kitodo/kitodo-production/blob/1.11.x/Goobi/config/goobi_digitalCollections.xml)* eingetragen werden 
* Wenn Kollektionen projektabhängig vergeben werden, muss auch noch definiert werden, welche Kollektion in welchem Projekt angezeigt werden soll.


# Benutzer

Selbstverständlich müssen alle notwendigen [Benutzer](Benutzer) für das Projekt zugelassen werden. Hier müssen auch die [Berechtigungsstufen](Berechtigungsstufen) beachtet werden, die angeben, welcher Benutzer bestimmte Aufgaben übernehmen darf.