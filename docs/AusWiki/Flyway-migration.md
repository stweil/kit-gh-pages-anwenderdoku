## Für Entwickler:

# New Database
Run Maven's profile 'flyway' with goal 'migrate'.

Result table schema_version:
![schema_version table after migrate](http://i.imgur.com/cIU8cED.png)

# Existing Database
Run Maven's profile 'flyway' two times. First goal: 'baseline', second goal: 'migrate'.

Result table schema_version:
![schema_version table after baseline and migrate](http://i.imgur.com/5hQ7iKT.png)

## Für Kitodo-Anwender
Auf der Datenbank das mitgelieferte "migrate_db.sql" Script ausführen
Achtung! Sollten sie nicht von der letzten Version migrieren, müssen sie auch die Migrationsscripte der übersprungenen Versionen ausführen.