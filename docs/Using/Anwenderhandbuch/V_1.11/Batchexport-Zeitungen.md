# Einleitung 
Um die korrekte Präsentation der Zeitungsausgaben zu ermöglichen, müssen alle Ausgaben einer Zeitung in einem Batch exportiert werden. Nur in diesem Fall werden in den drei Metadaten-Dateien Referenzierungen zueinander eingetragen: 

- *[Beispiel]*.xml
- *[Beispiel]*_anchor.xml
- *[Beispiel]*_year.xml

*Anhang: Beispiele* enthält Bereiche der METS-Dateien


In der SLUB werden die Zeitungsvorgänge zunächst durch den automatischen Export exportiert. 

Erst wenn alle Ausgaben eines Titels oder eine zuvor definierte Anzahl von Ausgaben automatisch exportiert wurden, wird der Batch-Export ausgelöst. 

# Ablauf
Auf dieser Seite wird der Ablauf in der SLUB dokumentiert. Dort werden die Zeitungsausgaben zuerst über den automatischen Export exportiert. Danach werden die ausgewählten Vorgänge in einem Batch-Vorgang exportiert. 

## Automatischer Export
Zunächst werden alle Vorgänge bearbeitet und automatisch exportiert. Somit muss der bisherige Workflow nicht geändert werden. 

Erst im Nachhinein werden alle Ausgaben, oder eine zuvor definierte Anzahl von Ausgaben per Batch-Export exportiert

## Batch-Export
Wenn alle oder eine bestimme Menge an Ausgaben exportiert wurden, kann der Batch-Export durchgeführt werden:

1. Zunächst wird eine der beiden folgenden Funktionen ausgeführt . Dies hängt davon ab, ob schon ein Batch existiert oder nicht.
	- *[Neuen Batch aus den gewählten Vorgängen erzeugen](Batches#neuen-batch-aus-den-gew%C3%A4hlten-vorg%C3%A4ngen-erzeugen)*
	- *[Selektierte Vorgänge zu ausgewähltem Batch hinzufügen](Batches#selektierte-vorg%C3%A4nge-zu-ausgew%C3%A4hltem-batch-hinzuf%C3%BCgen)*
2. Dann wird der Typ des Batchs geändert zu Zeitung
	- *[Typ setzen: Logistik, Zeitung, fortlaufendes Sammelwerk](Batches#typ-setzen-logistik-zeitung-fortlaufendes-sammelwerk)*
3. Dann wird der Batch mit allen Ausgaben exportiert
	- *[Gesamten Batch ins DMS exportieren](Batches#gesamten-batch-ins-dms-exportieren)*

**ACHTUNG**: In dem Batch-Modul lassen sich die Vorgänge nicht nach Bearbeitungsstand filtern. Es muss also zuvor ermittelt werden, welche Vorgänge eines Titels schon exportiert wurden. Nur diese Vorgänge dürfen dann in einem Batch zusammengefasst und exportiert werden. 

Ansonsten besteht die Gefahr, dass invalide (fehlende Images oder Metadaten) Vorgänge exportiert werden, die unnötig Fehler und Aufwände verursachen. 



## Nachträgliche Exporte

**ACHTUNG**: Wenn ein Vorgang nachträglich korrigiert und "normal" exportiert (auch Export ohne Images) wird, werden die "Batch-Metadaten-Dateien" überschrieben. Das bedeutet, dass nach jedem nachträglichen "normalen" Export nochmal ein "Batch-Export" mit allen zugehörigen und abgeschlossenen Vorgängen durchgeführt werden muss. 

Dieser Batch-Export muss mit allem zu dem Titel gehörigen Ausgaben durchgeführt werden. 



# Anhang: Beispiele

## *[Beispiel]*_anchor.xml
In der *[Beispiel]*_anchor.xml-Datei werden zum Beispiel in mets:structMap TYPE="LOGICAL" Verweise auf die year.xml-Dateien der im Batch enhaltenen Jahre eingetragen. Zum Beispiel: *LABEL="1822" TYPE="year"*

---
```
<mets:div DMDID="DMDLOG_0001" ID="LOG_0001" LABEL="1822" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220101/ArtiNo_425390144-18220101_year.xml"/>
</mets:div>
<mets:div DMDID="DMDLOG_0002" ID="LOG_0002" LABEL="1823" ORDERLABEL="1823" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18230118/ArtiNo_425390144-18230118_year.xml"/>
</mets:div>
<mets:div DMDID="DMDLOG_0003" ID="LOG_0003" LABEL="1824" ORDERLABEL="1824" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-1824063001/ArtiNo_425390144-1824063001_year.xml"/>
</mets:div>
<mets:div DMDID="DMDLOG_0004" ID="LOG_0004" LABEL="1825" ORDERLABEL="1825" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18250915/ArtiNo_425390144-18250915_year.xml"/>
</mets:div>
<mets:div DMDID="DMDLOG_0005" ID="LOG_0005" LABEL="1826" ORDERLABEL="1826" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18260731/ArtiNo_425390144-18260731_year.xml"/>
</mets:div>
<mets:div DMDID="DMDLOG_0006" ID="LOG_0006" LABEL="1830" ORDERLABEL="1830" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18300605/ArtiNo_425390144-18300605_year.xml"/>
</mets:div>
<mets:div DMDID="DMDLOG_0007" ID="LOG_0007" LABEL="1831" ORDERLABEL="1831" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18310326/ArtiNo_425390144-18310326_year.xml"/>
</mets:div>
<mets:div DMDID="DMDLOG_0008" ID="LOG_0008" LABEL="1832" ORDERLABEL="1832" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18321018/ArtiNo_425390144-18321018_year.xml"/>
</mets:div>
<mets:div DMDID="DMDLOG_0009" ID="LOG_0009" LABEL="1833" ORDERLABEL="1833" TYPE="year">
	<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18331102/ArtiNo_425390144-18331102_year.xml"/>
</mets:div>
```
---


## *[Beispiel]*_year.xml

In der *[Beispiel]*year.xml-Datei werden zum Beispiel in mets:structMap TYPE="LOGICAL" Verweise auf die xml-Dateien der im Batch enhaltenen Ausgaben eingetragen.
Unter einem Monat werden alle Tage des Monats aufgeführt. Zum Beispiel *ORDERLABEL="1" TYPE="month"* (Monat), *ORDERLABEL="7" TYPE="day"* (Tag).

---
```
<mets:structMap TYPE="LOGICAL">
	<mets:div CONTENTIDS="http://digital.slub-dresden.de/idArtiNo_425390144-18220101" DMDID="DMDLOG_0010" ID="LOG_0010" LABEL="Artistisches Notizenblatt" ORDERLABEL="Artistisches Notizenblatt" TYPE="newspaper">
		<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220101/ArtiNo_425390144-18220101_anchor.xml"/>
	<mets:div ADMID="AMD" DMDID="DMDLOG_0011" ID="LOG_0011" LABEL="1822" TYPE="year">
		<mets:div ADMID="AMD" DMDID="DMDLOG_0012" ID="LOG_0012" ORDERLABEL="1" TYPE="month">
			<mets:div ADMID="AMD" ID="LOG_0013" ORDERLABEL="1" TYPE="day">
				<mets:div ID="LOG_0014" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220101/ArtiNo_425390144-18220101.xml"/>
				</mets:div>
			</mets:div>
			<mets:div ADMID="AMD" ID="LOG_0015" ORDERLABEL="17" TYPE="day">
				<mets:div ID="LOG_0016" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220117/ArtiNo_425390144-18220117.xml"/>
				</mets:div>
			</mets:div>
		</mets:div>
		<mets:div ADMID="AMD" DMDID="DMDLOG_0015" ID="LOG_0017" ORDERLABEL="2" TYPE="month">
			<mets:div ADMID="AMD" ID="LOG_0018" ORDERLABEL="7" TYPE="day">
				<mets:div ID="LOG_0019" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220204/ArtiNo_425390144-18220204.xml"/>
				</mets:div>
			</mets:div>
			<mets:div ADMID="AMD" ID="LOG_0020" ORDERLABEL="23" TYPE="day">
				<mets:div ID="LOG_0021" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220223/ArtiNo_425390144-18220223.xml"/>
				</mets:div>
			</mets:div>
		</mets:div>
		<mets:div ADMID="AMD" DMDID="DMDLOG_0018" ID="LOG_0022" ORDERLABEL="3" TYPE="month">
			<mets:div ADMID="AMD" ID="LOG_0023" ORDERLABEL="6" TYPE="day">
				<mets:div ID="LOG_0024" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220306/ArtiNo_425390144-18220306.xml"/>
				</mets:div>
			</mets:div>
			<mets:div ADMID="AMD" ID="LOG_0025" ORDERLABEL="30" TYPE="day">
				<mets:div ID="LOG_0026" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220330/ArtiNo_425390144-18220330.xml"/>
				</mets:div>
			</mets:div>
		</mets:div>
		<mets:div ADMID="AMD" DMDID="DMDLOG_0021" ID="LOG_0027" ORDERLABEL="4" TYPE="month">
			<mets:div ADMID="AMD" ID="LOG_0028" ORDERLABEL="10" TYPE="day">
				<mets:div ID="LOG_0029" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220410/ArtiNo_425390144-18220410.xml"/>
				</mets:div>
			</mets:div>
			<mets:div ADMID="AMD" ID="LOG_0030" ORDERLABEL="27" TYPE="day">
				<mets:div ID="LOG_0031" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220427/ArtiNo_425390144-18220427.xml"/>
				</mets:div>
			</mets:div>
		</mets:div>
		<mets:div ADMID="AMD" DMDID="DMDLOG_0024" ID="LOG_0032" ORDERLABEL="5" TYPE="month">
			<mets:div ADMID="AMD" ID="LOG_0033" ORDERLABEL="22" TYPE="day">
				<mets:div ID="LOG_0034" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220522/ArtiNo_425390144-18220522.xml"/>
				</mets:div>
			</mets:div>
			<mets:div ADMID="AMD" ID="LOG_0035" ORDERLABEL="31" TYPE="day">
				<mets:div ID="LOG_0036" TYPE="issue">
					<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220531/ArtiNo_425390144-18220531.xml"/>
				</mets:div>
			</mets:div>
		</mets:div>
	</mets:div>
	</mets:div>
</mets:structMap>
```
---



## *[Beispiel]*.xml

In der *[Beispiel]*.xml-Datei werden zum Beispiel in mets:structMap TYPE="LOGICAL" Verweise auf die zugehörige anchor.xml-Datei und die übergeordnete year.xml-Datei eingetragen.
Zudem enthält sie Informationen zu Tag und Monat des Erscheinungsdatums.

---
```
<mets:structMap TYPE="LOGICAL">
	<mets:div CONTENTIDS="http://digital.slub-dresden.de/idArtiNo_425390144-18220101" ID="LOG_0072" LABEL="Artistisches Notizenblatt" ORDERLABEL="Artistisches Notizenblatt" TYPE="newspaper">
		<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220101/ArtiNo_425390144-18220101_anchor.xml"/>
		<mets:div ADMID="AMD" ID="LOG_0073" LABEL="1822" TYPE="year">
			<mets:mptr LOCTYPE="URL" xlink:href="http://digital.slub-dresden.de/fileadmin/data/ArtiNo_425390144-18220101/ArtiNo_425390144-18220101_year.xml"/>
			<mets:div ADMID="AMD" ID="LOG_0074" ORDERLABEL="1" TYPE="month">
				<mets:div ADMID="AMD" ID="LOG_0075" ORDERLABEL="1" TYPE="day">
					<mets:div ADMID="AMD" DMDID="DMDLOG_0048" ID="LOG_0076" TYPE="issue"/>
				</mets:div>
			</mets:div>
		</mets:div>
	</mets:div>
</mets:structMap>
```
---
