# Bearbeitung von Titeln in nicht-lateinischer Sprache

Ob in Kitodo.Production auch nicht-lateinische Schriften wie Arabisch oder Hebräisch bearbeitet werden können, hängt von mehreren Faktoren ab (Datenquelle, Präsentation, Kitodo.Production-Version, Datenbank- Format ...). Auf dieser Seite werden die bisherigen Erkenntnisse gesammelt. 

Diese wurden unter folgenden Bedingungen gewonnen: 

- Datenquelle: SWB 
- Kitodo.Production Version: CE 1.11
- Präsentation: Kitodo.Presentation 


**Fragen** 

1. Können nicht-lateinische Schriftzeichen aus dem SWB importiert werden (Originalschrift, Transliteration)?
2. Werden diese Schriftzeichen in Kitodo.Production korrekt dargestellt?
3. Gibt es Probleme mit der Kitodo.Production Datenbank?
4. Werden die Inhalte auch in der METS/MODS-Datei korrekt dargestellt?
5. Werden die Inhalte korrekt von den Exportscripten prozessiert?
6. Werden die Inhalte korrekt von der Präsentationssoftware interpretiert und dargestellt?
7. Können im Metadateneitor von Kitodo.Production auch hebräische oder arabische Schriftzeichen eingegeben werden?


**Antworten**

1. Erste Tests mit den unten aufgeführten Beispielen ergaben, dass hebräische und arabische Schriftzeichen sowohl in Originalschrift als auch in transliterierter Form aus dem SWB importiert werden können.
Wenn die 4000 wiederholt wurde, muss gegebenenfalls der transliterierte Text mit der Originalschrift ersetzt werden. Kitodo importiert nur das zuerst aufgeführte Feld 4000. 
2. Diese Schriftzeichen werden auch korrekt in den Metadatenfeldern von Kitodo.Production  dargestellt.
3. Mit der Datenbank gibt es Probleme, wenn der ATS mit nicht-lateinischen Schriftzeichen gebildet werden soll. Diese werden als "." übernommen, was ungültig ist. Es ist jedoch möglich, dass das Metadatum ATS manuell korrigiert wird, wodurch ein gültiger Vorgangstitel erstellt werden kann.
Zudem muss bedacht werden, dass die Datenbank je nach Zeichenkodierung nicht alle Sonderzeichen darstellen kann - unabhängig davon, dass die Zeichen in den Metadaten der METS/MODS-Datei korrekt angezeigt werden!
4. Mit den Beispielen konnte eine korrekte METS/MODS-Datei erzeugt werden (siehe Beispiel unten).
5. Im Testsystem ist der Export möglich.
6. Dies kann nicht bewertet werden, da keine Testpräsentation vorhanden ist. 
7. Der Metadateneditor bietet keine Eingabeerleichterung von hebräischen oder arabische Schriftzeichen. Diese Texte können aber in andern Programmen erstellt und in die jeweiligen Metadatenfelder eingefügt werden.


**Beispiele Titelaufnahmen SWB**

---
	0100 435213504
	0500 Aau
	1100 2014
	1130 druck
	1500 heb
	1700 XB-IL
	2000 978-965-493-390-2
	2000 965-493-390-X
	2240 BSZ: 435213504
	3000 $T01$ULatn%%!164748482!$PNaḥmān Ben-Śimḥā*1772-1811*
	3000 $T01$UHebr%%!164748482!נחמן<מברסלב>*1772-1811*
	3010 $T01$ULatn%%!406566674!Mark, Zvi*1963-*
	3010 $T01$UHebr%%!406566674!מרק, צבי*1963-*
	4000 $T01$ULatn%%Kol sipure Rabi Naḥman mi-Braslav$dha-maʻaśiyot, ha-sipurim ha-sodiyim, ha-ḥalomot ṿe-ha-ḥezyonot ; liḳuṭ ha-nusaḥim mi-kitve yad nedirim u-mi-mikhlol ha-sifrut ha-Braslavit be-tosefet pirḳe mavo ṿe-heḳshere ha-sipurim$hme-et Tsevi Marḳ
	4000 $T01$UHebr%%כל סיפורי רבי נחמן מברסלב$dהמעשיות, הסיפורים הסודיים, החלומות והחזיונות ; ליקוט הנוסחים מכתבי יד נדירים`וממכלול הספרות הברסלבית בתוספת פרקי מבוא והקשרי הסיפורים$hמאת צבי מרק
	4030 Jerusalem$nBialik Institute
	4060 472 S.
	4062 25 cm
	4201 Includes bibliographical references (p. 457-461) and indexes
	4211 Complete stories of Rabbi Nachman of Bratslav
	5500 |p|Naḥman 1772-1811; Naḥman 1772-1811
	5500 |s|Hasidic parables
	5500 |s|Hasidim; Legends
	5500 |s|Hasidic parables
	5500 |s|Hasidim; Legends
---

---

	0100 429542852
	0500 Aau
	0575 zkor
	1100 2015
	1130 druck
	1500 ara
	1700 XB-LB
	2000 978-9953-89-041-8
	2240 BSZ: 429542852
	3000 $T01$ULatn%%!301580537!Yazbak, Samar*1970-*
	3000 $T01$UArab%%!301580537!يزبك, سمر*1970-*
	4000 $T01$ULatn%%Rāʾiḥat al-qirfa$driwāya$hSamar Yazbak
	4000 $T01$UArab%%رائحة القرفة$dرواية$hسمر يزبك
	4020 $T01$ULatn%%Aṭ-Ṭabʿa 3
	4020 $T01$UArab%%الطبعة 3
	4030 $T01$ULatn%%Bairūt$nDār al-Ādāb
	4030 $T01$UArab%%بيروت$nدار الآداب
	4201 In arab. Schrift, arab.
---

**Beispiele MODS**

Folgende METS/MODS-Dateien wurden beim Export erstellt:

- [NamKol_435213504](images/NamKol_435213504.xml)
- [PeleEdi_435218530](images/PeleEdi_435218530.xml)
- [YazbRi_429542852](images/YazbRi_429542852.xml)


NamKol_435213504: 

---
	<mods:titleInfo>
	<mods:title>הספרות הברסלבית בתוספת פרקי מבוא והקשרי הסיפורים</mods:title>
	<mods:subTitle>ha-maʻaśiyot, ha-sipurim ha-sodiyim, ha-ḥalomot ṿe-ha-ḥezyonot ; liḳuṭ ha-nusaḥim mi-kitve yad nedirim u-mi-mikhlol ha-sifrut ha-Braslavit be-tosefet pirḳe mavo ṿe-heḳshere ha-sipurim</mods:subTitle>
	<mods:subTitle>המעשיות, הסיפורים הסודיים, החלומות והחזיונות ; ליקוט הנוסחים מכתבי יד נדירים וממכלול הספרות הברסלבית בתוספת פרקי מבוא והקשרי הסיפורים</mods:subTitle>
	</mods:titleInfo>
	<mods:language>
	<mods:languageTerm authority="rfc3066" type="code">heb</mods:languageTerm>
	<mods:scriptTerm authority="iso15924" type="code">Latf</mods:scriptTerm>
	</mods:language>
	<mods:originInfo>
	<mods:place>
	<mods:placeTerm type="text">Jerusalem</mods:placeTerm>
	</mods:place>
	<mods:dateOther encoding="w3cdtf" type="order">2014</mods:dateOther>
	<mods:publisher>Bialik Institute</mods:publisher>
	</mods:originInfo>
	<mods:name type="personal">
	<mods:role><mods:roleTerm authority="marcrelator" type="code">aut</mods:roleTerm></mods:role>
	<mods:namePart type="family">Naḥmān Ben-Śimḥā</mods:namePart>
	<mods:displayForm>Naḥmān Ben-Śimḥā</mods:displayForm></mods:name>
	<mods:name type="personal"><mods:role>
	<mods:roleTerm authority="marcrelator" type="code">aut</mods:roleTerm></mods:role>
	<mods:namePart type="family">נחמן<מברסלב>,</mods:namePart>
	<mods:displayForm>נחמן<מברסלב>,</mods:displayForm>

---

 
YazbRi_429542852: 

---

	<mods:titleInfo>
	<mods:title>رائحة القرف</mods:title>
	<mods:subTitle>riwāya</mods:subTitle>
	<mods:subTitle>رواية</mods:subTitle>
	</mods:titleInfo>
	<mods:language>
	<mods:languageTerm authority="rfc3066" type="code">ara</mods:languageTerm>
	<mods:scriptTerm authority="iso15924" type="code">Latf</mods:scriptTerm>
	</mods:language>
	<mods:originInfo>
	<mods:place>
	<mods:placeTerm type="text">Bairūt</mods:placeTerm>
	</mods:place>
	<mods:place>
	<mods:placeTerm type="text">بيروت</mods:placeTerm>
	</mods:place>
	<mods:dateOther encoding="w3cdtf" type="order">2015</mods:dateOther>
	<mods:publisher>Dār al-Ādāb</mods:publisher>
	<mods:publisher>دار الآداب</mods:publisher>
	</mods:originInfo>
	<mods:name type="personal">
	<mods:role><mods:roleTerm authority="marcrelator" type="code">aut</mods:roleTerm></mods:role>
	<mods:namePart type="family">Yazbak</mods:namePart><mods:namePart type="given">Samar</mods:namePart>
	<mods:displayForm>Yazbak, Samar</mods:displayForm></mods:name>
	<mods:name type="personal">
	<mods:role><mods:roleTerm authority="marcrelator" type="code">aut</mods:roleTerm></mods:role>
	<mods:namePart type="family">يزبك</mods:namePart><mods:namePart type="given">سمر</mods:namePart>
	<mods:displayForm>يزبك, سمر</mods:displayForm></mods:name>
	<mods:originInfo>
	<mods:edition>Aṭ-Ṭabʿa 3</mods:edition></mods:originInfo>

---


