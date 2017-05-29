# Einleitung

GoobiScripte dienen dazu, eine Aktion an mehreren Vorgängen durchzuführen, anstatt jeden Vorgang an sich bearbeiten zu müssen. 

# Schritt 1: Vorgänge suchen

Führen Sie zunächst eine [Suche](Suche-in-GoobiProduction) durch, die genau die Vorgänge als Treffer anzeigen wird, die bearbeitet werden sollen. Wenn es nicht möglich ist, die Treffermenge durch die Suche exakt zu beschränken, kann Schritt 2 durchgeführt werden. 

# Schritt 2: Vorgänge selektieren

Soll das GoobiScript nicht auf das gesamte Trefferset oder auf die gesamte Trefferseite angewendet werden, müssen zunächst die gewünschten Vorgänge aus dem Trefferset markiert werden. Dies erreicht man, indem zunächst unterhalb des Treffersets die Aktion "Anzeige anpassen" aufgerufen und dort die *Auswahlboxen* markiert werden.

![](images/Script1.jpg)

Ein Klick auf *Übernehmen* lädt anschliessend die Seite neu. so dass im Trefferset nun die Auswahlboxen angezeigt werden, mittels denen nun eine Selektion erfolgen kann.

**ACHTUNG!**: Es muss unbedingt darauf geachtet werden, dass nur die Vorgänge markiert sind, die tatsächlich durch das Script bearbeiten werden sollen. Einige Funktionen können nicht rückgängig gemacht werden.

![](images/Script2.jpg)

# Schritt 3: GoobiScript auswählen

Wenn die Vorgänge, die bearbeitet werden sollen, korrekt ausgewählt wurden, muss das Script ausgewählt werden, das ausgeführt werden soll. 

![](images/Script3.jpg)

## Auslösen der Scripte

Mit folgenen Befehlen wird das Script ausgelöst:

* *Auswahl*: Das Script wird bei den Vorgängen angewendet, die mit den Auswahlboxenmarkiert wurden.

* *Treffer dieser Seite*: Das Script wird bei den Vorgängen angewendet, die auf der Seite angezeigt werden.

* *Gesamtes Trefferset*: Das Script wird bei allen Vorgängen des Treffersets angewendet, also auch Vorgänge, die nicht auf der Seite angezeigt werden, wenn die Vorgangsliste so lange ist, dass es mehrere Listen gibt.

## Mögliche Scripte

Es werden mehrere Scripte zur Auswahl angeboten. Im Folgenden werden diese mit dem zugehörigen Befehl aufgelistet. Aufgrund mangelnder Erfahrung wird in den meisten Fällen auf eine Beschreibung verzichtet.

Großgeschriebene Textteile (TITLE_STEP, USER_NAME,...) sind Variable, die vor der Anwendung des Scripts durch den entsprechenden Wert (Bezeichnung eines bestimmten Schritts, Name eines Benutzers) ersetzt werden müssen.

 

*addUser*: 

	action:addUser "steptitle:TITLE_STEP" username:USER_NAME

Mit diesem Befehl können den Vorgängen eines Trefferset einer Aufgabe ein bestimmter Benutzer zugewiesen werden. 

*addUserGroup*: 

	action:addUserGroup "steptitle:TITLE_STEP" group:GROUP_NAME

Mit diesem Befehl können den Vorgängen eines Trefferset einer Aufgabe eine bestimmter Benutzergruppe zugewiesen werden. 

*deleteTiffHeaderFile*: 

	action:deleteTiffHeaderFile

Zu diesem Befehl liegen keine gesicherten Informationen vor. 

*swapSteps*: 

	action:swapSteps swap1nr:ORDER_NUMBER_FIRST_STEP "swap1title:TITLE_FIRST_STEP"swap2nr:ORDER_NUMBER_SECOND_STEP "swap2title:TITLE_SECOND_STEP"

Zu diesem Befehl liegen keine gesicherten Informationen vor.

*importFromFileSystem*: 

	action:importFromFileSystem sourcefolder:SOURCE_FOLDER

Zu diesem Befehl liegen keine gesicherten Informationen vor.

*swapProzessesOut*: 

	action:swapProzessesOut

Zu diesem Befehl liegen keine gesicherten Informationen vor. -> Das Script scheint nicht zu funktionieren: https://bugs.launchpad.net/goobi-production/+bug/789027

*setRuleset*: 

	action:setRuleset "ruleset:TITLE_RULESET"

Zu diesem Befehl liegen keine gesicherten Informationen vor.

*swapProzessesIn*: 

	action:swapProzessesIn

Zu diesem Befehl liegen keine gesicherten Informationen vor.

*deleteStep*: 

	action:deleteStep "steptitle:TITLE_STEP"

Mit diesem Befehl können den in den Vorgängen eines Treffersets eine Aufgabe gelöscht werden. 

*addStep*: 

	action:addStep "steptitle:TITLE_STEP" number:NUMBER_1_TO_?

Mit diesem Befehl können die Vorgänge eines Treffersets um eine weitere Aufgabe ergänzt werden. 

*setStepStatus*: 

	action:setStepStatus "steptitle:TITLE_STEP" status:NUMBER_0_TO_3

Mit diesem Befehl können in den Vorgängen eines Treffersets der Status einer Aufgabe geändert werden. 

*setStepNumber*: 

	action:setStepNumber "steptitle:TITLE_STEP" number:NUMBER_1_TO_?

Mit diesem Befehl können in den Vorgängen eines Treffersets die Nummer (Reihenfolge) einer Aufgabe geändert werden. 

*addModuleToStep*: 

	action:addModuleToStep "steptitle:TITLE_STEP" "module:MODULE_NAME"

Zu diesem Befehl liegen keine gesicherten Informationen vor.

*addShellScriptToStep*: 

	action:addShellScriptToStep "steptitle:TITLE_STEP" "label:LABEL_FOR_SCRIPT" "script:PATH_TO_SCRIPT"

Zu diesem Befehl liegen keine gesicherten Informationen vor.

*setTaskProperty*: 

	action:setTaskProperty "steptitle:TITLE_STEP" property:metadata_readimages_writeimages_validate_exportdms_automatic_batch value:true_OR_false

Zu diesem Befehl liegen keine gesicherten Informationen vor.

*tiffWriter*: 

	action:tiffWriter

Zu diesem Befehl liegen keine gesicherten Informationen vor.

*export*

	action:export exportImages:{true|false} exportOcr:{false|true}

Mit diesem Befehl werden die Vorgänge eines Trefferset exportiert, über die Parameter `exportImages` und `exportOcr` kann man bestimmen, ob die Bilddaten und / oder OCR Daten mit exportiert werden oder nicht.

*exportDms*: 

	action:exportDms exportImages:false

Mit diesem Befehl werden die Vorgänge eines Trefferset exportiert, jedoch **ohne** Metadaten. 

	action:exportDms exportImages:true

Mit diesem Befehl werden die Vorgänge eines Trefferset exportiert, jedoch **mit** Metadaten.  