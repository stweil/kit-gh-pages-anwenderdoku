# Aktualisierungshinweise auf Kitodo.Production 2.1.0

## Änderungen an der goobi_config.properties Datei

- Es ist die Option `advancedPaginationEnabled` mit dem Wert `true` hinzugekommen, so dass die erweiterten Paginierungsmöglichkeiten angezeigt werden
- Für die Unterstützung des RDA Imports sind diverse `namespace.*` und `authority*` Einträge hinzugekommen

## Änderungen an der goobi_opac.xml Datei

### Dynamische Suchterme

Es wurden Änderungen vorgenommen, dass die Suchterme in den genutzten OPACs nicht mehr fest kodiert sondern frei definiert sind. Daher müssen bei den genutzten OPACs die Suchterme hingefügt werden.

1) Am Beispiel des GBVs:

alter Eintrag:
```
<catalogue title="GBV">
    <config address="gso.gbv.de" database="2.1" description="Gemeinsamer Bibliotheksverbund" iktlist="IKTLIST-GBV.xml" port="80" ucnf="UCNF=NFC" />
</catalogue>
```

neuer Eintrag:
```
<catalogue title="GBV">
    <config address="gso.gbv.de" database="2.1" description="Gemeinsamer Bibliotheksverbund" port="80" ucnf="UCNF=NFC" />
    <searchFields>
        <searchField label="Title" value="4" />
        <searchField label="Identifier" value="12" />
        <searchField label="ISBN" value="7" />
        <searchField label="ISSN" value="8" />
        <searchField label="Barcode" value="8535" />
        <searchField label="Barcode 8200" value="8200" />
    </searchFields>
</catalogue>
```

2) Am Beispiel der ZDB:

alter Einrag:
```
<catalogue title="ZDB">
    <config address="dispatch.opac.d-nb.de" database="1.1" description="Zeitschriftendatenbank (ZDB)" iktlist="IKTLIST-ZDB.xml" port="80" />
</catalogue>
```

neuer Eintrag:
```
<catalogue title="ZDB">
    <config address="dispatch.opac.d-nb.de" database="1.1" description="Zeitschriftendatenbank (ZDB)" port="80" />
    <searchFields>
        <searchField label="Title" value="4" />
        <searchField label="Identifier" value="12" />
        <searchField label="ISBN" value="7" />
        <searchField label="ISSN" value="8" />
        <searchField label="Barcode" value="8535" />
        <searchField label="Barcode 8200" value="8200" />
        <searchField label="ZDB-ID" value="8506" />
    </searchFields>
</catalogue>

```
### Auflösungsregeln

Für den Import von Normdaten über RDA können nun `resolve` Regeln definiert werden. Eine Erklärung dazu befindet sich in der `goobi_opac.xml`

### Weitere Änderungen

Im Zuge der Aufräumarbeiten für das 2.1.0 Release wurden die nicht genutzten `iktlist` Attribute aus der `goobi_opac.xml` entfernt.

## Neues Plugin: ModsPlugin

- Durch die Unterstützung des Imports von MODS Daten aus SRU basierenden Katalogen, ist das OPAC Plugin `ModsPlugin.jar` dazu gekommen. Damit man dieses genutzt werden kann, muss es wie das PicaPlugin aus dem `plugin/opac` Unterverzeichnis der deployten Kitodo Anwendung im Tomcat in das Unterverzeichnis `opac` des in `goobi_config.properties` angegebenen `pluginFolder` kopieren oder unter Beibehaltung des Namens zu verlinken oder kopiert werden.

- Die Konfigurationsdatei `kitodo_mods_opac.xml` für die Konfiguration des genutzten MODS-SRU-Schnittstelle muss aus dem `WEB-INF/classes` Verzeichnis der deployten Kitodo Anwendung ins `KonfigurationsVerzeichnis` angegebene Verzeichnis aus der `goobi_config.properties` Datei kopiert und ggf. angepasst oder erweitert werden.

- Die Konfigurationsdatei `kalliope2kitodo.xsl` für die Konfiguration des Datenmappings aus MODS-SRU ins Kitodo interne Datenformat uss aus dem `WEB-INF/classes` Verzeichnis der deployten Kitodo Anwendung ins `xsltFolder` angegebene Verzeichnis aus der `goobi_config.properties` Datei kopiert und ggf. angepasst oder erweitert werden.

------

# Aktualisierungshinweise auf Kitodo.Production 2.0.0

Im Release von Kitodo.Production 2.0.0 wurden die dynamisch erzeugten Datenbank-Indizes durch fest vordefinierte Namen ersetzt.

Wird auf Kitodo.Production 2.0.0 von einer länger laufenden Goobi.Production Instanz (vor und inklusive Version 1.11.2) aktualisiert, benötigt man die folgenden SQL Migrationsdateien:

- [remove_old_index_prior_1.11.2.sql](https://github.com/kitodo/kitodo-production/tree/kitodo-production-2.0.0/Goobi/setup/migrate_index/remove_old_index_prior_1.11.2.sql)
- [remove_old_index_1.11.2.sql](https://github.com/kitodo/kitodo-production/tree/kitodo-production-2.0.0/Goobi/setup/migrate_index/remove_old_index_1.11.2.sql)
- [add_new_index_2.0.0.sql](https://github.com/kitodo/kitodo-production/tree/kitodo-production-2.0.0/Goobi/setup/migrate_index/add_new_index_2.0.0.sql)

Diese sollte vor dem ersten Start der Anwendung in die Datenbank eingespielt werden:

- mysql -h `database host` -u `user` -p `database` < remove_old_index_prior_1.11.2.sql
- mysql -h `database host` -u `user` -p `database` < remove_old_index_1.11.2.sql
- mysql -h `database host` -u `user` -p `database` < add_new_index_2.0.0.sql

Wird auf Kitodo.Production 2.0.0 aktualisiert und vorher wurde nur die Version Goobi.Production 1.11.2 eingesetzt, dann benötigt man die folgenden SQL Migrationsdateien:

- [remove_old_index_1.11.2.sql](https://github.com/kitodo/kitodo-production/tree/kitodo-production-2.0.0/Goobi/setup/migrate_index/remove_old_index_1.11.2.sql)
- [add_new_index_2.0.0.sql](https://github.com/kitodo/kitodo-production/tree/kitodo-production-2.0.0/Goobi/setup/migrate_index/add_new_index_2.0.0.sql)

Diese sollten vor dem ersten Start der Anwendung in die Datenbank eingespielt werden:

- mysql -h `database host` -u `user` -p `database` < remove_old_index_1.11.2.sql
- mysql -h `database host` -u `user` -p `database` < add_new_index_2.0.0.sql

Bei einigen Installationen funktionieren die obigen SQL-Dateien aufgrund bestehender Fremdschlüsseleinschränkungen möglicherweise nicht. In diesem Fall müssen Sie vor dem Ausführen der obigen Zeilen, abhängig von Ihrer aktuellen Version, einen der folgenden Befehle ausführen:

- mysql -h `database host` -u `user` -p `database` < remove_old_foreign_keys_prior_1.11.2.sql
- mysql -h `database host` -u `user` -p `database` < remove_old_foreign_keys_1.11.2.sql

Sie müssen `database host`, `user` und `database` mit den genutzten Einstellungen ersetzen. Der Benutzer `user` muss die Berechtigung haben, die Datenbankstruktur der genutzten Datenbank zu ändern.

- [remove_old_foreign_keys_prior_1.11.2.sql](https://github.com/kitodo/kitodo-production/tree/2.x/Goobi/setup/migrate_index/remove_old_foreign_keys_prior_1.11.2.sql)
- [remove_old_foreign_keys_1.11.2.sql](https://github.com/kitodo/kitodo-production/tree/2.x/Goobi/setup/migrate_index/remove_old_foreign_keys_1.11.2.sql)
