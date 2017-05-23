# Einleitung

Auf dieser Seite wird die Struktur der Regelsatz-Datei der SLUB erläutert. 

Die Datei besteht aus den drei Bereichen: 

* Metadaten-Bereich
* Strukturelemente-Bereich
* Formate-Bereich 
 * PicaPlus
 * MODS


# Metadaten-Bereich
In diesem Bereich sind die Metadaten aufgelistet, die in Kitodo.Production verwendet werden können, um im Metadateneditor Strukturelemente zu beschreiben. Dieser Bereich untergliedert sich in folgende Bereiche:

* Metadaten für die physische Dokumentstruktur
* Metadaten für die logische Dokumentstruktur

Jedes Element besteht aus den Feldern:

`<Name>`: Diese Zeile definiert die Benennung des Elements im Dateisystem von Kitodo.Production.

`<language name="de">`: Diese Zeile definiert die deutsche Benennung des Metadatums, wie es dem Anwender im Metadateneditor angezeigt wird. 

`<language name="en">`: Diese Zeile definiert die englische Benennung des Metadatums, wie es dem Anwender im Metadateneditor angezeigt wird.

Die Inhalte in den zwei Bereichen folgen dem gleichen Schema, zum Beispiel: 

---
	<MetadataType>
        	<Name>TitleDocMain</Name>
        	<language name="de">Haupttitel</language>
        	<language name="en">main title</language>
	</MetadataType>
---

Einen Sonderfall stellen dabei Personenmetadaten dar. Diese werden durch ein zusätzliches Attribut gekennzeichnet. Das führt dazu, dass Kitodo.Production dieses Metadatum automatisch in Form mehrerer gruppierter Unterfelder behandelt. Statt eines einzigen Eingabefeldes erscheinen separate Felder für Vor- und Nachname, Rolle der Person und GND-Identifier:

---
	<MetadataType type="person">
        	<Name>Author</Name>
        	<language name="de">Autor</language>
        	<language name="en">Author</language>
	</MetadataType>
---


# Strukturelemente-Bereich
In diesem Bereich sind die Strukturelemente aufgelistet, die in Kitodo.Production verwendet werden können. Zudem wird hier definiert, welche Kind-Strukturelemente ein Strukturelement enthalten darf und welche Metadata dem Strukturelement zugewiesen werden dürfen. Dieser Bereich ist nicht weiter untergliedert. 

`<Name>`: Diese Zeile definiert die Benennung des Elements im Dateisystem von Kitodo.Production. 

`<language name="de">`: Diese Zeile definiert die deutsche Benennung des Metadatums, wie es dem Anwender im Metadateneditor angezeigt wird. 

`<language name="en">`: Diese Zeile definiert die englische Benennung des Metadatums, wie es dem Anwender im Metadateneditor angezeigt wird.

`<allowedchildtype>`: Diese Zeilen benennen Strukturelemente, die als Kind-Elemente angelegt werden können.

`<metadata>`: Diesen Zeilen benennen Metadatenfelder, die zur Erschließung des Strukturelements genutzt werden können. Es enthält mehrere Attribute:
* `num="*"` Dieses Attribut bewirkt, dass das Feld mehrfach beliebig oft in einem Strukturelement angelegt werden kann (0 - n Mal).
* `num="1o"` Dieses Attribut bewirkt, dass das Feld nur einmal in einem Strukturelement angelegt werden kann (0 - 1 Mal).  
* `num="1m"` Dieses Attribut bewirkt, dass das Feld genau einmal in einem Strukturelement angelegt werden muss (1 Mal). 
* `DefaultDisplay="true"` Dieses Attribut bewirkt, dass das Feld bei der Auswahl des Strukturelement angezeigt wird und nicht ausgewählt werden muss.

*zum Beispiel:*

---
	<DocStrctType>
		<Name>Bibliography</Name>
		<language name="de">Bibliographie</language>
		<language name="en">Bibliography</language>
		<allowedchildtype>Appendix</allowedchildtype>
		<allowedchildtype>Introduction</allowedchildtype>
		<allowedchildtype>Chapter</allowedchildtype>
		<allowedchildtype>Errata</allowedchildtype>
		<allowedchildtype>IllustrationDescription</allowedchildtype>
		<allowedchildtype>OtherDocStrct</allowedchildtype>
		<allowedchildtype>Preface</allowedchildtype>
		<allowedchildtype>TableDescription</allowedchildtype>
		<metadata num="*">Author</metadata>
		<metadata DefaultDisplay="true" num="1o">TitleDocMain</metadata>
		<metadata num="1o">TitleDocMainShort</metadata>
		<metadata num="*">DocLanguage</metadata>
		<metadata num="*">slub_Digitizer</metadata>
		<metadata num="*">slub_Finance</metadata>
	</DocStrctType>
---

Die Überordnungen von mehrbändigen Werken (sog. "anchor") werden durch das Attribut anchor="true" gekennzeichnet. In der Regel besitzen diese Anker-Elemente nur ein einziges <allowedchildtype>:

---
	<DocStrctType anchor="true">
        	<Name>Periodical</Name>
			<language name="de">Zeitschrift</language>
			<language name="en">periodical</language>
			<allowedchildtype>PeriodicalVolume</allowedchildtype>
			<metadata num="1o">ProcessID</metadata>
			<metadata DefaultDisplay="true" num="1m">CatalogIDDigital</metadata>
			<metadata DefaultDisplay="true" num="*">CatalogIDSource</metadata>
			<metadata DefaultDisplay="true" num="*">PublicationRun</metadata>
			<metadata num="1o">PublicationStart</metadata>
			<metadata num="1o">PublicationEnd</metadata>
			<metadata DefaultDisplay="true" num="*">ISSN</metadata>
  	  </DocStrctType>

---

# Formate-Bereich
In diesem Bereich ist dokumentiert, wie die Metadaten und Strukturelemente aus den ersten beiden Bereichen in andere Formate gemappt werden. Dieser Bereich untergliedert sich in folgende Bereiche:

* RDF (nicht mehr in Verwendung)
* PicaPlus 
* MODS

## RDF
Dies ist obsolet und soll sollte nicht genutzt werden. Er diente früher dem Export von AgoraXML.

## PicaPlus 

Pica Plus wird genutzt, um die Titeldaten aus dem SWB zu importieren. Es gibt einen Bereich für Personenmetadaten und einen Bereich für Titelmetadaten.

Die **Personenmetadaten** bestehen aus den Feldern:

`<picaMainTag>`: Diese Zeile definiert die Benennung des Elements im Dateisystem von Kitodo.Production.

`<Name>`: Benennung des Feldes

`<picaSubTag type="firstname">`: Hier wird das Subfeld benannt, das den Vornamen des Autors enthält.

`<picaSubTag type="lastname">`: Hier wird das Subfeld benannt, das den Nachnamen des Autors enthält.

`<picaSubTag type="identifier">`: Hier wird das Subfeld benannt, das die PPN des Personendatensatzen des Autors enthält.

`<picaSubTag type="expansion">`: Hier wird das Subfeld benannt, das die Expansion (Anzeige des Namens) des bevorzugten Namens enthält


*zum Beispiel:*

---
	<Person>
		<picaMainTag>028A</picaMainTag>
		<Name>Author</Name>
		<picaSubTag type="firstname">d</picaSubTag>
		<picaSubTag type="lastname">a</picaSubTag>
		<picaSubTag type="identifier">9</picaSubTag>
		<picaSubTag type="expansion">8</picaSubTag>
	</Person>
---

Die **Titelmetadaten** bestehen aus den Feldern:

`<picaMainTag>`: Diese Zeile definiert die Benennung des Elements im Dateisystem von Kitodo.Production.

`<Name>`: Benennung des Feldes

`<picaSubTag>`: Hier wird das Subfeld benannt, das den gewünschten Inhalt enthält.

*zum Beispiel:*

---
	<Metadata>
		<picaMainTag>021A</picaMainTag>
		<picaSubTag>a</picaSubTag>
		<Name>TitleDocMain</Name>
	</Metadata>
---


## MODS

MODS ist das Format, das ausgegeben wird. METS-Elemente beschreiben die Struktur des Dokuments und MODS-Elemente beschreiben deskriptive Eigenschaften des Dokuments.

In diesem Bereich werden die intern genutzen Benennungen nach MODS oder METS gemappt.

### MODS

Das MODS Schema findet sich unter folgender URL: http://www.loc.gov/standards/mods/v3/mods-3-6.xsd. Auch hier unterscheiden sich die Personenmetadaten von den Titelmetadaten

Die **Personenmetadaten** bestehen aus den Feldern:

`<InternalName>`: Dieses Feld beinhaltet die Kitodo.Production-interne Bezeichnung des Feldes.

`<MODSName>`: Dieses Feld gibt an, dass es sich um Personenmetadatensatz handelt.

`<WriteXPath>`: Dieses Feld gibt Art und Ort des MODS-Feld an, das zum Mapping genutzt wird.

`<FirstnameXPath>`: Dieses Feld gibt Art und Ort des MODS-Feld an, das zum Mapping genutzt wird.

`<LastnameXPath>`: Dieses Feld gibt Art und Ort des MODS-Feld an, das zum Mapping genutzt wird.

`<DisplayNameXPath>`: Dieses Feld gibt Art und Ort des MODS-Feld an, das zum Mapping genutzt wird.

`<IdentifierXPath>`: Dieses Feld gibt Art und Ort des MODS-Feld an, das zum Mapping genutzt wird.

*zum Beispiel:*

---
	<Metadata>
		<InternalName>Author</InternalName>
		<MODSName>Person</MODSName>
		<WriteXPath>./mods:mods/#mods:name[@type='personal'][mods:role/mods:roleTerm='aut'[@authority='marcrelator'][@type='code']]</WriteXPath>
		<FirstnameXPath>./mods:namePart[@type='given']</FirstnameXPath>
		<LastnameXPath>./mods:namePart[@type='family']</LastnameXPath>
		<DisplayNameXPath>./mods:displayForm</DisplayNameXPath>
		<!-- Yet still hardcoded in UGH -->
		<IdentifierXPath>../mods:name[@authority='pnd']/@ID</IdentifierXPath>
	</Metadata>
---

Die **Titelmetadaten** bestehen aus den Feldern:

`<InternalName>`: Dieses Feld beinhaltet die Kitodo.Production-interne Bezeichnung des Feldes.

`<WriteXPath>`: Dieses Feld gibt Art und Ort des MODS-Feld an, das zum Mapping genutzt wird. Achtung: Es dürfen keine doppelten Anführungszeichen verwendet werden! Das Rautensymbol "#" gibt an, ab welcher Ebene im XML ein neues Subelement angelegt werden soll.


*zum Beispiel:*

(wenn ./mods:mods/mods:titleInfo bereits existiert, wird darin ein neues /mods:title angelegt, andernfalls wird der ganze Pfad neu angelegt):

---
	<Metadata>
		<InternalName>TitleDocMain</InternalName>
    		<WriteXPath>./mods:mods/mods:titleInfo/#mods:title</WriteXPath>
	</Metadata>
---

Zusätzlich können über die folgenden Angabe weitere Manipulationen der Feldinhalte vorgenommen werden:

`<valueCondition>`: Dieses Feld enthält einen regulären Ausdruck. Nur wenn dieser Ausdruck auf den Inhalt des Feldes zutrifft, wird das Feld ausgegeben.

`<valueRegExp>`: Dieses Feld enthält einen regulären Ausdruck, der auf den Feldinhalt angewendet wird. Das Ergebnis wird dann ausgegeben.

Das sieht zum Beispiel so aus (nur wenn der Schrifttyp "fraktur" ist, soll das Feld ausgegeben werden, wobei "fraktur" dabei durch "Latf" ersetzt werden soll):

---
	<Metadata>
		<InternalName>slub_script</InternalName>
		<ValueCondition>/^fraktur$/i</ValueCondition>
		<ValueRegExp>s/(.*)/Latf/</ValueRegExp>
		<WriteXPath>./mods:mods/mods:language/#mods:scriptTerm[@type='code'][@authority='iso15924']</WriteXPath>
	</Metadata>
---

Zu beachten ist, dass ein internes Feld im MODS-Mapping mehrfach vorkommen darf und dann auch mehrfach ausgegeben wird. Zum Beispiel:

---
	<Metadata>
		<InternalName>CatalogIDDigital</InternalName>
		<ValueRegExp>s/(.*)/oai:de:slub-dresden:db:id-$1/</ValueRegExp>
		<WriteXPath>./mods:mods/#mods:recordInfo/mods:recordIdentifier[@source='http://digital.slub-dresden.de/oai/']</WriteXPath>
	</Metadata>
	<Metadata>
		<InternalName>CatalogIDDigital</InternalName>
		<ValueCondition>/^[0-9]{8}[0-9X]{1}$/</ValueCondition>
		<WriteXPath>./mods:mods/#mods:identifier[@type='swb-ppn']</WriteXPath>
	</Metadata>
	<Metadata>
		<InternalName>CatalogIDDigital</InternalName>
		<ValueRegExp>s/(.*)/http:\/\/digital\.slub-dresden\.de\/id$1/</ValueRegExp>
		<WriteXPath>./mods:mods/#mods:identifier[@type='purl']</WriteXPath>
	</Metadata>
---


### METS

Beim METS-Mapping handelt es sich nicht um METS im strengen Sinne. Eigentlich werden hier nur die internen Bezeichnungen für Strukturelemente in standardisierte Begriffe übertragen (z.B. entsprechend des DFG-Viewer-Strukturdatensets). Diese Begriffe werden dann innterhalb der METS-Struktur als "type" der Strukturelemente verwendet.

`<InternalName>`: Dieses Feld beinhaltet die Kitodo.Production-interne Bezeichnung des Feldes.

`<MetsType>`: Dieses Feld beinhaltet die METS-Bezeichnung des Feldes.

*zum Beispiel:*

---
	<DocStruct>
		<InternalName>Chapter</InternalName>
		<MetsType>chapter</MetsType>
	</DocStruct>
---
