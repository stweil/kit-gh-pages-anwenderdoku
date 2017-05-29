# Default Werte in projects.xml

In früheren Kitodo (Goobi) Versionen war es möglich, dass beim Anlegen der Vorgänge in Auswahllisten der zuerst aufgeführte Wert in das 
jeweilige Feld eingetragen wurde, wenn kein Wert ausgewählt wurde. Dies hatte den Vorteil, dass häufig auftretende Werte als erstes 
aufgelistet wurden und die Auswahlliste nur beachtet werden musste, wenn ein abweichender Wert eingetragen werden sollte. 
Jetzt muss ein Wert der Auswahlliste ausgewählt werden, um einen Vorgang anlegen zu können. 
Zudem wurde in der Datei `<default>` genutzt, um einen Standardwert zu bezeichnen. Dies hat aber nicht funktioniert!
Die gewünschte Funktion wurde durch oben skizziertes Verhalten erfüllt. 

Nach bisherigen Erkenntnissen hat `<default>` keine Auswirkung und kann aus der projects.xml-Datei entfernt werden. 
Es ist auch keine andere Lösung bekannt, die die zuvor beschriebene Funktion ermöglicht. 