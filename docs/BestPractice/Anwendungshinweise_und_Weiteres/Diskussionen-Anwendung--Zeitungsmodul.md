# Erkenntnisaustausch rund um die Anwendung des Zeitungsmoduls

##Grundlegende Informationen 
In diesem Wiki sind folgende Informationen zum Zeitungsmodul vorhanden: 

_Anlegen von Vorgängen mit dem Zeitungsmodul auf Ausgabenebene_: 

Neuen-Vorgang-anlegen-I-Zeitungen 

_Zeutschel-Dokumentation des Zeitungsmoduls_: 

http://www.goobi.org/fileadmin/groups/goobi/pdf/TS-1090_TechnInfo_Zeitungsdigital.pdf

##Granularität
Es muss entschieden werden, in welcher Granularität die Zeitungen in Kitodo.Production bearbeitet werden sollen. 
###Ausgaben-Granularität

Vorteile: 
* Flexibles Hinzufügen und Löschen von Ausgaben ohne Auswirkung auf andere Ausgaben 
* Keine Strukturierung in den Vorgängen notwendig, um Ausgaben auszuzeichnen 

Nachteile: 
* Sehr großer Aufwand, um die Images aufzuteilen und nach Kitodo.Production zu verschieben 
* Es muss vor dem Anlegen der Vorgänge bekannt sein, welche Ausgaben tatsächlich vorhanden sind (ansonsten sind „leere“ Vorgänge  vorhanden oder die Vorgänge müssen gelöscht werden)

###Tages-, Wochen-, Monats-, Quartals-,  Jahres-Granularität
Theoretisch müssen die Ausgaben in den Vorgängen strukturiert werden, wenn man die einzelnen Ausgaben identifizieren will. Es muss unbedingt sichergestellt werden, dass diese Strukturelemente auch von der jeweiligen Präsentation (Kalenderansicht) erkannt und verarbeitet werden können. 

## Beilagen 

Eine Frage, die vor dem Beginn der Digitalisierung geklärt sein sollte, ist der Umgang mit Beilagen. Diese können in den Vorlagen unterschiedlich  eingebunden sein: jeweils einzeln an der Ausgabe oder gebündelt am Ende eines Bandes. 

Folgende Fragen sollten beantwortet werden: 

* Erhalten Beilagen eine eigene Titelaufnahme und werden sie als eigenständige Publikation bearbeitet (eigene PURL, ...)? 
* Werden die Beilagen auf Ausgabenebene angelegt? 
* Werden die Beilagen zu den zugehörigen Zeitungs-Ausgaben hinzugefügt? 
* Wie wird mit Beilagen umgegangen, die am Ende eines Bandes eingebunden sind? 

Je nach Vorlage der Beilagen und deren geplante Bearbeitung treten umfangreiche zusätzliche Aufgaben auf. 


##Skizze des geplanten Ablaufs in der SBB
Vorbemerkung: der Ablauf bezieht sich auf Ausgaben-Granularität
* Anlegen eines (temporären) _Kitodo_-Vorgangs zwecks Scannen das vorliegenden Originals (z.B. gebundener Jahrgang)
* Scannen des physikalisch vorliegenden Originals
* Erfassung erster Metadaten mittels ``CreateMetadata`` (siehe unten)
 * es entstehen die Einträge in der _Kitodo_-Datenbank
 * es entstehen die _Kitodo_-XML-Metadaten im Filesystem
 * es entstehen die Verzeichnisse mit Images
* temporärer Vorgang kann (nach Prüfung, ggf. automatisch) gelöscht werden

###Programm CreateMetadata
In Java geschriebenes Programm zur Metadaten-Erfassung mit grafischer Unterstützung. Damit zügiges Arbeiten ermöglicht wird, werden Derivate der Master-Images abgelegt 
* Vorteile
 * die oben aufgeführten Nachteile der Ausgaben-Granularität treten nicht auf
 * intuitives, zügiges Arbeiten (1 Jahrgang mit knapp 1000 Images in 20 Minuten)
 * Unterstützung der Fehlererkennung
 * funktionell getestet (European Newspaper Project)
 * nur relativ geringe Anpassungen der vorhandenen Software nötig
 * jederzeit an veränderte Anforderungen anpassbar (Java-Kompetenz ist im Haus vorhanden)
* Nachteile
 * Vorverarbeitung (für Thumbnails) notwendig, könnte aber ggf. automatisiert werden
 * proprietäre Software

