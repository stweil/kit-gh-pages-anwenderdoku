# Einleitung 
Ein Thema, das die Anwender von Kitodo schon länger beschäftigt und im Zuge der [RAK-RDA-Umstellung](RAK-RDA-Umstellung) noch dringlicher wurde, ist der Import von Personen- und Körperschafts-Metadaten. 

In GitHub ist dieses Thema schon an zwei Stellen teilweise beschrieben worden: 
- [New features for METS Editor](New-features-for-METS-Editor)
- [Import of personal and corporate names / missing identifier #195 ](https://github.com/kitodo/kitodo-production/issues/195)

In der Mailing-Liste wurde unter dem Thread „_[Goobi] RDA-Umstellung_“ ein [Dokument](images/Personenimport_GOOBI_Anforderungen_2016_ver4_FDHohmann.pdf) zur Diskussion gestellt, in dem die grundlegenden Wünsche beschrieben wurden. Auf dessen Grundlage sollten die Anforderungen der unterschiedlichen Anwender und der Entwickler zusammengebracht werden, um zu einer guten und transparenten Lösung zu gelangen. 

Auf dieser Seite werden die wichtigsten Diskussionspunkte und Hinweise gesammelt. Diese Inhalte dienen nur der Ideensammlung! Konkrete Ergebnisse für Entwickler müssen als [Issue](https://github.com/kitodo/kitodo-production/issues) formuliert werden. Es ist hilfreich, wenn dort die Anforderung knapp beschrieben wird und gegebenenfalls auf diese Stelle verwiesen wird. 

# Diskussionsthemen
## MODS / `termsOfAddress`

Es ist nach [MODS](http://www.loc.gov/standards/mods/userguide/name.html) erlaubt, das Attribut `termsOfAddress` mehrfach zu verwenden. Jedoch wurde von den Entwicklern darauf aufmerksam gemacht, dass wenn mehrere Felder wie zum Beispiel: 

- Präfix
- Zählung
- Beiname
- Gattungsname
- Territorium
- Titulatur
- Beziehungskennzeichnung (Code)

mit dem gleichen Attribut `termsOfAddress` ausgezeichnet werden, eine "kontrollierte" Prozessierung der Daten nicht möglich ist. Dies betrifft zum Beispiel die Reihenfolge der Felder in der Anzeige oder auch "zurück mappen" nach PICA. 

Wenn MODS keine anderen Felder oder Attribute bietet, um diese Informationen zu speichern, muss natürlich mit den gegebenen Möglichkeiten eine Lösung gefunden werden. 

## Gruppieren von Metadaten

Da der Import von Körperschafts-Metadaten bisher nicht implementiert ist, kann eine Gruppierung der Metadaten genutzt werden, wie sie in der [Zeutschel Dokumentation](http://www.goobi.org/fileadmin/groups/goobi/dokumentation/TS-1105_Weiterentwicklungen-GOOBI-WLB.pdf) auf Seite 14 ff. beschrieben ist. 

Es muss unbedingt beachtet werden, dass die Prozessierung der Metadaten grundlegend anders durchgeführt wird, als bei Personennamen. Zudem muss untersucht werden, ob es möglich ist, gruppierte Metadaten zu gruppieren. Dies wäre notwendig, wenn die Metadaten der Körperschaft mit anderen Metadaten gruppiert werden sollen. _Eine Schachtelung von Metadatengruppen ist zur Zeit nicht möglich_: [https://maillist.slub-dresden.de/pipermail/goobi-community/Week-of-Mon-20160516/000604.html](https://maillist.slub-dresden.de/pipermail/goobi-community/Week-of-Mon-20160516/000604.html).  

Die andere Möglichkeit ist die Anpassung der [ugh](https://github.com/goobi/goobi-ugh/tree/master/ugh). Die größte Hürde bei diesem Lösungsansatz ist deren sehr lückenhafte bis nicht vorhandene Dokumentation. 

## Beziehungskennzeichnungen 

Die Rolle einer Person oder einer Körperschaft wird in RDA durch Beziehungskennzeichnungen definiert. Diese sollte nach Kitodo.Production übernommen werden, um ein manuelles Ausfüllen des Metadatums zu vermeiden. 

Wichtig ist eine Entscheidung darüber, ob diese Information  im Regelsatz definiert wird, oder ob diese Information auch ohne Mapping zum Export gebracht werden kann. 

Letzteres würde eine umfangreiche Regelsatzerweiterung vermeiden. Andererseits wäre keine individuelle Zuordnung zu bestimmten Strukturelementen möglich. 

Es gibt unterschiedliche Quellen für diese Beziehungskennzeichnungen, aber alle nutzen den dreistelligen MARC-Code. Es sollte diskutiert werden, welche Beziehungskennzeichnungen genutzt werden sollen.  
Es wurde eine [Übersichtstabelle](images/RDA_Beziehungskennzeichen.xlsx) erstellt, die die Werte von SWB, MARC und GBV enthält. Bis auf SoftwareentwicklerIn (oth) sind im SWB und GBV alle Werte gleich. MARC bietet jedoch noch weitere Werte. SWB und GBV bieten Beziehungskennzeichnungen an, die den gleichen MARC-Code (oth) verwenden. Hier muss geprüft werden, ob dies Probleme beim Export verursacht.  

Quellen: 

_MARC Code List for Relators_: 

[http://www.loc.gov/marc/relators/relacode.html](http://www.loc.gov/marc/relators/relacode.html)

_SWB - Beziehungskennzeichnungen für die Felder 3010 und 3110_: 

[http://swbtools.bsz-bw.de/winibwhelp/Liste_3010_3110_AnhangI.htm](http://swbtools.bsz-bw.de/winibwhelp/Liste_3010_3110_AnhangI.htm)

_SWB - Beziehungskennzeichnungen für die Felder 3000 (Unterfeld $B)_: 

[http://swbtools.bsz-bw.de/cgi-bin/help.pl?cmd=kat&val=3000&regelwerk=RDA&verbund=SWB](http://swbtools.bsz-bw.de/cgi-bin/help.pl?cmd=kat&val=3000&regelwerk=RDA&verbund=SWB) 

_SWB - Beziehungskennzeichnungen für die Felder 3100 (Unterfeld $B)_: 

[http://swbtools.bsz-bw.de/cgi-bin/help.pl?cmd=kat&val=3100&regelwerk=RDA&verbund=SWB](http://swbtools.bsz-bw.de/cgi-bin/help.pl?cmd=kat&val=3100&regelwerk=RDA&verbund=SWB) 

_GBV - Beziehungskennzeichnungen für die Felder 3010 und 3110_: 

[https://www.gbv.de/bibliotheken/verbundbibliotheken/02Verbund/01Erschliessung/02Richtlinien/02KatRichtRDA/anhaenge/anhang-beziehungskennzeichen](https://www.gbv.de/bibliotheken/verbundbibliotheken/02Verbund/01Erschliessung/02Richtlinien/02KatRichtRDA/anhaenge/anhang-beziehungskennzeichen) 

_MODS – RoleTerm_: 

[http://www.loc.gov/standards/mods/mods-outline-3-6.html#name](http://www.loc.gov/standards/mods/mods-outline-3-6.html#name) 

