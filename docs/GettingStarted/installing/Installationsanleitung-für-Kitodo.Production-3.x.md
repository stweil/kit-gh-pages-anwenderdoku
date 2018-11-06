# Install Kitodo 3.0.0-beta.1

Die folgende Anleitung beschreibt exemplarisch die Installation von Kitodo.Production auf einem Debian-System mit lokaler Datenbank. Für andere Distributionen sind insbesondere die Pfadangaben entsprechend anzupassen. Soll ein separater Datenbankserver verwendet werden, ist dies beim Anlegen des Datenbanknutzers für Kitodo bei der Rechtevergabe zu beachten.

Kitodo.Production benötigt mindestens 1 leistungsstarke CPU und 3 GB RAM sowie ca. 10 GB Festplattenspeicher. Darin ist der Speicherplatzbedarf der Digitalisierungsdaten nicht enthalten!

## A) Installation

We will install the [Kitodo.Production 3.0.0-beta.1 pre-release](https://github.com/kitodo/kitodo-production/releases/tag/kitodo-production-3.0.0-beta.1) on a Debian 9.5 operating system with Tomcat 8, MySQL 5.7 and Elasticsearch 5.x. Please follow the instructions.

### A1. Install Debian 9.5 (Stretch)

Download and install [Debian 9.5](https://cdimage.debian.org/debian-cd/9.5.0/amd64/iso-cd/).

### A2. Install sudo and reboot

Debian recommends to use [sudo](https://wiki.debian.org/sudo) instead of opening a session as root.

```
su -c "apt install -y sudo && adduser $USER sudo && echo \"Defaults timestamp_timeout=300\" >> /etc/sudoers.d/timeout && reboot"
```

### A3. Add mysql.com 5.7 and elastic.co 5.x repositories

We will add official repositories of Oracle and elastic to get the newest versions of MySQL 5.7 and Elasticsearch 5.x.

```
sudo apt install -y apt-transport-https dirmngr
```

```
sudo apt-key adv --keyserver pgp.mit.edu --recv-keys 5072E1F5 && echo "deb http://repo.mysql.com/apt/debian/ stretch mysql-5.7" | sudo tee -a /etc/apt/sources.list.d/mysql-5.7.list
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - && echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
```

### A4. Install packages openjdk-8, tomcat8, mysql-community-server, elasticsearch and curl

You will be asked to set a root password for mysql. You may leave it blank (not recommended for production mode).

```
sudo apt update && sudo apt install -y openjdk-8-jdk tomcat8 mysql-community-server elasticsearch curl
```

### A5. Configure Tomcat

We recommend to provide at least 1920m JAVA heap space to Tomcat.

```
sudo sed -i 's/JAVA_OPTS="-Djava.awt.headless=true/JAVA_OPTS="-Djava.awt.headless=true -Xmx1920m/' /etc/default/tomcat8
```

### A6. Configure MySQL

The following commands will preconfigure MySQL, create a database and a database user. You will be asked for the MySQL root password that you set before.

```
sudo sh -c "echo '[mysqld] innodb_file_per_table' >> /etc/mysql/my.cnf"
sudo service mysql restart
sudo mysql -e "create database kitodo;grant all privileges on kitodo.* to kitodo@localhost identified by 'kitodo';flush privileges;"
```

Now we will ingest a SQL file from the Kitodo GitHub Repository to set up the database schema and provide some example data.

```
curl -L https://github.com/kitodo/kitodo-production/releases/download/kitodo-production-3.0.0-beta.1/kitodo-production-3.0.0-beta.1.sql | mysql -u kitodo -D kitodo --password=kitodo
```

### A7. Configure ElasticSearch

The following commands will set configs in `/etc/elasticsearch/elasticsearch.yml` and create an index named `kitodo`.

```
sudo sed -i 's/#path.data: \/path\/to\/data/path.data: \/var\/lib\/elasticsearch/' /etc/elasticsearch/elasticsearch.yml
sudo sed -i 's/#path.logs: \/path\/to\/logs/path.logs: \/var\/log\/elasticsearch/' /etc/elasticsearch/elasticsearch.yml
sudo sed -i 's/#cluster.name: my-application/cluster.name: kitodo/' /etc/elasticsearch/elasticsearch.yml
sudo sed -i 's/#node.name: node-1/node.name: kitodo-1/' /etc/elasticsearch/elasticsearch.yml
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable elasticsearch.service
sudo systemctl start elasticsearch.service
```

Other ElasticSearch settings can be adjusted in _kitodo_config.properties_ file:

```
elasticsearch.host=localhost
elasticsearch.port=9200
elasticsearch.protocol=http
elasticsearch.index=kitodo
elasticsearch.batch=1000
elasticsearch.useAuthentication=true
elasticsearch.user=kitodo
elasticsearch.password=kitodo
```

### A8. Create directories and set permissions

We will download a zip file from the Kitodo GitHub Repository that contains all needed directories and additional config files. We will extract the zip archive into the default folder `usr/local/kitodo`. If you want to use another folder please update paths in `/var/lib/tomcat8/webapps/kitodo/WEB-INF/classes/kitodo_config.properties` (will be generated in the deployment of war file below) also.

```
sudo mkdir /usr/local/kitodo
wget https://github.com/kitodo/kitodo-production/releases/download/kitodo-production-3.0.0-beta.1/kitodo-production-3.0.0-beta.1-config.zip
sudo unzip kitodo-production-3.0.0-beta.1-config.zip -d /usr/local/kitodo
sudo chown -R tomcat8:tomcat8 /usr/local/kitodo
```

### A9. Download modules

Modules need to be downloaded and copied into the modules folder, e.g. `/usr/local/kitodo/modules/`

```
sudo mkdir /usr/local/kitodo/modules
wget https://github.com/kitodo/kitodo-production/releases/download/kitodo-production-3.0.0-beta.1/kitodo-production-3.0.0-beta.1-modules.zip
sudo unzip kitodo-production-3.0.0-beta.1-modules.zip -d /usr/local/kitodo/modules
sudo chown -R tomcat8:tomcat8 /usr/local/kitodo/modules
```

### A10. Deploy war file into Tomcat

Moving the prepared war file from the Kitodo GitHub Repository into the webapps directory triggers Tomcat to deploy the application automatically.

```
wget https://github.com/kitodo/kitodo-production/releases/download/kitodo-production-3.0.0-beta.1/kitodo-3.0.0-beta.1.war
sudo chown tomcat8:tomcat8 kitodo-3.0.0-beta.1.war
sudo mv kitodo-3.0.0-beta.1.war /var/lib/tomcat8/webapps/kitodo.war
until curl -s GET "localhost:8080/kitodo/pages/login.jsf" | grep -q -o "KITODO.PRODUCTION" ; do sleep 1; done
```

### A11. Login

The Kitodo Webapp should be available at <http://localhost:8080/kitodo/> now. Give it a try before you continue to configure the system.

* user: testAdmin
* pass: test

### A12. Index example data

After logging in you can access the indexing page (via menu "System" or directly at <http://localhost:8080/kitodo/pages/system.jsf>). First create mapping by clicking button "Create mapping". Next, start indexing the provided example data by clicking on the button "Start indexing" (at whole index).

## B) Configuration (optional)

### B1. change default project settings

You may want to set some defaults in config file `/usr/local/kitodo/config/kitodo_projects.xml`.

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
- `<catalogue>` gibt den Standard-Katalog aus kitodo_opac.xml an
- `<defaultdoctype>` gibt den voreingestellten Standard-Dokumenttyp aus kitodo_opac.xml an
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

### B2. change further configs

Further settings may be made in the following config files:

* `/usr/local/kitodo/config/kitodo_opac.xml`
* `/usr/local/kitodo/config/kitodo_metadataDisplayRules.xml`
* `/usr/local/kitodo/config/kitodo_digitalCollections.xml`
* `/var/lib/tomcat8/webapps/kitodo/WEB-INF/classes/kitodo_config.properties` (general settings, e.g. filename prefix for images)
* `/var/lib/tomcat8/webapps/kitodo/WEB-INF/classes/hibernate.cfg.xml` (connection url, username and password to mysql database)
* `/var/lib/tomcat8/webapps/kitodo/WEB-INF/classes/log4j2.xml` (logging)

### B3. save temp images in /tmp instead of webapp folder

Temporary image files will be saved in the Tomcat webapp folder. You may want to save them in the /tmp directory to save disk space.

```
sudo ln -s /tmp /var/lib/tomcat8/webapps/kitodo/pages/imagesTemp
sudo chown -h tomcat8:tomcat8 /var/lib/tomcat8/webapps/kitodo/pages/imagesTemp
sudo sed -i 's/<\/Context>/    <Resources allowLinking="true" \/>\n<\/Context>/' /var/lib/tomcat8/webapps/kitodo/META-INF/context.xml
```

### B4. restart Tomcat

To apply changes we need to reload the Kitodo webapp. Assuming there are no other webapps deployed on this server, we could just restart the Tomcat server.

```
sudo systemctl restart tomcat8
until curl -s GET "localhost:8080/kitodo/pages/login.jsf" | grep -q -o "KITODO.PRODUCTION" ; do sleep 1; done
```