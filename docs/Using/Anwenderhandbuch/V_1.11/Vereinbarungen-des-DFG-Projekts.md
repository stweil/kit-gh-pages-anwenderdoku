# SQL-Schema-Namenskonventionen

## Allgemein

* ensure the name is unique and does not exist as a reserved keyword (often problem with word **group**!) → http://dev.mysql.com/doc/refman/5.7/en/keywords.html
* names must begin with a letter and may not end with an underscore
* only use letters, numbers and underscores in names
* avoid the use of multiple consecutive underscores
* avoid abbreviations and if you have to use them make sure they are commonly understood

## Tabelle

* singular, start from capital letter e.g. _User_
* avoid long names, but in case they are necessary don't use underscores (exception many to many relation) e.g. _HomeAddress_
* many to many relations with _x_ e.g. _Group_x_User_
* no prefixes e.g. _tbl_, _Table_ or any other

## Reihe

* singular, start from small letter, camel case e.g. _postalCode_
* primary key always id
* foreign key table_id e.g. _user_id_
* no column with the same name as its table

## Schlüssel

* foreign key FK_table_field e.g. _FK_User_address_id_

## Beispiel
![Example](http://i.imgur.com/34YMtIO.png)