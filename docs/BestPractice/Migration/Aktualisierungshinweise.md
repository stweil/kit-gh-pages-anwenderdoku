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

In beiden Fällen müssen `database host`, `user` und `database` mit den genutzten Einstellungen ersetzt werden. Der Benutzer `user` muss die Berechtigung haben, die Datenbankstruktur der genutzten Datenbank zu ändern.
