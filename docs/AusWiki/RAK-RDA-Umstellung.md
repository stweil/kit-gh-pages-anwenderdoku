# RAK-RDA Umstellung (SLUB - SWB)
## Vorbemerkung 
Für die RDA-Umstellung muss in Kitodo.Production der Regelsatz angepasst werden, so dass weiterhin die Inhalte der benötigten Felder in den Verbünden in die dafür vorgesehenen Felder in Kitodo.Production, beziehungsweise nach MODS gemappt werden können. 

Dies ist einfach, wenn nur die Feldbezeichnungen geändert würden. Jedoch wurden zusätzlich Feldinhalte geändert, so dass nicht nur darauf geachtet werden muss, eine Feldnamenänderung zu übernehmen, sondern auch den korrekten Inhalt. 

Es lassen sich folgende Änderungen unterscheiden: 

1. Felder, die schon vorhanden sind, jedoch inhaltlich anders belegt werden
2. Felder, die entfallen, deren Inhalt jedoch in einem anderen Feld eingetragen werden
3. Felder, die neu hinzukommen 
4. Felder, die entfallen

Damit lassen sich zum Beispiel im SWB folgende Felder kategorisieren: 

- 1100 (011@) -> 1
- 3210 (022A) -> 1
- 3220 (025@) -> 4
- 4022 (032C) -> 4
- 4030 (033A) -> 1 
- 4060 (034D) -> 1 
- 4110 (036L/00) -> 2 
- 4119 (036L/09) -> 2
- 4120 (036M/00) -> 2
- 4256 (039I) -> 3
- 3001 (028B) -> 2

Im Folgenden werden die Felder beschrieben, die in der Mailing Liste diskutiert wurden. Dies soll einen schnellen Überblick über die Thematik ermöglichen. 

## Felder 1100, 4030, 4060
Diese Feldinhalte ändern sich, weil in RDA Reproduktionen formal mit dem Erscheinungsdatum und Erscheinungsvermerk der Reproduktion beschrieben werden. Bisher wurden die Daten der Vorlage genutzt.  

Nun muss ein Weg gefunden werden, wie die Daten der Vorlage genutzt werden können: 

- 1100: In Unterfeld $r wird das Erscheinungsjahr in Sortierform der Vorlage angegeben. Das Erscheinungsjahr in Vorlageform ist in 1100 nicht vorhanden.  
- 4060: Der Inhalt ändert sich durch die Angabe "1 Online-Ressource", jedoch wird in Klammern der Umfang der Vorlage angegeben. 
- 4030: Die Angaben der Vorlage sind nicht hinterlegt. Es werden nur die Daten des Produzenten der Reproduktion angeboten. 

Es ist offensichtlich, dass es hier grundlegende Änderungen der Feldinhalte gibt, die nur schwer in Kitodo.Production umgesetzt werden können. Zumindest, wenn man weiterhin mit den Metadaten der Vorlage arbeiten will. Es scheint jedoch breite Übereinstimmung zu herrschen, mit den Metadaten der Vorlage arbeiten zu wollen. 

Eine weitere Lösungsmöglichkeit ist das Feld SWB-4256 (039I). In der PICA+-Ansicht werden die Inhalte der Vorlage angeboten, auch wenn es verknüpft ist. Die Expansion in PICA 3 zeigt diese Daten jedoch nicht an. Ein Beispiel könnte so aussehen: 

`039I ƒaElektronische Reproduktion vonƒ9450162699ƒVTpiƒaEckardtƒdErnstƒE1889ƒ1Sachsens Fürsten-ZugƒDWurzenƒGTestƒF1889ƒH[4] Blatt, 100 Seiten, [2] Blatt`

Die Daten werden in folgenden Unterfeldern gespeichert:

|  |  RAK (Pica 3) | RDA (Pica+) | RDA (Pica+ Unterfeld) |
| ------------- | ------------- | ------------- | ------------- |
| Autor (Nachname)  |   | 039I  | **ƒa**
| Autor (Vorname)  |   | 039I  | **ƒd**
| Erscheinungsjahr (Sortierform)  | 1100  | 039I  | **ƒF**
| Titel  | 4000  | 039I  | **ƒ1**
| Verlagsort  | 4030  | 039I  | **ƒD**
| Verlagsname  | 4030  | 039I  | **ƒG**
| Umfangsangabe  | 4060  | 039I  | **ƒH**


Bisher werden diese Daten nicht über die Schnittstelle bereitgestellt und können somit nicht genutzt werden. Ob und wann diese Daten angeboten werden, wird noch entschieden. Die Vorrausetzungen in den Verbünden können sich jedoch unterscheiden. 


## Feld 3010 
In RDA werden die Felder 3001, 3030 und 3040 nicht mehr verwendet. Alle dort aufgeführten Personen werden in dem Feld 3010 eingetragen. 

Dies führt dazu, dass diese Personen nicht mehr durch den Feldnamen identifiziert werden können. Die Funktion lässt sich nur durch die Beziehungskennzeichnung ableiten. Diese kann beim Import jedoch nicht genutzt werden. 

Folgende Szenarien stehen zur Verfügung: 

1. 3000 wird importiert, 3010 wird nicht importiert 
`+: einfach im Regelsatz abbildbar` 
`-: viele Personenmetadaten werden nicht in die Metadaten aufgenommen, einschließlich weitere Verfasser` 
2. 3000 und 3010 werden importiert, für 3000 wird die Rolle Autor vergeben; für 3010 wird die Rolle sonstige Person vergeben (Korrektur nachträglich im Metadateneditor manuell möglich)
`+: relativ einfach im Regelsatz abbildbar`
`+: alle Personenmetadaten werden übernommen` 
`-: Rollen der Personen nur ungenau beschrieben, mit RDA auch die von Verfassern` 
`-: wenn die Rollen manuell nachträglich vergeben werden, entsteht ein größerer Aufwand`
3. 3000 und 3010 werden importiert, 3000 wird die Rolle Autor vergeben; 3010 wird die Rolle abhängig von der Beziehungskennzeichnung vergeben (wenn es technisch möglich ist!) 
`+: alle Feldinhalte aus 3000 und 3010 werden mit korrekter Rolle übernommen` 
`-: ungewiss, ob bedingter Import möglich ist` 
`-: wenn möglich, ist die Umsetzung im Regelsatz sehr umfangreich` 


Dies sind erste Überlegungen, die gerne verbessert und ergänzt werden dürfen. 

Im Zuge der RDA-Umstellung sollte unbedingt auch der generelle Wunsch nach einem verbessertem Personen- und Körperschaften-Metadaten-Import beachtet werden. Zum Beispiel: [New features for METS Editor](https://github.com/kitodo/kitodo-production/wiki/New-features-for-METS-Editor). 

## Felder 4110, 4119, 4120

Gesamttitel und ungezählte Schriftenreihen der Sekundärausgabe werden in RDA in den Feldern 4170, 4180 und 4190 angegeben. 

Es sollte geprüft werden werden, ob die Inhalte dieser Felder in Kitodo.Production verarbeitet werden sollen, wie die Inhalte der Felder der Vorlage. Da nur die Felder 4170 - 4174, beziehungsweise 4180 - 4184 zur Verfügung stehen, sollte überlegt werden, auf welche Angaben unter Umständen verzichtet werden kann. 

## Feld 3210 
Das Feld 3210 (022A) bleibt zwar erhalten. Jedoch werden die Inhalte in Unterfelder aufgeteilt. Je nachdem, welche Inhalte man benötigt, muss dies im Regelsatz berücksichtigt werden. 

Erste Versuche haben ergebn, dass die Inhalte mehrerer Unterfelder in PICA in ein Metadatumfeld in Kitodo.Production gemappt werden können. Problematisch sind wiederholbare Unterfelder wie im SWB zum Beispiel $m (Besetzungsangaben) oder $n (Zählung eines Musikwerks). Diese werden überschrieben, so dass letztendlich nur der letzte Wert übernommen wird. 

Auf der Seite [Zeutschel Dokumentation](https://github.com/kitodo/kitodo-production/wiki/Zeutschel-Dokumentation) finden Sie einen Link auf das Dokument [Goobi.Production 1.11 : Beauftragte Weiterentwicklungen](http://www.goobi.org/fileadmin/groups/goobi/dokumentation/TS-1105_Weiterentwicklungen-GOOBI-WLB.pdf). Dieses enthält mehrere Beschreibungen zum Import und Mappen von Datenfeldern. 


## Quellen 

Hier werden einige wichtige Informationsquellen aufgeführt. 

Titeldaten für RDA: 

- https://vitruv.uni-tuebingen.de/ilias3/goto_bsz1_file_565_download.html
- In diesem Dokument werden nur PICA3-Felder aufgeführt. Eine korrekte Aussage über PICA+-Felder ist nicht möglich.

Übersicht über Formatänderungen im SWB:

- https://vitruv.uni-tuebingen.de/ilias3/goto_bsz1_file_848_download.html
- In diesem Dokument werden nur PICA3-Felder aufgeführt. Eine korrekte Aussage über PICA+-Felder ist nicht möglich. 

Dokumentation des Formats der Pica-Verbunddatenbank des SWB (RDA - Ansicht): 

- http://swbtools.bsz-bw.de/cgi-bin/help.pl?cmd=index&regelwerk=RDA&verbund=SWB
- Felder ohne Änderungen sind hier teilweise noch nicht aufgeführt.

Dokumentation des Formats der Pica-Verbunddatenbank des SWB (RDA - Ansicht) - nach PICA+ sortiert: 

- http://swbtools.bsz-bw.de/cgi-bin/help.pl?cmd=pp_list&verbund=SWB&regelwerk=RDA
- Felder ohne Änderungen sind hier teilweise noch nicht aufgeführt.

Informationen zu Reproduktionen: 

- https://wiki.dnb.de/display/RDAINFO/Original+-+Reproduktionen
- Auf dieser Seite wird die Verlinkung zwischen Original und Reproduktion beschrieben.

Modul 5A.05 - Reproduktionen: 

- https://vitruv.uni-tuebingen.de/ilias3/goto_bsz1_file_1063_download.html
- In dieser Präsentation wird erläutert, wie Reproduktionen nach RDA katalogisiert werden.

