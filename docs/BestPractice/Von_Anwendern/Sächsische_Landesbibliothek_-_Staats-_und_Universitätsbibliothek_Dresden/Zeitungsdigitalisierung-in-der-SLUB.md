# Zeitungsdigitalisierung in der SLUB

Im Folgenden wird die Zeitungsdigitalisierung in der SLUB skizziert: 

_Vorbedingungen_ 

* [Ausgabengranularität](../../Anwendungshinweise_und_Weiteres/Diskussionen-Anwendung--Zeitungsmodul.md#granularit%C3%A4t), das bedeutat für jede Ausgabe wird ein [Vorgang](../../../Using/Anwenderhandbuch/V_1.11/Vorgang.md) angelegt. 
* [Beilagen](../../Anwendungshinweise_und_Weiteres/Diskussionen-Anwendung--Zeitungsmodul.md#beilagen) werden eigenständig bearbeitet, wenn eine ZDB-Aufnahme vorliegt. Ansonsten wird eine Beilage an die jeweilige Zeitungsausgabe angefügt, in der sie erschienen ist. 

*Scannen und Aufteilung der Images*

1. Scannen der Mikrofilme, beziehungsweise der Originale 
2. Ableitung der Erscheinungsweise der Zeitung (täglich, Mo bis Fr, ...) aus der ZDB oder anderen Quellen 
3. Abbildung der Erscheinungsweise in einer Excel-Tabelle 
4. Erstellen von Ordnern im Windows-Explorer mittels Batch-Funktion
5. Aufteilen der Images in Ordner "Ausgaben" (wenn die Images als Vorschaubilder angezeigt werden, können Ausgaben auf Grund der Titelseite  gut erkannt werden). 
Dabei können [Beilagen](../../Anwendungshinweise_und_Weiteres/Diskussionen-Anwendung--Zeitungsmodul.md#beilagen) gesondert aufgeteilt werden, wenn es gefordert ist. 
6. Während des Aufteilens werden fehlende Ausgaben identifiziert und in der Excel-Liste markiert [Diese werden nicht in Kitodo.Production angelegt] 
7. Während des Aufteilens werden Beilagen erkannt und in der Excel-Liste markiert [Diese können den Anforderungen entsprechend verarbeitet werden] 
8. Auf Basis der Tabelle werden für die vorhandenen Ausgaben die Vorgänge in Kitodo.Production mit dem [Zeitungsmodul](../../../Using/Anwenderhandbuch/V_1.11/Neuen-Vorgang-anlegen-I-Zeitungen.md) angelegt 
9. Auf Basis der ähnlichen Benennung der "Kitodo-Ordner" und der "Ausgabeordner" lassen sich die Images unkompliziert in den vorgesehen "Kitodo-Ordner" verschieben. 

Folgende Vorgaben haben diesen Workflow beeinflusst: 

* Es sollen so wenig Kitodo.Production-Vorgänge wie möglich gelöscht werden müssen 
* Aufteilung der Arbeitsschritte im Digitalisierungszentrum und in der Erschließung.
* Beilagen mit eigener ZDB-Nummer erhalten eigene Titelaufnahme und müssen extrahiert werden. 

Es ist jedoch auch möglich, Software für die Bearbeitung einzusetzen. Die SBB zum Beispiel nutzt das [Programm CreateMetadata](../../Anwendungshinweise_und_Weiteres/Diskussionen-Anwendung--Zeitungsmodul.md#skizze-des-geplanten-ablaufs-in-der-sbb). 

*Erschließung* 

Die Erschließung hängt von den jeweiligen Anforderungen ab. In der Regel wird nur eine Paginierung durchgeführt. 




