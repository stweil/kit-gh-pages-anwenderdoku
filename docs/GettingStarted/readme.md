# Mitmachen


## Pflege dieser Doku

### Grundsätzliches Vorgehen

Diese Anwender-Dokumentation hat ein eigenes Repository und kann getrennt von den anderen Kitodo-Zweigen gepflegt werden. Getrennt betrachtet
müssen 
 
- Anwenderdoku
- Entwickler-Doku

Die Dokumentation der Entwickler wird als Teil des Entwicklungszweiges zusammen mit der Software erstellt und gepflegt. Die Dokumentation
für den Endanwender findet sich [hier](https://github.com/kitodo/kitodo-production.git) (im Unterverzeichnis "docs").

Da es sich bei der Anwenderdoku um ein eigenes Projekt handelt umfasst ihre Pflege und Weiterentwicklung folgende Schritte:

- Auschecken des Git-Verzeichnisses (clonen)
- Herbeiführen der gewünschten Änderung durch Einflegen der gewünschten Informationen in die ausgecheckte Quelle
- Zurückspielen der geänderten Informationen ins Repository, um die Änderungen mit anderen zu teilen (committen)

Wenn ein Release-Management eingesetzt werden soll, so ist das _Clonen_ durch ein _Fork_ zu ersetzen und das _Commitment_ durch das 
Stellen eine _Pull-Request_ an den Release-Manager.

Durch das Auschecken oder Forken entsteht in der lokalen Dateistruktur ein Verzeichnis, in dem sich ein _Docs_ -Verzeichnis befindet.
Dieses Verzeichnis ist die Wurzel der Dokumentation - in ihm liegen alle Dokumentationsquellen (thematisch sortiert in Unterordnern).

### Formate

Die Quelldateien dieser Dokumentation werden im Format "MarkDown" gepflegt. Dieses Dateiformat ist eine Textauszeichnungssprache,
die ohne Steuerzeichen auskommt. Damit ist sie mit jedem beliebigen Editor pflegbar - die Speicherung der Dateien soll immer im
Textformat erfolgen, die Kodierung des Textes soll immer UTF-8 sein. Beides ist im Editor einstellbar.  

Einen Überblick über das Format "Markdown" findet sich [hier](https://de.wikipedia.org/wiki/Markdown). Wenngleich einige verschiedene 
Weiterentwicklungen von Markdown exisiteren so unterscheiden sie sich in den grundsätzlichen Elementen nur geringfügig. 

Von der Verwendung von Auszeichnungen aus diesen Weiterentwicklungen wird abgeraten.  

### Organisation der Dateien in der Wurzel der Dokumentation

Um die Pflegbarkeit der Dokumentation zu erhöhren ist es hilfreich, sie wie einen Zettelkasten zu verstehen. Innerhalb des Zettelkastens werden 
die Zettel durch Reiterkarten strukturiert und geordnet. Die Zettel entsprechen hier unseren Dokumenten - die Reiterkarte entspricht 
einem Ordner.

Die Struktur der Anwenderdokumentation soll einfach bleiben. Daher sind nur drei Oberkategorien vorgesehen:

- "BestPractice" (Mitteilungen von Anwendern, FAQ, etc.)
- "GettingStarted" (z.B. Installationsanweisungen)
- "Using" (z.B. Anwenderhandbuch)

Vermutlich lassen sich alle Dokumentationsobjekte in dieser Struktur unterbringen. Gelingt das nicht sollte überlegt werden,
ob es sich nicht vielleicht um Entwicklerdoku handelt. Das Anlegen von Unterverzeichnissen zur Gruppierung von Dokumentation ist statthaft.

Auf Verweise, die auf Dokumente in anderen Ordnern referenzieren, sollte aus Gründen der Wartbarkeit verzichtet werden - so sind leicht 
logische Umgruppierungen möglich, ohne dass man fürchten muss, eventuelle Navigationsverweise unbrauchbar zu machen. Die logische Zusammengehörigkeit
von Dokumenten sollte anhand der Pfadstruktur erkannt werden.