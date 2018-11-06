[Was macht man mit Kitodo.Production?](https://github.com/kitodo/kitodo-production/wiki/FAQs#was-macht-man-mit-kitodoproduction)

[Wie können die Scan Verzeichnisse hinzugefügt, entfernt oder umbenannt werden?](https://github.com/kitodo/kitodo-production/wiki/FAQs#wie-k%C3%B6nnen-die-scan-verzeichnisse-hinzugef%C3%BCgt-entfernt-oder-umbenannt-werden)

[Ist es möglich, mehrere Regelsätze in Kitodo.Production zu nutzen?](https://github.com/kitodo/kitodo-production/wiki/FAQs#ist-es-m%C3%B6glich-mehrere-regels%C3%A4tze-in-kitodoproduction-zu-nutzen)

[Wie werden die Metadaten aus Datenquellen importiert?](https://github.com/kitodo/kitodo-production/wiki/FAQs#wie-werden-die-metadaten-aus-datenquellen-importiert) 

[Was kann mit dem OPAC Beautifier geändert werden?](https://github.com/kitodo/kitodo-production/wiki/FAQs#was-kann-mit-dem-opac-beautifier-ge%C3%A4ndert-werden)

[Wie können mehrere gleiche Metadatenfelder mit unterschiedlichen Inhalten nach Kitodo.Production geladen werden?](https://github.com/kitodo/kitodo-production/wiki/FAQs#wie-k%C3%B6nnen-mehrere-gleiche-metadatenfelder-mit-unterschiedlichen-inhalten-nach-kitodoproduction-geladen-werden)

[Wozu dient die tiffwriter.conf-Datei?](https://github.com/kitodo/kitodo-production/wiki/FAQs#wozu-dient-die-tiffwriterconf-datei)

[Können Strukturelemente und deren Metadaten in der XML-Datei kopiert werden?](https://github.com/kitodo/kitodo-production/wiki/FAQs#k%C3%B6nnen-strukturelemente-und-deren-metadaten-in-der-xml-datei-kopiert-werden)

[Unterstützt Kitodo.Production UTF-8?](https://github.com/kitodo/kitodo-production/wiki/FAQs#unterst%C3%BCtzt-kitodoproduction-utf-8)

[Wie kann der Laufzettel in Kitodo.Production angepasst werden?](https://github.com/kitodo/kitodo-production/wiki/FAQs#wie-kann-der-laufzettel-in-kitodoproduction-angepasst-werden)

---


### Was macht man mit Kitodo.Production?

Kitodo.Production ist Teil von Kitodo und ermöglicht die Steuerung von Digitalisierungsprozessen. Dies beinhaltet unter anderem das Management von Arbeitsschritten wie Scannen, Strukturdatenerfassung und somit das Erstellen und Verwalten von Workflows als auch die Benutzerverwaltung. 

Weitere allgemeine Informationen zu Kitodo.Production finden sich unter http://www.kitodo.org/software/kitodoproduction/. 

---

### Wie können die Scan Verzeichnisse hinzugefügt, entfernt oder umbenannt werden?

Das Hinzufügen / Entfernen / Umbenennen von Scan-Verzeichnissen kann in Kitodo.Production nicht einfach umgesetzt werden. Der Grund ist die Auswirkung der Ordnerstruktur auf die Verlinkung in das Homeverzeichnis. Wenn die Ordnerstruktur geändert wird, muss auch das Shell-Skript für die Verlinkung geändert werden.

In der Installationsanleitung finden sich Informationen zu diesem Thema an zwei Stellen unter WEB-INF/classes/goobi_config.properties anpassen [1]:

- Unter „Verzeichnisse für Scans konfigurieren“ sind die Konfigurationsparameter genannt  
- Unter „Shell-Skripte konfigurieren (Vorlagen in Github unter Goobi/scripts/)“ sind die Pfade zu den Shell-Skripten genannt. Vorlagen finden sich in GitHub [2].  



[1] (https://github.com/kitodo/kitodo-production/wiki/Installationsanleitung-f%C3%BCr-Goobi.Production-CE-1.10#3-web-infclassesgoobi_configproperties-anpassen)

[2](https://github.com/kitodo/kitodo-production/tree/master/Kitodo/scripts "https://github.com/kitodo/kitodo-production/tree/master/Kitodo/scripts")

---

### Ist es möglich, mehrere Regelsätze in Kitodo.Production zu nutzen?

Es ist möglich, mehrere Regelsätze für eine Institution zu erstellen. Die Regelsätze müssen in dem dafür vorgesehenen Ordner [1] vorliegen. In der Produktionsvorlage kann der Regelsatz ausgewählt werden [2].

Mehrere Regelsätze bieten die Möglichkeit, Quelldaten für bestimmte Vorgänge unterschiedlich zu importieren, beziehungsweise zu exportieren. Dies kann genutzt werden, um zum Beispiel Metadaten von RAK- und RDA-Aufnahmen in Kitodo.Production verarbeiten zu können. Es kann jedoch nicht ausgeschlossen werden, dass Konfigurationen an anderer Stelle in Kitodo.Production eine parallele Verarbeitung von RAK und RDA verhindern. Zusätzlich bedeuten mehrere Regelsätze einen höheren Pflegeaufwand.

Im Wiki finden sich an Informationen an mehreren Stellen: 

* Pfad zu dem Verzeichnis, an dem die Regelsatz-Dateien gespeichert werden [1] 
* Erläuterungen zur Regelsatz-Datei [2]
* Auswahl des Regelsatzes für eine Produktionsvorlage [3] 
* Beispiel SBB-PK [4]


[1] https://github.com/kitodo/kitodo-production/wiki/Installationsanleitung-f%C3%BCr-Goobi.Production-CE-1.10#1-verzeichnisse-anlegen-pfade-nach-bedarf-anpassen

[2](../Using/Anwenderhandbuch/V_1.11/Regelsatz-XML-Datei.md "Regelsatz-XML-Datei")

[3](../Using/Anwenderhandbuch/V_1.11/Bearbeitung-Produktionsvorlage.md#1-festlegen-der-details-f%C3%BCr-einen-vorgang-produktionsvorlage "Bearbeitung-Produktionsvorlage")

[4](Von_Anwendern/SBB/Staatsbibliothek-zu-Berlin---Preußischer-Kulturbesitz.md#Regelsätze "Regelsätze")

---

### Wie werden die Metadaten aus Datenquellen importiert?

Kitodo.Production kann standardmäßig nur PICA OPACs nutzen. Die Verbindungsdaten werden in der goobi_opac.xml [1] angegeben. Nur wenn diese korrekt angegeben sind, ist es möglich, Metadaten automatisch beim Anlegen der Vorgänge zu importieren.

In der goobi_opac.xml können mehrere PICA-OPACs als Quelle angegeben werden. Beim Anlegen von Vorgängen kann über ein Drop-Down-Menü der jeweilige Katalog ausgewählt werden.

Zum Beispiel: 

```
...
<catalogue title="SWB">
<config
    description="Südwestdeutscher Bibliotheksverbund Baden-Württemberg, Saarland, Sachsen (SWB)"
    address="swb.bsz-bw.de" port="80" database="2.1" iktlist="IKTLIST-SWB.xml" charset="UTF-8" />
</catalogue>
 
<catalogue title="GBV">
<config
    description="Gemeinsamer Bibliotheksverbund"
    address="gso.gbv.de" port="80" database="2.1" iktlist="IKTLIST-GBV.xml" />
</catalogue>
...
```

Über einen Identifier werden die Metadaten abgerufen. Je nach Dokumenttyp müssen noch zusätzliche Felder belegt werden [2]. 


[1] https://github.com/kitodo/kitodo-production/blob/master/Goobi/config/goobi_opac.xml

[2](../Using/Anwenderhandbuch/V_1.11/Neuen-Vorgang-anlegen.md "Neuen Vorgang anlegen")

---

### Was kann mit dem OPAC Beautifier geändert werden?

Mit dem OPAC Beautifier [1] kann der Import der Metadaten korrigiert werden. Dies wird in der goobi_opac.xml [2] Datei konfiguriert. 

Mögliche Anwendungsbeispiele sind:

- Zusammenmappen mehrerer Metadatenfelder ([1] Seite 13)
- Löschen aller "@"-Zeichen in einem Metadatum ([1] Seite 14)
- Definition des Dokumenttyps anhand der Inhalte aus mehreren Feldern

 

Zum Beispiel kann das Digitalisat einer Handschrift durch die Inhalte der beiden PICA-Felder "002@" und "013H" definiert werden:


```
...
<catalogue title="SWB">
    <config
        description="Südwestdeutscher Bibliotheksverbund Baden-Württemberg, Saarland, Sachsen (SWB)"
        address="swb.bsz-bw.de" port="80" database="2.1" iktlist="IKTLIST-SWB.xml" charset="UTF-8" />
    <beautify>
        <setvalue tag="002@" subtag="0" value="Oz">
            <condition tag="002@" subtag="0" value="Oa.*" />
            <condition tag="013H" subtag="0" value="hand" /> 
        </setvalue>
    </beautify>
</catalogue>
...
```


[1](http://www.goobi.org/fileadmin/groups/goobi/dokumentation/TS-1105_Weiterentwicklungen-GOOBI-WLB.pdf "TS-1105_Weiterentwicklungen-GOOBI-WLB.pdf")

[2](https://github.com/kitodo/kitodo-production/blob/master/Goobi/config/goobi_opac.xml "")

---

### Wie können Vorgänge in unterschiedliche Präsentationen exportiert werden?  

Wenn Vorgänge in unterschiedliche Präsentationen exportiert werden sollen, kann dies in den Projekteinstellungen [1] unter Technische Daten [2] geändert werden.

Dazu muss in den folgenden Feldern der Pfad angepasst werden:

- DMS-Export-Ordner für XML-Datei
- DMS-Export-Images-Ordner

 

[1](../Using/Anwenderhandbuch/V_1.11/Bearbeitung-Projekte.md "Bearbeitung Projekte")

[2](../Using/Anwenderhandbuch/V_1.11/Bearbeitung-Projekte.md#technische-daten "Bearbeitung Projekte")

---

### Wie können mehrere gleiche Metadatenfelder mit unterschiedlichen Inhalten nach Kitodo.Production geladen werden? 

Wenn in einer Titelaufnahme wiederholbare Metadatenfelder, wie zum Beispiel die Fußnote 4201 (037A) enthalten sind, muss im Regelsatz [1, 2] dieses Feld als _num="*"_ definiert sein. Ansonsten kann das Feld nicht mehrfach nach Kitodo übernommen werden. 

[1](../Using/Anwenderhandbuch/V_1.11/Regelsatz.md "Regelsatz")

[2](../Using/Anwenderhandbuch/V_1.11/Regelsatz-XML-Datei.md "")

--- 

### Wozu dient die tiffwriter.conf-Datei? 

Mit Hilfe dieser Datei kann ein Perl-Skript die, einem Image seitens der Scan-Software im Tiff-Header hinterlegten Daten überschreiben, beziehungsweise erst erzeugen. [1]

[1](../BestPractice/Anwendungshinweise_und_Weiteres/Verwendung%20der%20tiffwriterconf-Datei.md "")

--- 

### Können Strukturelemente und deren Metadaten in der XML-Datei kopiert werden? 

Wenn die Strukturelemente und deren Metadaten gleicher oder ähnlicher Vorgänge nicht jeweils im Metadateneditor manuell eingegeben werden sollen, ist es möglich, die Daten direkt in der meta.xml-Datei zu kopieren [1]. Dies muss sehr sorgfältig durchgeführt werden! 

[1](../Using/Anwenderhandbuch/V_1.11/Kopieren-von-Strukturelmenten-und-deren-Metadaten-in-einer-meta.xml-Datei.md "")

--- 

### Unterstützt Kitodo.Production UTF-8? 

Kitodo.Production unterstützt UTF-8 und es können Sonderzeichen wie das sorbische Ṕ, ṕ, Ẃ, ẃ oder auch nicht-lateinische Schriftzeichen [1] verarbeitet werden. Die Eingabe im Metadateneditor wird jedoch nicht unterstützt. Daher müssen Sonderzeichen, die nicht auf der Tastatur vorhanden sind, aus anderen Systemen kopiert und eingefügt oder mit Tastenkombinationen eingegeben werden. 

[1](../BestPractice/Anwendungshinweise_und_Weiteres/Bearbeitung-von-Titeln-in-nicht-lateinischer-Sprache.md "")

--- 

### Wie kann der Laufzettel in Kitodo.Production angepasst werden? 

In Kitodo.Production kann ein Laufzettel [1] erstellt werden, der Angaben wie Signatur, Projektname, Identifier oder andere Angaben aus Werkstück- und Vorlageneigenschaften enthält. Die Angaben können in einer Konfigurationsdatei angepasst werden. Eine Anleitung dazu findet sich unter [2]. 

[1](../Using/Anwenderhandbuch/V_1.11/Laufzettel.md "Laufzettel")

[2](../Using/Anwenderhandbuch/V_1.11/Anpassungen-in-der-docket.xsl.md "") 

--- 