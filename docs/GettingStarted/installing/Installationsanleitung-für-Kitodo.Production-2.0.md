  Die folgende Anleitung beschreibt exemplarisch die Installation von Kitodo.Production auf einem Debian-System mit lokaler Datenbank. Für andere Distributionen sind insbesondere die Pfadangaben entsprechend anzupassen. Soll ein separater Datenbankserver verwendet werden, ist dies beim Anlegen des Datenbanknutzers für Kitodo bei der Rechtevergabe zu beachten (Schritt 3 der Grundinstallation).

Kitodo.Production benötigt mindestens 1 leistungsstarke CPU und 2 GB RAM sowie ca. 10 GB Festplattenspeicher. Darin ist der Speicherplatzbedarf der Digitalisierungsdaten nicht enthalten!

Stand: Oktober 2016.

# Grundinstallation

## 1. Debian 8 (Jessie) installieren

- OpenJDK7
- Tomcat7
- MySQL-Server 5.5 / MariaDB

## 2. MySQL-Konfiguration für InnoDB anpassen (in `/etc/mysql/my.cnf`)

- `[mysqld] innodb_file_per_table`
- MySQL-Dienst neustarten

## 3. MySQL-Datenbank und -Nutzer für Kitodo anlegen

- `mysql -uroot -p`
- `create database kitodo;`
- `grant all privileges on kitodo.* to kitodo@localhost identified by ´kitodo´;`
- `flush privileges;`
- `exit;`

## 4. Tomcat-Konfiguration für Speichermanagement anpassen (in /`etc/default/tomcat7`)

- `JAVA_OPTS="-Djava.awt.headless=true -Xmx1920m -XX:MaxPermSize=128m -XX:+UseConcMarkSweepGC"`
- Tomcat-Dienst neustarten

Hinweis: Wenn unter Tomcat neben Kitodo.Production noch weitere Applikationen (beispielsweise Solr für Kitodo.Presentation) laufen, dann sollte ein größerer Wert für MaxPermSize konfiguriert werden, beispielsweise `-XX:MaxPermSize=256m`.

## 5. Kitodo.Production WAR-Datei von GitHub ins `webapps` Verzeichnis des Tomcat kopieren

Die WAR-Datei findet man auf https://github.com/kitodo/kitodo-production/releases, und man kopiert sie bei Debian nach `/var/lib/tomcat7/webapps/`.

- Deployment läuft automatisch
- `WEB-INF/classes/hibernate.cfg.xml` anpassen
  - `hibernate.connection.url`
  - `hibernate.connection.username`
  - `hibernate.connection.password`

## 6. Datenbank für Kitodo anlegen

- DatenbankSchema (schema.sql) und Beispieldaten (default.sql) aus Unterverzeichnis `database-setup` der entpackten Kitodo Anwendung einspielen:
 - `mysql -ukitodo -Dkitodo --password=kitodo < schema.sql`
 - `mysql -ukitodo -Dkitodo --password=kitodo < default.sql`
- Tomcat neu starten, damit die erstellte Datenbank gefunden und genutzt werden kann


# Grundkonfiguration

## 1. Verzeichnisse anlegen (Pfade nach Bedarf anpassen)

- `/usr/local/kitodo/config/` (Konfiguration)
- `/usr/local/kitodo/debug/` (*) (Debug-Meldungen des OPAC-Beautifiers)
- `/usr/local/kitodo/import/`
- `/usr/local/kitodo/logs/` (*) (Log-Meldungen)
- `/usr/local/kitodo/messages/` (Lokalisierungsdateien)
- `/usr/local/kitodo/metadata/` (*) (Vorgangsverzeichnisse)
- `/usr/local/kitodo/plugins/` (Funktionsmodule)
  - `./command/`
  - `./import/`
  - `./opac/`
  - `./step/`
  - `./validation/`
- `/usr/local/kitodo/rulesets/` (Regelsätze)
- `/usr/local/kitodo/scripts/` (Shell-Skripte)
- `/usr/local/kitodo/swap/` (*) (ausgelagerte Vorgänge)
- `/usr/local/kitodo/temp/` (*) (Temporäre Dateien)
- `/usr/local/kitodo/users/` (*) (Benutzer-Verzeichnisse)
- `/usr/local/kitodo/xslt/` (XSL-Stylesheets)

## 2. Zugriffsrechte für Tomcat-User (z. B. tomcat7) für die Verzeichnisse anpassen

- Lese-/Schreibzugriff als auch Ausführungsrecht für mit * markierte Verzeichnisse
- Lesezugriff und Ausführungsrecht für alle anderen Verzeichnisse

## 3. `WEB-INF/classes/goobi_config.properties` anpassen

- Verzeichnisse konfigurieren
  - `MetadatenVerzeichnis=/usr/local/kitodo/metadata/`
  - `RegelsaetzeVerzeichnis=/usr/local/kitodo/rulesets/`
  - `KonfigurationVerzeichnis=/usr/local/kitodo/config/`
  - `xsltFolder=/usr/local/kitodo/xslt/`
  - `dir_Users=/usr/local/kitodo/users/`
  - `debugFolder=/usr/local/kitodo/debug/`
  - `pluginFolder=/usr/local/kitodo/plugins/`
  - `swapPath=/usr/local/kitodo/swap/`
  - `tempfolder=/usr/local/kitodo/temp/`
  - `localMessages=/usr/local/kitodo/messages/`

- Shell-Skripte konfigurieren (Vorlagen unter scripts/)
  - `script_createDirUserHome=/usr/local/kitodo/scripts/script_createDirUserHome.sh` (Neues Benutzerverzeichnis anlegen)
  - `script_createDirMeta=/usr/local/kitodo/scripts/script_createDirMeta.sh` (Neues Vorgangsverzeichnis anlegen)
  - `script_createSymLink=/usr/local/kitodo/scripts/script_createSymLink.sh` (Vorgang im Home-Verzeichnis verlinken)
  - `script_deleteSymLink=/usr/local/kitodo/scripts/script_deleteSymLink.sh` (Vorgang aus dem Home-Verzeichnis entfernen)

- Namenskonventionen
  - `ImagePrefix=\\d{8}` (Namenskonvention für Image-Dateien)
  - `ImageSorting=number` (Numerische oder alphanumerische Sortierung)

## 4. `WEB-INF/classes/log4j.properties` anpassen:

- `log4j.appender.rolling.File=/usr/local/kitodo/logs/kitodo.log`

## 5. Schritt:
- Alle `goobi_*.xml` und `modules.xml` aus `WEB-INF/classes/` in das in `goobi_config.properties` angegebene `KonfigurationVerzeichnis` kopieren 

## 6. Schritt
- `docket.xsl` und `docket_multipage.xsl` aus `WEB-INF/classes/` in das in `goobi_config.properties` angegebene `xsltFolder` kopieren

## 7. Schritt:
- Shell-Skripte (*.sh) aus dem Unterverzeichnis `scripts` der deployten Kitodo Anwendung in `goobi_config.properties` angegebenen Stellen (`script_*`) legen, Ausführungsrechte geben und ggf. anpassen

## 8. _Optional_: 
- Verzeichnis `pages/imagesTemp/` in der WebApp als symbolischen Link auf ein temporäres Verzeichnis anlegen
  - Damit Tomcat symbolischen Links folgt, muss auch dessen Konfiguration angepasst werden!

## 9. Datei `goobi_projects.xml` im `KonfigurationVerzeichnis` anpassen:

- `<project name="default">` wird als Standard-Projekt verwendet, weitere Projekte können definiert werden
- `<item>/<hide>` definiert das Mapping einzelner Metadatenfelder, wobei "hide"-Felder in der Oberfläche nicht angezeigt, aber dennoch prozessiert werden
  - `from="werk"` speichert Wert in Werkstückeigenschaften, `from="vorlage"` speichert Wert in Vorlageneigenschaften
  - `isdoctype`/`isnotdoctype` bestimmt, ob ein Feld für bestimmte Dokumenttypen angezeigt/nicht angezeigt werden soll; mehrere Dokumenttypen können durch "|" getrennt werden
  - `ughbinding` bestimmt, ob der Wert in der meta.xml gespeichert wird
  - `metadata` bestimmt, in welches Metadatenfeld der Wert gespeichert werden soll
  - `required` definiert Pflichtfelder
  - `docstruct="topstruct"` speichert den Wert im obersten Strukturelement (z. B. mehrbändiges Werk), docstruct="firstchild" speichert den Wert im ersten Kind-Strukturelement (z. B. Band)
- `<processtitle>` bestimmt die Bildungsvorschrift für Vorgangstitel
- `<opac use="true">` definiert, ob ein Katalogimport möglich sein soll
- `<catalogue>` gibt den Standard-Katalog aus goobi_opac.xml an
- `<defaultdoctype>` gibt den voreingestellten Standard-Dokumenttyp aus goobi_opac.xml an
- `<templates use="true"/>`
- `<metadatageneration use="true"/>`
- `<tifheader>` bestimmt die Bildungsvorschrift der TIF-Header
- `<dmsImport/>`
- `<validate>` bestimmt Validierungs- und Umformungsregeln für einzelne Metadatenfelder
  - `docstruct` (Regel trifft nur auf bestimmte Dokumenttypen zu)
  - `metadata` (Regel trifft nur auf bestimmtes Metadatenfeld zu)
  - `startswith` (Metadatenfeld beginnt mit dieser Zeichenfolge)
  - `endswith` (Metadatenfeld endet mit dieser Zeichenfolge)
  - `createelementfrom` (Namen der zusammenzuführenden Metadatenfelder)

## 10. Schritt:
- Datei `goobi_metadataDisplayRules.xml` im `KonfigurationVerzeichnis` anpassen

## 11. Schritt:
- Datei `goobi_processProperties.xml` im `KonfigurationVerzeichnis` anpassen

## 12. Schritt:
- Datei `goobi_digitalCollections.xml` im `KonfigurationVerzeichnis` anpassen

## 13. Schritt
- die Regelsatzdateien aus dem `rulesets` Verzeichnis der deployten Kitodo Anwendung in das in `goobi_config.properties` angegebene `RegelsaetzeVerzeichnis` kopieren

# Plugins installieren

## 1. OPAC-Import-Plugin
- Datei `PicaPlugin.jar` aus dem `plugin/opac` Unterverzeichnis der deployten Kitodo Anwendung im Tomcat in das Unterverzeichnis `opac` des in `goobi_config.properties` angegebenen `pluginFolder` kopieren oder unter Beibehaltung des Namens zu verlinken
- `goobi_opac.xml` im KonfigurationVerzeichnis anpassen
 - Überprüfen, ob eigener Verbundkatalog in `<catalogue>` definiert ist
 - `<doctypes>` nach Bedarf um eigene Dokumenttypen aus PICA 0500/002@ ergänzen
 - `<beautify>` nach Bedarf um eigene Konditionen ergänzen

## 2. Pica-Massimport-Plugin
- Datei `PicaMassImport.jar` aus dem `plugin/import` Unterverzeichnis der deployten Kitodo Anwendung im Tomcat in das Unterverzeichnis `import` des in `goobi_config.properties` angegebenen `pluginFolder` kopieren oder unter Beibehaltung des Namens zu verlinken
