# Einleitung 
In Kitodo.Production werden Projekteinstellungen in der Datei "goobi_projects.xml" Im KonfigurationVerzeichnis gespeichert. in der [Installationsanleitung](https://github.com/kitodo/kitodo-production/wiki/Installationsanleitung) gibt es Erläuterungen zu den einzelnen Feldern.

Im Allgemeinen dient die Datei dazu:
- die Metadatenfelder zu definieren, die beim Anlegen eines Vorgangs angezeigt werden sollen, beziehungsweise die ausgeblendet werden sollen
- die Bildung des Vorgangstitels zu definieren
- die Bildung des tifheader zu definieren
- projektspezifische Felder, wie zum Beispiel einen Förderer einzutragen, so dass diese Daten nicht nachträglich eingegeben werden müssen.

Zur Verdeutlichung wird eine Beispiel-Datei [goobi_projects.xml](SLUB_Doku/goobi_projects_example.xml) bereit gestellt.

# Erste Ebene
Auf der obersten Ebene ist die Datei recht übersichtlich. Wenn keine projektspezifischen Angaben benötigt werden, ist der Abschnitt <project name="default"> ausreichend.

	<?xml version="1.0" encoding="UTF-8"?>
	<goobiProjects>
		<project name="default">
		<project name="VD_17">
		<project name="VD_18">
		<project name="Opernarchiv">
		<project name="Zeitungen_DFG">
		<project name="Hofkirche">
	</goobiProjects>

# Zweite Ebene 
Die Zweite Ebene enthält in diesem Beispiel vier Bereiche:

	<?xml version="1.0" encoding="UTF-8"?>
	<goobiProjects>
		<project name="default">
			<createNewProcess>
			<tifheader>
			<dmsImport/>
			<validate>
		</project>
	</goobiProjects>


- `<createNewProcess>`
beinhaltet Informationen darüber, welche Felder (Titel, Autor, Signatur, ...) beim Anlegen neuer Vorgänge angezeigt werden.
    beinhaltet zumeist Informationen, die in der zuvor erwähnten Anleitung erläutert sind.
- `<tifheader>`
    beinhaltet Informationen darüber, welche Inhalte in den TIf-Header geschrieben werden.
- `<dmsImport/>`
    wird in der SLUB nicht genutzt.
- `<validate>`
    definiert, dass alle Personen in den Titelmetadaten angelegt werden.

*Hinweis*: Fast alle Angaben sind medientypabhängig, so dass das Attribut isdoctype korrekt ausgefüllt werden muss.

## Beispiel `<createNewProcess>`

`<createNewProcess>` kann zum Beispiel so aussehen:

	<?xml version="1.0" encoding="UTF-8"?>
	<goobiProjects>
		<project name="default">
			<createNewProcess>
				<itemlist>
					<item from="werk"> Artist
						<select label="SLUB"> Sächsische Landesbibliothek - Staats- und Universitätsbibliothek Dresden, Germany </select>
					</item>

					<!-- Schrifttyp -->
					<item from="werk" isdoctype="monograph|manuscript|newspaper" required="true" ughbinding="true" docstruct="topstruct" metadata="slub_script">Schrifttyp
						<select label="Antiqua">Antiqua</select>
						<select label="Fraktur">Fraktur</select>
						<select label="keine OCR">keine_OCR</select>
					</item>
					<item from="werk" isdoctype="periodical|multivolume" required="true" ughbinding="true" docstruct="firstchild" metadata="slub_script">Schrifttyp
						<select label="Antiqua">Antiqua</select>
						<select label="Fraktur">Fraktur</select>
						<select label="keine OCR">keine_OCR</select>
					 </item>

					<!-- Konvolut -->
					<item from="werk" isdoctype="bundle" required="true" ughbinding="true" docstruct="firstchild" metadata="slub_script">Schrifttyp
                    <select label="keine OCR">keine_OCR</select>
					</item>

					<!-- Besitzer der Vorlage -->
					<item from="werk" isdoctype="monograph|manuscript|newspaper" ughbinding="true" metadata="slub_ownerOrig" docstruct="topstruct">Besitzer der Vorlage</item>
					<item from="werk" isdoctype="multivolume|periodical" ughbinding="true" metadata="slub_ownerOrig" docstruct="firstchild">Besitzer der Vorlage</item>

					<!-- Titel -->
					<item from="vorlage" isdoctype="monograph|multivolume|periodical|manuscript|newspaper" required="true" ughbinding="true" docstruct="topstruct" metadata="TitleDocMain"> Titel </item>
					<item from="vorlage" isdoctype="monograph|multivolume|periodical|manuscript|newspaper" required="true" ughbinding="true" docstruct="topstruct" metadata="TitleDocMainShort"> Titel (Sortierung)</item>
					<!-- Titel für Konvolut -->
					<item from="vorlage" isdoctype="bundle" required="true" ughbinding="true" docstruct="topstruct" metadata="TitleDocMain">Titel Konvolut</item>

					<!-- Urheber -->
 					<item from="vorlage" isdoctype="monograph|multivolume|periodical|manuscript" ughbinding="true" docstruct="topstruct" metadata="ListOfCreators"> Autoren </item>
					<!-- Identifikator -->
					<item from="werk" isnotdoctype="periodical|newspaper" ughbinding="true" metadata="TSL_ATS" docstruct="topstruct">ATS</item>
					<item from="werk" isdoctype="periodical|newspaper" ughbinding="true" metadata="TSL_ATS" docstruct="topstruct">TSL</item>
					<item from="vorlage" isdoctype="multivolume" ughbinding="true" docstruct="topstruct" metadata="CatalogIDSource"> PPN analog c-Satz </item>
					<item from="werk" isdoctype="multivolume" required="true" ughbinding="true" docstruct="topstruct" metadata="CatalogIDDigital"> PPN digital c-Satz</item>
					<item from="vorlage" isdoctype="monograph|manuscript" ughbinding="true" docstruct="topstruct" metadata="CatalogIDSource"> PPN analog a-Satz </item>
					<item from="werk" isdoctype="monograph|manuscript" required="true" ughbinding="true" docstruct="topstruct" metadata="CatalogIDDigital"> PPN digital a-Satz</item>
					<item from="vorlage" isdoctype="periodical|newspaper" required="true" ughbinding="true" docstruct="topstruct" metadata="CatalogIDSource"> PPN analog b-Satz </item>
					<item from="werk" isdoctype="periodical|newspaper" required="true" ughbinding="true" docstruct="topstruct" metadata="CatalogIDDigital"> PPN digital b-Satz</item>
					<item from="werk" isdoctype="periodical|newspaper" ughbinding="true" docstruct="topstruct" metadata="ISSN"> ISSN </item>
					<item from="vorlage" isdoctype="periodical" ughbinding="true" docstruct="firstchild" metadata="CatalogIDSource"> PPN analog Band </item>
					<item from="werk" required="true" isdoctype="periodical" ughbinding="true" docstruct="firstchild" metadata="CatalogIDDigital"> PPN digital Band </item>
					<item from="vorlage" isdoctype="bundle" required="true" ughbinding="true" docstruct="topstruct" metadata="CatalogIDDigital">Identifikator Konvolut</item>
					<item from="werk" isdoctype="bundle" required="true" ughbinding="true" docstruct="firstchild" metadata="CatalogIDDigital">Identifikator Mappe</item>
					<item from="vorlage" isdoctype="newspaper" ughbinding="true" docstruct="topstruct" metadata="CatalogIDPeriodicalDB">ZDB-ID</item>

					<!--Informationen für Bände -->
					<item from="vorlage" isdoctype="multivolume" ughbinding="true" docstruct="firstchild" metadata="TitleDocMain"> Titel (Band)</item>
					<item from="vorlage" isdoctype="multivolume" ughbinding="true" docstruct="firstchild" metadata="TitleDocMainShort"> Titel (Band) (Sortierung)</item>
					<item from="vorlage" isdoctype="periodical" ughbinding="true" docstruct="firstchild" metadata="TitleDocMain"> Titel (Band)</item>
					<item from="vorlage" isdoctype="periodical" ughbinding="true" docstruct="firstchild" metadata="TitleDocMainShort"> Titel (Band) (Sortierung)</item>
					<item from="vorlage" isdoctype="multivolume" ughbinding="true" docstruct="firstchild" metadata="ListOfCreators"> Autoren (Band)</item>
					<item from="vorlage" isdoctype="bundle" ughbinding="true" docstruct="firstchild" metadata="TitleDocMain">Titel (Mappe)</item>
					<item from="vorlage" isdoctype="bundle" required="true" ughbinding="true" docstruct="firstchild" metadata="CurrentNo">Mappennummer</item>
					<item from="vorlage" isnotdoctype="monograph|manuscript|newspaper" ughbinding="true" docstruct="firstchild" metadata="CurrentNo"> Bandnummer </item>
					<item from="vorlage" isnotdoctype="monograph|manuscript|bundle|newspaper" required="true" ughbinding="true" docstruct="firstchild" metadata="CurrentNoSorting"> Nummer (Sortierung) </item>
					<item from="vorlage" isdoctype="multivolume|periodical"> Nummer (Benennung) </item>
					<item from="vorlage" isdoctype="multivolume" ughbinding="true" docstruct="firstchild" metadata="CatalogIDSource"> PPN analog f-Satz </item>
					<item from="werk" required="true" isdoctype="multivolume" ughbinding="true" docstruct="firstchild" metadata="CatalogIDDigital"> PPN digital f-Satz </item>

					<!-- Sprache für Zeitungen -->
					<item from="werk" isdoctype="newspaper" ughbinding="true" docstruct="topstruct" metadata="DocLanguage">Sprache</item>

					<!-- Erscheinungsjahr, Erscheinungsort und Verlag -->
					<item from="vorlage" isdoctype="monograph|multivolume|periodical|newspaper|manuscript" ughbinding="true" docstruct="topstruct" metadata="PlaceOfPublication"> Erscheinungsort </item>
					<item from="vorlage" isdoctype="monograph|manuscript" ughbinding="true" docstruct="topstruct" metadata="PublicationYear"> Erscheinungsjahr </item>
					<item from="vorlage" isdoctype="periodical|newspaper|multivolume" ughbinding="true" docstruct="firstchild" metadata="PublicationYear"> Erscheinungsjahr </item>
					<item from="vorlage" isdoctype="multivolume|periodical" ughbinding="true" docstruct="firstchild" metadata="PublisherName"> Verlag </item>
					<item from="vorlage" isdoctype="monograph|manuscript|newspaper" ughbinding="true" docstruct="topstruct" metadata="PublisherName"> Verlag </item>

					<!-- Signatur -->
					<item from="vorlage" isdoctype="multivolume" ughbinding="true" docstruct="firstchild" metadata="shelfmarksource"> Signatur </item>
					<item from="vorlage" isdoctype="monograph|manuscript" ughbinding="true" docstruct="topstruct" metadata="shelfmarksource"> Signatur </item>
					<item from="vorlage" isdoctype="periodical" ughbinding="true" docstruct="firstchild" metadata="shelfmarksource"> Signatur </item>

					<!-- Informationen für Konvolut -->
					<item from="vorlage" isdoctype="bundle" ughbinding="true" docstruct="firstchild" metadata="shelfmarksource">Signatur</item>
					<item from="vorlage" isdoctype="bundle" ughbinding="true" docstruct="topstruct" metadata="slub_ownerOrig">Besitzende Institution (Vorlage)</item>
					<item from="vorlage" isdoctype="bundle" ughbinding="true" docstruct="topstruct" metadata="slub_ownerDigi">Besitzende Institution (Digitalisat)</item>
					<item from="werk" isdoctype="bundle" ughbinding="true" docstruct="firstchild" metadata="slub_ownerOrig">Besitzende Institution (Vorlage)</item>
					<item from="werk" isdoctype="bundle" ughbinding="true" docstruct="firstchild" metadata="slub_ownerDigi">Besitzende Institution (Digitalisat)</item>

					<!-- Vorgangstitel -->
					<processtitle isdoctype="multivolume">ATS+TSL+'_'+PPN digital f-Satz+'_'+Nummer (Benennung)</processtitle>
					<processtitle isdoctype="monograph|manuscript">ATS+TSL+'_'+PPN digital a-Satz</processtitle>
					<processtitle isdoctype="periodical">TSL+'_'+PPN digital Band+'_'+Nummer (Benennung)</processtitle>
					<processtitle isdoctype="bundle">ATS+TSL+'_'+Identifikator Mappe+'_'+Mappennummer</processtitle>
					<processtitle isdoctype="newspaper">TSL+'_'+PPN digital b-Satz+'-'+#YEAR+#MONTH+#DAY+'_'+#issu</processtitle>
					<hide/>
				</itemlist>
				<opac use="true">
					<catalogue>SWB</catalogue>
				</opac>
				<templates use="true"/>
				<defaultdoctype>monograph</defaultdoctype>
				<metadatageneration use="true"/>
			</createNewProcess>
		</project>
	</goobiProjects>


**Dies sind BEISPIELE!**, um zu demonstrieren, wie diese Datei aussehen kann. Sie kann natürlich auch an die lokalen Bedürfnisse angepasst werden.
 
## Erklärung zu den item Tags

	...
	<item from="werk" isnotdoctype="periodical|newspaper" ughbinding="true" metadata="TSL_ATS" docstruct="topstruct">ATS</item>
	...
	<item from="vorlage" isdoctype="multivolume" ughbinding="true" docstruct="firstchild" metadata="shelfmarksource">Signatur</item> 


- **from**: legt den Ursprung fest. Mögliche Werte sind *werk* für [Werkstückseigenschaften](https://github.com/kitodo/kitodo-production/wiki/Vorgangsdetails---Werkst%C3%BCckeigenschaft) oder *vorlage* als [Vorlageneigenschaft](https://github.com/kitodo/kitodo-production/wiki/Vorgangsdetails---Physische-Vorlagen). 
- **isdoctype / isnotdocptype**: damit kann die Anzeige eines Metadatum für bestimmte Dokumenttypen konfiguriert werden. Zum Beispiel: isdoctype="multivolume" → gilt nur für mehrbändige Werke.
- **ughbindung**: legt fest, ob der Wert in der Datenbank als Werkstück- oder Vorlageneigenschaft gespeichert wird.
- **metadata**: bestimmt das Metadatum aus den [Regelsatz](https://github.com/kitodo/kitodo-production/wiki/Regelsatz-XML-Datei).
- **required**: definiert das Feld als Pflichtfeld, das ausgefüllt sein muss, um den Datensatz speichern zu können.
- **docstruct**: über die möglichen Werte *topstruct* und *firstchild*, wird bestimmt, ob der Wert in das Topelement (Zum Beispiel *Zeitschrift*) oder erste Kindelement (Zum Beispiel *Zeitschriften-Band*) der Struktur gespeichert wird
- **Wert des item Tags**: dient als Anzeigename in der Eingabemaske beim [Anlegen der Vorgänge](https://github.com/kitodo/kitodo-production/wiki/Neuen-Vorgang-anlegen). In diesem Beispiel: Signatur.


Weitere Hinweise:

Soll aus mehreren Werten ausgewählt werden können, so müssen jeweils *select* Tags innerhalb des *item* Tags erstellt werden. Neben den Wert des *select* Tags, der als gespeicherte / genutzter Wert agiert, definiert das *label Attribut* den Anzeigewert:

	<item from="werk" isdoctype="monograph|manuscript|newspaper" required="true" ughbinding="true" docstruct="topstruct" metadata="slub_script">Schrifttyp
		<select label="Antiqua">Antiqua</select>
		<select label="Fraktur">Fraktur</select>
		<select label="keine OCR">keine_OCR</select>
	</item>

