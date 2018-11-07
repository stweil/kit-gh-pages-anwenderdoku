# Verwendung der tiffwriter.conf Datei

In der [Mailingliste](https://maillist.slub-dresden.de/pipermail/kitodo-community/2016-July/000000.html) wurde nachgefragt, ob die Datei "tiffwriter.conf" von den Anwendern benötigt wird oder nicht. Die Antworten fielen unterschiedlich aus. Generell scheint die Datei nicht benötigt zu werden. Es wurde zudem ermittelt, wozu diese Datei genutzt werden kann: 

"tiffwriter.conf dient dazu – falls gewünscht – mittels eines Perl-Skripts die im einem Image seitens der Scan-Software im Tiff-Header hinterlegten Daten zu überschreiben bzw. überhaupt erst anzulegen. Das dazugehörige [Perl-Skript](https://maillist.slub-dresden.de/pipermail/kitodo-community/2016-July/000003.html) stammt noch aus Göttinger-Zeit und kann (ggf. als automatischer Schritt) aufgerufen werden, um die Schreibweise in Tiff-Headern zu „normalisieren“."

Da die Datei genutzt werden kann, sollte sie zunächst nicht aus Kitodo.Production entfernt werden. Hinsichtlich der Weiterentwicklung von [Kitodo.Production](http://www.slub-dresden.de/ueber-uns/projekte/infrastruktur-und-softwareentwicklung/weiterentwicklung-kitodoproduction/) sollte über deren Verwendung noch einmal diskutiert werden. 

