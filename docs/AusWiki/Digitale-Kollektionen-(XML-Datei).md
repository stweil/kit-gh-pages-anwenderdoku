Um [Digitale Kollektionen](https://github.com/kitodo/kitodo-production/wiki/Digitale-Kollektionen) vergeben zu können, müssen diese in einer Datei *goobi_digitalCollections.xml* (https://github.com/kitodo/kitodo-production/tree/1.11.x/Goobi/config) verzeichnet werden. Die Datei befindet sich laut [Installationsanleitung](https://github.com/kitodo/kitodo-production/wiki/Installationsanleitung-f%C3%BCr-Goobi.Production-CE-1.10) im Konfigurations-Verzeichnis.

Es ist möglich, die Digitalen Kollektionen projektspezifisch zu vergeben (in jedem [Projekt](https://github.com/kitodo/kitodo-production/wiki/Projekt) werden spezifische Kollektionen angeboten), jedoch ist dies nur sinnvoll, wenn viele Kollektionen verwendet werden. Außerdem sollten nachträgliche Änderungen der Kollektionsnamen in der Datei vermieden werden, da diese Änderungen KEINE Auswirkung auf den Kollektionsnamen in bestehenden Vorgängen hat. 

Wenn beim Anlegen aller Vorgänge alle Digitalen Kollektionen auswählbar sein sollen, sieht es so aus:

    <?xml version="1.0" encoding="UTF-8"?>
        <DigitalCollections>
            <default>
                <DigitalCollection>Bestandsschutz digitaler Objekte</DigitalCollection>
                <DigitalCollection>Drucke des 15. Jahrhunderts</DigitalCollection>
                <DigitalCollection>Drucke des 16. Jahrhunderts</DigitalCollection>
                <DigitalCollection>Drucke des 17. Jahrhunderts</DigitalCollection>
                <DigitalCollection>Drucke des 18. Jahrhunderts</DigitalCollection>
                [...]
                <DigitalCollection>Projekt: Uhrmacher-Zeitschriften</DigitalCollection>
                <DigitalCollection>Sammlung Fürsten- und Landesschule Grimma</DigitalCollection>
                <DigitalCollection>Saxonica</DigitalCollection>
                <DigitalCollection>Staatliche Kunstsammlungen Dresden</DigitalCollection>
                <DigitalCollection>Stenografische Sammlung</DigitalCollection>
                <DigitalCollection>Technikgeschichte</DigitalCollection>
                <DigitalCollection>Varia</DigitalCollection>
                <DigitalCollection>Virtuelle Schatzkammer</DigitalCollection>
                <DigitalCollection>Wissenschaftsgeschichte</DigitalCollection>
                <DigitalCollection>Zeitgenössische Kunst</DigitalCollection>
                <DigitalCollection>Zeitungen</DigitalCollection>
            </default>
            [...] 


Wenn die Digitalen Kollektionen projektspezifisch angezeigt werden sollen, sieht es so aus:

    <?xml version="1.0" encoding="UTF-8"?>
    <DigitalCollections>
        <!-- projektunspezifische Kollektion -->
        <default>
            <DigitalCollection>Bestandsschutz digitaler Objekte</DigitalCollection>
            <DigitalCollection>Drucke des 15. Jahrhunderts</DigitalCollection>
            <DigitalCollection>Drucke des 16. Jahrhunderts</DigitalCollection>
            <DigitalCollection>Drucke des 17. Jahrhunderts</DigitalCollection>
            <DigitalCollection>Drucke des 18. Jahrhunderts</DigitalCollection>
            [...]
            <DigitalCollection>Projekt: Uhrmacher-Zeitschriften</DigitalCollection>
            <DigitalCollection>Sammlung Fürsten- und Landesschule Grimma</DigitalCollection>
            <DigitalCollection>Saxonica</DigitalCollection>
            <DigitalCollection>Staatliche Kunstsammlungen Dresden</DigitalCollection>
            <DigitalCollection>Stenografische Sammlung</DigitalCollection>
            <DigitalCollection>Technikgeschichte</DigitalCollection>
            <DigitalCollection>Varia</DigitalCollection>
            <DigitalCollection>Virtuelle Schatzkammer</DigitalCollection>
            <DigitalCollection>Wissenschaftsgeschichte</DigitalCollection>
            <DigitalCollection>Zeitgenössische Kunst</DigitalCollection>
            <DigitalCollection>Zeitungen</DigitalCollection>
        </default>
        <!-- projektspezifische Kollektionen-->
        <project>
            <name>Adressbücher</name>
            <DigitalCollection>Bestandsschutz digitaler Objekte</DigitalCollection>
            <DigitalCollection>Drucke des 18. Jahrhunderts</DigitalCollection>
            <DigitalCollection>Projekt: Dresdner Adressbücher</DigitalCollection>
            <DigitalCollection>Projekt: Sächsische Adressbücher</DigitalCollection>
            <DigitalCollection>Saxonica</DigitalCollection>
        </project>
        <project>
            <name>DigislubM</name>
            <name>DigislubM_OCR</name>
            <name>DigislubZ</name>
            <name>DigislubZ_OCR</name>
            <DigitalCollection>Bestandsschutz digitaler Objekte</DigitalCollection>
            <DigitalCollection>Drucke des 15. Jahrhunderts</DigitalCollection>
            <DigitalCollection>Drucke des 16. Jahrhunderts</DigitalCollection>
            <DigitalCollection>Drucke des 17. Jahrhunderts</DigitalCollection>
            <DigitalCollection>Drucke des 18. Jahrhunderts</DigitalCollection>
            <DigitalCollection>Kunst</DigitalCollection>
            <DigitalCollection>Musik</DigitalCollection>
            <DigitalCollection>Saxonica</DigitalCollection>
            <DigitalCollection>Technikgeschichte</DigitalCollection>
            <DigitalCollection>Varia</DigitalCollection>
        </project>
        <project>
            <name>Digitalisierte_Zettelkataloge</name>
            <DigitalCollection>Projekt: Digitalisierte Zettelkataloge</DigitalCollection>
        </project>
    </DigitalCollections>


Im [Metadateneditor](https://github.com/kitodo/kitodo-production/wiki/Metadateneditor---Allgemeines) können für jedes Projekt weiterhin alle Digitalen Kollektionen vergeben werden können. Das Ziel der projektabhängigen Kollektionsvergabe ist eine überschaubare Liste an Digitalen Kollektionen beim [Anlegen der Vorgänge](https://github.com/kitodo/kitodo-production/wiki/Neuen-Vorgang-anlegen).