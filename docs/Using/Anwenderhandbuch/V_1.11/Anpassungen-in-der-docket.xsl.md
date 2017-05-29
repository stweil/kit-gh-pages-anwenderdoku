Die Generierung des Laufzettels erfolgt mittels einer .xsl Datei. In unserem Beispiel nennen wir diese docket.xsl. Die docket.xsl beschreibt, wie der generierte [Laufzettel](Laufzettel) aussieht.
## Kerninformationen
Dies sind alle Eigenschaften des Vorgangs, die unter Vorgangsdetails-Vorgang im Frontend zu finden sind. Hier die vollständige Liste:

| Information        | Schlüsselwort
| ------               | -------
| Projektname          | kitodo:project
| Vorgangstitel/PPN    |  kitodo:title
| VorgangsId           |  @processID
| Anlegedatum          |  kitodo:time
| Name des Regelsatzes |  kitodo:ruleset
| Kommentar            |  kitodo:comment
| zugehörige Batches   |  kitodo:batch

Ein einfaches Besipiel, wie der Name des Projektes hinzugefügt wird:

     […] 
     1: <fo:table-row> 
     2:    <fo:table-cell> 
     3:       <fo:block>Projektname:</fo:block> 
     4:    </fo:table-cell> 
     5:    <fo:table-cell> 
     6:       <fo:block> 
     7:          <xsl:value-of select="kitodo:project"/> 
     8:       </fo:block> 
     9:    </fo:table-cell> 
     10: </fo:table-row 
     […]
Zur Darstellung auf dem Laufzettel wird mit kitodo:project (Zeile 7) auf den Projekttitel zugegriffen. Dies funktioniert mit allen bereitgestellten Informationen.

## Tabelleninformationen
Zusätzlich zu diesen Informationen, werden vier Datenbanktabellen ausgelesen:
- Werkstückeingenschaften
- Vorlageneigenschaften
- Vorgangseigenschaften
- Schritte

Auf diese kann mit dem passenden Schlüsselwort zugegriffen werden, der Mechanismus ist immer gleich. Hier die Liste der Tabellen und die zugehörigen Schlüsselwörter:

| Tabelle                 | Schlüsselwort
| -----| -------
| Vorlageneigenschaften    |  kitodo:originals/kitodo:original
| Vorgangseigenschaften    |  ---
| Schritte                 |  kitodo:steps/kitodo:step
| Werkstückeigenschaften   |  kitodo:digitalDocuments/kitodo:digitalDocument

Das Einbinden einer Information aus der Tabelle “Vorlageneigenschaften” geschieht wie folgt:

     […] 
     1: <xsl:for-each select="kitodo:originals/kitodo:original"> 
     2:    <xsl:for-each select="kitodo:properties/kitodo:property"> 
     3:       <xsl:if test="@propertyIdentifier ='Signatur'"> 
     4:          <xsl:value-of select="@value"/> 
     5:       </xsl:if>
     6:    </xsl:for-each> 
     7: </xsl:for-each> 
     […]

Entscheidend dafür, welche Tabelle ausgelesen wird ist hier das Schlüsselwort **kitodo:originals/kitodo:original** (Zeile 1).
Ein weiteres Beispiel, für das Auslesen einer Information aus der Tabelle Werkstückeigenschaften:

     […] 
     1: <xsl:for-each select="kitodo:digitalDocuments/kitodo:digitalDocument "> 
     2:    <xsl:for-each select="kitodo:properties/kitodo:property"> 
     3:       <xsl:if test="@propertyIdentifier ='DocType'"> 
     4:          <xsl:value-of select="@value"/> 
     5:       </xsl:if> 
     6:    </xsl:for-each> 
     7: </xsl:for-each> 
     […]

Mit dem Test „@propertyIdentifier =‘DocType‘“ wähle ich das anzuzeigende Element aus. „docType“ ist hierbei der Wert in der Spalte „title“ der Tabelle, der dazugehörige Wert (Spalte „value“) wird mit @value angesprochen.
Die Inhalte der Tabelle können über die Projekt-XML Datei konfiguriert werden. Eine Erklärung dazu gibt es hier[ Projekt-XML-Datei#erkl%C3%A4rung-zu-den-item-tags].
Die Tabelle „Vorgangseigenschaften“ benötigt kein spezielles Schlüsselwort. Hier kann die äußere for-each Schleife (Zeile 1 + 7) weggelassen werden. Ein Beispiel:

    […] 
    1: <xsl:for-each select="kitodo:properties/kitodo:property"> 
    2:    <xsl:if test="@propertyIdentifier ='digitalCollection'"> 
    3:       <xsl:value-of select="@value"/> 
    4:    </xsl:if> 
    5: </xsl:for-each> 
    […]

**Eine Ausnahme bildet die Tabelle Schritte.**
Hier heißen die Attribute nicht „propertyIdentifier“ und „value“. Es gibt hier folgende Elemente:

| Wert                  |  Schlüsselwort
| ------| ------
| Titel                  |     titel
| SchrittID               |    @stepID
| Bearbeitungsstatus      |    processingstatus
| Bearbeitungsbeginn      |    time (@start time)
| Bearbeitungsende       |     time (@end time)
| Bearbeitungsbenutzer    |    user
| Editierungstyp          |    edittype

Ein Beispiel für die Verwendung einer Information aus der Schritttabelle:

    […]
    1: <xsl:for-each select="kitodo:steps/kitodo:step"> 
    2:    <xsl:value-of select="kitodo:user"/> 
    3: <xsl:for-each>
    […]

Ein weiteres Beispiel für das Auslesen des Bearbeitungsbeginns: 

    […]
    1: <xsl:for-each select="kitodo:steps/kitodo:step"> 
    2:    <xsl:for-each select="kitodo:time"> 
    3:       <xsl:if test="@type ='start time'"> 
    4:          <xsl:value-of select="kitodo:time"/> 
    5:       </xsl:if> 
    6:    </xsl:for-each> 
    7: </xsl:for-each>
    […]

## Erzeugen eines Barcodes
Das Erzeugen eines Barcodes funktioniert wie folgt:

    […] 
    1: <xsl:variable select="kitodo:title" name="barcode1"/> 
    2: <fo:block text-align="center"> 
    3:    <fo:instream-foreign-object> 
    4:       <barcode:barcode message="{$barcode1}"xmlns:barcode="http://barcode4j.krysalis.org/ns"> 
    5:          <barcode:code128> 
    6:             <barcode:module-width>0.21mm</barcode:module-width> 
    7:             <barcode:height>20mm</barcode:height> 
    8:          </barcode:code128> 
    9:       </barcode:barcode> 
    10:   </fo:instream-foreign-object> 
    11: </fo:block> 
    […]

Die im Barcode anzuzeigende Information wird in Zeile 1 gesetzt select="kitodo:title" Es werden alle Zeichen des US-ASCII Codes zur Barcodegenerierung unterstützt. Diese sind:

!"#$%&'()*+,-./0123456789:;<=>?
@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_
`abcdefghijklmnopqrstuvwxyz{|}~

Dies bedeutet insbesondere keine Umlaute, sowie kein ß. Es muss also darauf geachtet werden, welche Informationen in den Barcode geschrieben werden, da sonst die Generierung des Laufzettels fehlschlägt.