Auf dieser Seite werden die Einstellungen der [Aufgaben](https://github.com/kitodo/kitodo-production/wiki/Aufgaben) einer Produktionsvorlage beispielhaft aufgeführt. Dies soll zeigen, welche Aktionen in einer Aufgabe möglich sind. So wird durch Aktivierung von _Images lesen_ und _Images schreiben_ die Verlinkung ins Homeverzeichnis ermöglicht, um Images nach Kitodo.Production verschieben zu können. Durch Aktivierung von _Metadaten_ wird der Metadateneditor gestartet, wenn eine Aufgabe übernommen wird.
Kurzum, kann aus folgender Tabelle eine Einstellung übernommen werden, die die grundlegenden Funktionen der Aufgaben ermöglicht. 


| Details | Aufgabe1 | Aufgabe2 | Aufgabe3 | Aufgabe4 | Aufgabe5 | Aufgabe6 |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| Titel  | Anlegen eines Vorganges  | Scannen  | LZA Validierung  | Erfassen der Meta- und Strukturdaten  | OCR durchführen  | Export / Import in das DMS |
| Reihenfolge | 1 | 2 | 3 | 4 | 5 | 6 |
| Priorität | 0 | 0 | 0 | 0 | 0 | 0 |
| Metadaten | - | - | - | Haken | - | - |
| Import mittels Dateiupload | - | - | - | - | - | - |
| Images lesen | - | Haken | - | - | - | - |
| Images schreiben | - | Haken | - | - | - | - |
| Beim Abschließen verifizieren | Haken | - | - | Haken | - | - |
| Export DMS | - | - | - | - | - | Haken |
| Aufgabe beim Annehmen abschließen | - | - | - | - | - | - |
| Automatische Aufgabe | - | - | Haken | - | Haken | Haken |
| Script Schritt | - | - | LZA Validierung | - | OCR | - |
| Status | Abgeschlossen | Offen | Gesperrt | Gesperrt | Gesperrt | Gesperrt |
| Batch Schritt || - | - | - | - | - | - |
| Schritt Plugin | - | - | - | - | - | - |
| Validierungs Plugin | - | - | - | - | - | - |
|   |   |   |   |   |   |   |
| **[Benutzergruppen](https://github.com/kitodo/kitodo-production/wiki/Benutzergruppen)** | Prozessverwaltung | Scanner | LZA Validierung | Metadaten | OCR | Import DMS |