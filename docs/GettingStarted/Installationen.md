Diese Auflistung von Kitodo-Installationen soll Anwendern und Entwicklern bei der Entscheidung, welche Softwareversionen relevant sind, helfen. Für Entwickler ist wichtig zu wissen, ob noch ältere Softwareversionen abgekündigt werden können. Anwender interessiert vielleicht, ob die Kombination Kitodo.Production Version x mit Tomcat Version y funktioniert.

| Institution | OS   | Kitodo.Production | Webserver   | JSP Engine  | Java JRE | Database | Viewer | Notes |
| :---        | :--- | :---             | :---        | :---        | :---     | :---   | :---  | :---  |
| [SLUB Dresden](https://www.slub-dresden.de/) | Debian Jessie | 2.0.0 | Apache2 2.4 | Tomcat 7.0 | OpenJDK 7  | MySQL 5.5 | [Goobi.Presentation](http://digital.slub-dresden.de/) | MySQL mit MyISAM Engine und latin1_swedish_ci als Collation / Charset |
| [UB Mannheim](https://www.bib.uni-mannheim.de/) | Debian Jessie + Stretch | 2.1.0+ | Apache2 2.4 | Tomcat 7.0.75-1~bpo8+1 | OpenJDK 7 | MariaDB 10.1.26 | [Goobi.Presentation 1.3.0](https://digi.bib.uni-mannheim.de/) | |


**Legende**:

* **Institution** Name der Institution (optional mit Link auf Website). Bitte Liste alphabetisch nach diesem Namen sortieren.
* **OS** Betriebsystem (typischerweise Name und Version der Linux-Distribution)
* **Kitodo.Production** Version der Kitodo.Production Software
* **Webserver** Name und Version des Webservers (typischerweise Apache2, Version 2.2 oder 2.4)
* **JSP Engine** Name und Version der Software für Java Server Pages (JSP) (typischerweise Tomcat)
* **Java JRE** Name und Version der genutzten Java Runtime Environment (JRE) 
* **Database** Name und Version der Datenbank (typischerweise MySQL oder MariaDB)
* **Viewer** Name (und optional Version, optional mit Link auf Website) der Viewer Software (beispielsweise Kitodo.Presentation oder Intranda Viewer)
* **Notes** Anmerkungen (optional)
