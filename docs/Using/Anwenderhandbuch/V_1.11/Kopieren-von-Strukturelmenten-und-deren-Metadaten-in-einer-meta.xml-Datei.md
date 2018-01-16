# Einleitung 
Es ist in Kitodo.Production möglich, Meta- und Strukturdaten direkt in der XML-Datei zu bearbeiten. Ein Anwendungsfall ist das Kopieren der Struktur-und Metadaten von Vorgängen gleichen oder ähnlichen Inhalts. Wenn Digitalisate eine ähnliche und umfangreiche Struktur aufweisen, ist es sehr zeitintensiv, die Strukturen anzulegen und diese mit Metadaten auszuzeichnen. Eine Möglichkeit, das manuelle Anlegen zu umgehen, ist das Kopieren der Inhalte direkt in der meta.xml-Datei. 

Diese Manipulation muss äußerst sorgfältig durchgeführt werden, da die Datei bei fehlerhaftem Kopieren invalide und somit unbrauchbar wird. Um Fehler zu vermeiden, wird zunächst die Struktur der Datei erläutert, danach werden die Bereiche benannt, die kopiert werden. 

# Struktur der meta.xml-Datei
Die Datei entspricht dem METS-Standard, jedoch handelt sich um ein Kitodo-internes Format und nicht um die Datei, die nach dem Export erstellt und archiviert wird. 

Bevor die meta.xml-Datei manipuliert wird, muss deren Struktur klar worden sein. Sie besteht aus folgenden Teilen: 

- Deskriptive Metadaten 
  - Titel-Metadaten
  - Metadaten der Strukturelemente
  - Path Image Files 
- Links zu den tif-Dateien 
- Strukturelemente
- Paginierung
- Links 

## Deskriptive Metadaten `<dmdSec>`
Weitere Informationen zur `<dmdSec>` finden sich unter: http://www.loc.gov/standards/mets/METSOverview.v2.html#filegrp

### Titel-Metadaten

In diesem Bereich werden die deskriptiven Titelmetadaten der Vorlage (Monografie, Zeitschriften-Band, ...) gespeichert. Das Element ist als `DMDLOG_0001` bezeichnet. 

Beispiel: 

```
<mets:dmdSec ID="DMDLOG_0001">
	<mets:mdWrap MDTYPE="MODS">
		<mets:xmlData>
			<mods:mods >
				<mods:extension>
					<goobi:goobi">
						<goobi:metadata name="CatalogIDDigital">20052145Z</goobi:metadata>
						<goobi:metadata anchorId="true" name="CatalogIDDigital">349689334</goobi:metadata>
						<goobi:metadata name="CurrentNo">43.1900</goobi:metadata>
						<goobi:metadata name="CurrentNoSorting">1900</goobi:metadata>
						<goobi:metadata name="PublicationYear">1900</goobi:metadata>
						<goobi:metadata name="singleDigCollection">Saxonica</goobi:metadata>
						<goobi:metadata name="singleDigCollection">Projekt: Sächsische Adressbücher</goobi:metadata>
						<goobi:metadata name="shelfmarksource">Hist.Sax.H.929-1900</goobi:metadata>
					</goobi:goobi>
				</mods:extension>
			</mods:mods>
		</mets:xmlData>
	</mets:mdWrap>
</mets:dmdSec>
```

### Metadaten der Strukturelemente
In diesem Element werden die deskriptiven Metadaten (Monografie, Zeitschriften-Band, ...) gespeichert, die im [Metadateneditor](https://github.com/kitodo/kitodo-production/wiki/Metadateneditor---Allgemeines) eingegeben wurden. 

Das Element ist als `DMDLOG_0002`, `DMDLOG_0003`, `DMDLOG_0004`, ... bezeichnet. 

Beispiel: 

```
<mets:dmdSec ID="DMDLOG_0002">
	<mets:mdWrap MDTYPE="MODS">
		<mets:xmlData>
			<mods:mods>
				<mods:extension>
					<goobi:goobi>
						<goobi:metadata name="TitleDocMain">Inhalts-Verzeichnis</goobi:metadata>
					</goobi:goobi>
				</mods:extension>
			</mods:mods>
		</mets:xmlData>
	</mets:mdWrap>
</mets:dmdSec>
<mets:dmdSec ID="DMDLOG_0003">
…
<mets:dmdSec ID="DMDLOG_0085">
	<mets:mdWrap MDTYPE="MODS">
		<mets:xmlData>
			<mods:mods>
				<mods:extension>
					<goobi:goobi>
						<goobi:metadata name="TitleDocMain">Thalia-Theater zu Chemnitz</goobi:metadata>
						<goobi:metadata name="slub_Place">Chemnitz</goobi:metadata>
						<goobi:metadata name="slub_PlaceSWDID">4029702-0</goobi:metadata>
					</goobi:goobi>
				</mods:extension>
			</mods:mods>
		</mets:xmlData>
	</mets:mdWrap>
</mets:dmdSec> 
```

### Path Image Files
Dieser Bereich enthält den Pfad zu dem Speicherort der Images.

Das Element ist als `DMDPHYS_0000` bezeichnet. 

Beispiel: 

```
<mets:dmdSec ID="DMDPHYS_0000">
	<mets:mdWrap MDTYPE="MODS">
		<mets:xmlData>
			<mods:mods>
				<mods:extension>
					<goobi:goobi>
						<goobi:metadata name="pathimagefiles">
						file:///home/goobi/work/daten/37571/images/adredefau_20052145Z_1900_tif
						</goobi:metadata>
					</goobi:goobi>
				</mods:extension>
			</mods:mods>
		</mets:xmlData>
	</mets:mdWrap>
</mets:dmdSec>
```

## Links zu den tif-Dateien `<fileSec>`
Dieser Bereich enthält die Pfade zu den einzelnen Images. 

Weitere Informationen zur `<fileSec>` finden sich unter: http://www.loc.gov/standards/mets/METSOverview.v2.html#filegrp

Beispiel: 

```
<mets:fileSec>
	<mets:fileGrp USE="LOCAL">
		<mets:file ID="FILE_0000" MIMETYPE="image/tiff">
			<mets:FLocat LOCTYPE="URL" xlink:href="file:///home/goobi/work/daten/37571/images/scans_tif/00000001.tif"/>
		</mets:file>
		…
		<mets:file ID="FILE_1583" MIMETYPE="image/tiff">
			<mets:FLocat LOCTYPE="URL" xlink:href="file:///home/goobi/work/daten/37571/images/scans_tif/00001350.tif"/>
		</mets:file>
	</mets:fileGrp>
</mets:fileSec>
```

## Strukturelemente `<structMap> / TYPE=LOGICAL`
Dieser Bereich enthält die erstellten Strukturelemente des Vorgangs. Sie werden in einer Baumstruktur dargestellt, so dass Kindelemente "geschachtelt" werden.  

Weitere Informationen zur `<structMap>` finden sich unter: http://www.loc.gov/standards/mets/METSOverview.v2.html#structmap

Beispiel: 

```
<mets:structMap TYPE="LOGICAL">
	<mets:div ID="LOG_0002" TYPE="Periodical">
		<mets:mptr LOCTYPE="URL" xlink:href="" xmlns:xlink="http://www.w3.org/1999/xlink"/>
		<mets:div DMDID="DMDLOG_0001" ID="LOG_0003" TYPE="PeriodicalVolume">
			<mets:div ID="LOG_0004" TYPE="TitlePage"/>
			<mets:div DMDID="DMDLOG_0002" ID="LOG_0005" TYPE="TableOfContents"/>
			... 
			<mets:div DMDID="DMDLOG_0079" ID="LOG_0082" TYPE="PeriodicalPart">
				<mets:div DMDID="DMDLOG_0080" ID="LOG_0083" TYPE="OtherDocStrct"/>
				<mets:div DMDID="DMDLOG_0081" ID="LOG_0084" TYPE="OtherDocStrct"/>
			...
			<mets:div DMDID="DMDLOG_0085" ID="LOG_0088" TYPE="PeriodicalPart"/>
		</mets:div>
	</mets:div>
</mets:structMap>
```

## Paginierung `<structMap> / TYPE=PHYSICAL`
Dieser Bereich enthält die Informationen zur Paginierung der einzelnen Images. 

Weitere Informationen zur `<structMap>` finden sich unter: http://www.loc.gov/standards/mets/METSOverview.v2.html#structmap

Beispiel: 

```
<mets:structMap TYPE="PHYSICAL">
	<mets:div DMDID="DMDPHYS_0000" ID="PHYS_0000" TYPE="BoundBook">
		<mets:div ID="PHYS_0001" ORDER="1" ORDERLABEL="uncounted" TYPE="page">
			<mets:fptr FILEID="FILE_0000"/>
		</mets:div>
		<mets:div ID="PHYS_0002" ORDER="2" ORDERLABEL="uncounted" TYPE="page">
			<mets:fptr FILEID="FILE_0001"/>
		</mets:div>
		...
		<mets:div ID="PHYS_0030" ORDER="30" ORDERLABEL="XXVI" TYPE="page">
			<mets:fptr FILEID="FILE_0029"/>
		</mets:div>
		...
		<mets:div ID="PHYS_0578" ORDER="578" ORDERLABEL="544" TYPE="page">
			<mets:fptr FILEID="FILE_0577"/>
		</mets:div>
		...
		<mets:div ID="PHYS_1350" ORDER="1350" ORDERLABEL="uncounted" TYPE="page">
			<mets:fptr FILEID="FILE_1349"/>
		</mets:div>
	</mets:div>
</mets:structMap>
```

## Links `<structLink>`

Dieser Bereich enthält die Informationen darüber, welche Images zu welchen Strukturelementen gehören. 

Weitere Informationen zur `<structLink>` finden sich unter: http://www.loc.gov/standards/mets/METSOverview.v2.html#structlink

Beispiel: 

```
<mets:structLink>
	<mets:smLink xlink:to="PHYS_0001" xlink:from="LOG_0003"/>
	<mets:smLink xlink:to="PHYS_0002" xlink:from="LOG_0003"/>
	<mets:smLink xlink:to="PHYS_1347" xlink:from="LOG_0087"/>
	<mets:smLink xlink:to="PHYS_1347" xlink:from="LOG_0088"/>
</mets:structLink>
```

# Zulässige Änderungen 
Wenn Strukturelemente und deren Metadaten kopiert werden sollen, werden Änderungen an zwei Stellen vorgenommen: 

- [Metadaten der Strukturelemente](https://github.com/kitodo/kitodo-production/wiki/Kopieren-von-Strukturelmenten-und-Metadaten-in-einer-meta.xml-Datei#metadaten-der-strukturelemente) `DMDLOG_0002`, `DMDLOG_0003`, `DMDLOG_0004`, ... 
- [Strukturelemente](https://github.com/kitodo/kitodo-production/wiki/Kopieren-von-Strukturelmenten-und-Metadaten-in-einer-meta.xml-Datei#strukturelemente-structmap--typelogical)
 `<structMap> / LOGICAL` 

Alle anderen Elemente (Paginierung, ...) sollten **nicht** verändert werden, da diese in der Regel in jedem Band voneinader abweichen. 

Beim Kopieren und Einfügen muss zudem darauf geachtet werden, dass bestehende Elemente korrekt überschrieben werden. 
