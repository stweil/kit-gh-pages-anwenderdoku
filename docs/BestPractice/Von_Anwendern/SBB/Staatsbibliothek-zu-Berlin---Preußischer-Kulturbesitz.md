# Anwenderdokumentation der _Staatsbibliothek zu Berlin - Preußischer Kulturbesitz_ 

In der Anwenderdokumentation der _Staatsbibliothek zu Berlin - Preußischer Kulturbesitz_ wird die Anwendung von Projekten, Produktionsvorlagen und Regelsätzen beschrieben. Zusätzlich werden einzelne Funktionen des Metadateneditors erläutert und Konfigurationsdateien annotiert. 


---
##### _Steckbrief_ 

- Goobi.Production seit März 2008 im Einsatz; zunächst mit Version 1.4.9; ab 2010 mit Version 1.5.1; ab 2017 Goobi.Production-CE-Version 1.11.2
- Digitalisierung von Druckschriften (Monographien, Mehrbändige Werke, Zeitschriften), Handschriften und Autographen (Musikhandschriften, Orientalische Handschriften, Abendländische Handschriften u.a.m.)
- Anzahl Vorgänge (Mai 2016): 98.000
- Präsentation: ursprünglich entspr. Göttinger Präsentation; aktuell Eigenentwicklung
- URL der Digitalisierten Sammlungen: [http://digital.staatsbibliothek-berlin.de](http://digital.staatsbibliothek-berlin.de)
- OAI-Schnittstelle: [http://digital.staatsbibliothek-berlin.de/oai](http://digital.staatsbibliothek-berlin.de/oai)

---

##### _[Anhängende Werke (PDF)](goobi-anhaengende-werke.pdf)_

In diesem Dokument wird beschrieben, wie anhängende Werke über den Befehl _Strukturelemente aus Opac hinzufügen_ die Struktur- und Metadaten einer anderen Publikation in einen Vorgang eingefügt werden können. 

Siehe auch: 

* [Strukturdaten bearbeiten](../../../Using/Anwenderhandbuch/V_1.11/Strukturdaten-bearbeiten.md)
* [Metadaten bearbeiten](../../../Using/Anwenderhandbuch/V_1.11/Metadaten-bearbeiten.md)

---

##### _[Konfigurations-Dateien (PPT)](goobi_Konfigdateien.ppt)_

In diesem Dokument werden die Konfigurationsdateien von Kitodo.Production skizziert. Dieses Dokument eignet sich hervorragend, um Artikel für die Dateien im Wiki zu erstellen und um diese mit der Installationsanleitung, beziehungsweise den Beispiel-Dateien zu verknüpfen.   

Siehe auch: 

* [Installationsanleitung für Goobi.Production CE 1.10](https://github.com/kitodo/kitodo-production/wiki/Installationsanleitung-f%C3%BCr-Goobi.Production-CE-1.10)
* [Regelsatz](../../../Using/Anwenderhandbuch/V_1.11/Regelsatz.md)
* [goobi_opac.xml](https://github.com/kitodo/kitodo-production/blob/master/Goobi/config/goobi_opac.xml)
* [goobi_projects.xml](https://github.com/kitodo/kitodo-production/blob/master/Goobi/config/goobi_projects.xml)
* [goobi_webapi.xml](https://github.com/kitodo/kitodo-production/blob/master/Goobi/config/goobi_webapi.xml)
* [goobi_metadataDisplayRules.xml](https://github.com/kitodo/kitodo-production/blob/master/Goobi/config/goobi_metadataDisplayRules.xml)

---

##### _Produktionsvorlagen_

Produktionsvorlagen werden modulartig aus bekannten Schritten zusammengesetzt und benannt. Zum Beispiel: 
* _V_Drucke_P17_DIGI_MAX_ (Workflow mit Strukturdatenerfassung für Projekt P17) 
* _V_Drucke_P17_WUENSCHE_MAX_ (Workflow mit Strukturdatenerfassung und Nutzerwunsch für Projekt P17) 

Somit kann aus dem Namen bereits auf grundsätzliche Abläufe im Digitalisierungsworkflow geschlossen werden.

Siehe auch:

* [Produktionsvorlage](../../../Using/Anwenderhandbuch/V_1.11/Produktionsvorlage.md)
* [Projektorganisation](../../../Using/Anwenderhandbuch/V_1.11/Projektorganisation.md)

---

##### _Projekte_

In der SBB sollen keine unnötigen Projekte eingerichtet werden. Daher werden neue Projekte in Kitodo.Production vor allem aus folgenden Gründen definiert:

* Projektspezifische Eigenschaften, die über Kitodo-Projekteigenschaften besetzt werden (z.B. abweichender Eigentümer der digitalisierten Vorlagen, abweichende digitalisierende Einrichtung)
* Notwendigkeit einer separaten projektspezifischen Statistik (Drittmittelprojekt)
* Vergabe gezielter Berechtigungen für Projektmitarbeiter

In der projects.xml-Konfigurationsdatei werden nur im begründeten Fall abweichende Projektfestlegungen definiert. 

Siehe auch:

* [Projekt](../../../Using/Anwenderhandbuch/V_1.11/Projekt.md)
* [goobi_digitalCollections.xml](https://github.com/kitodo/kitodo-production/blob/master/Goobi/config/goobi_digitalCollections.xml)
* [Projektorganisation](../../../Using/Anwenderhandbuch/V_1.11/Projektorganisation.md)

---

##### _Regelsätze_ 

In der SBB werden grundsätzlich vier Regelsätze für unterschiedliche Medientypen verwendet:

* Druckschriften
* Musikdrucke
* Handschriften
* Nachlässe

Sie unterscheiden sich vor allem in der Kombination definierter Metadaten bzw. einem materialspezifischen Export. Außerdem werden veränderte Regelsätze mit einem Datum gekennzeichnet, um Änderungen nachzuvollziehen zu können. Bei einem erneuten Export von Vorgängen ganzer Projekte müssen daher vorab alle Vorgänge auf den gewünschten Regelsatz mit Hilfe eines Skripts umgehängt werden.

Um die Abwärtskompatibilität der Regelsätze zu gewährleisten, werden alle einmal definierten Metadaten mitgeführt. Das gilt auch für Projektspezifika (zum Beispiel spezielle Metadaten für das Projekt _P_Drucke_Europeana1914-1918_).

Zur Veranschaulichung wird eine [Regelsatz-Datei](SBB_Regelsatz_Drucke_Kommentiert_20160423.xml) bereitgestellt. **Achtung**: Dieser Regelsatz wird nicht zur praktischen Anwendung bereitgestellt! Ohne die ursprüngliche Kitodo.Production-Umgebung kann eine erfolgreiche Implementierung nicht garantiert werden. 

Siehe auch:

* [Regelsatz](../../../Using/Anwenderhandbuch/V_1.11/Regelsatz.md)
* [Regelsatz XML Datei](../../../Using/Anwenderhandbuch/V_1.11/Regelsatz-XML-Datei.md)

---