# STORY

> Die Geschichte des Exit Game ist die inhaltliche Erzählung, mit denen sich die Spielenden fortbewegen.

**TIPP**: Die Komplexität und der Umfang der Geschichte ist an den Spielenden auszurichten. Zu viel Text kann in einem Team mit verschiedenen Charaktären zu unterschiedlichen Spielgeschwindigkeiten führen. Dahe rist es ratsam, die Geschichte anhand der Veranstaltung unter Umständen unterschiedlich zu beschreiben.

# Timer

In einem Chapter kann ein Timer für das Lösen der Quest angegeben werden. Dieser Timer wird als überlagernder Dialog in der oberen rechten Ecke des Browser-Fensters angezeigt. Folgende Einstellungsmöglichkeiten gibt es:

| Parameter     | Standard          | Beschreibung |
| ------------- |:-------------:| :----------- |
| show | true | Definiert, ob der Timer dem Benutzer angezeigt werden soll. |
| delay | 0 | Verzögert den Start des Timers um die angegebene Anzahl Minuten. Um eine Verzögerung unter einer Minute zu erreichen ist ein Wert zwischen 0 und 1 anzugeben.  |
| init_sound | ... | Gibt die Audio-Datei an, die bei Start des Timers (nach dem Delay) abgespielt werden soll. |
| tick_sound | ... | Gibt die Audio-Datei an, die in der Warnphase jede Sekunde abgespielt werden soll. |
| minutes | ... | Definiert die Anzahl der Minuten, die der Timer (Countdown) umfassen soll. |
| next | ... | Definiert das Kapitel, welches bei Ablauf des Timers aufgerufen werden soll. |


# Platzhalter

**HINWEIS**: Platzhalter können sowohl in Story als auch Event eingesetzt werden.

## Grundsätzlicher Aufbau

## {file: }

Der angegeben Dateinamen wird geladen und anstelle des Platzhalters `file` als Ausgabe festgelegt. Wird der Platzhalter in einem anderen Text eingebettet, wird der geladene Text in den Text eingefügt.

Beispiel:  
> {file:output.html}

## {variable: }

Mit dem Platzhalter `variable` können Inhalte aus der Event-Definition in die Ausgabe eingebracht werden. Hierbei wird zuerst versucht die Variable aus der Team-Definition (event.json->team->teacode->variables->`variable`:`inhalt`) zu ermitteln. Wenn dies nicht erfolgreich ist, wird die Variable versucht aus der Event-Definition (event.json->variables->`variable`:`inhalt`) zu ermitteln.

Der Platzhalter `{variable:master}` bewirkt, dass die Variable `master` gesucht wird und der gesamte Platzhalter ({...}) mit dem Inhalt `inhalt` ersetzt wird.

### Vordefinierte (interne) Variablen
Ergänzend zu den eigendefinierten Variablen sind auch interne Variablen definiert. Diese internen Variablen sind reservierte Begriffe, die nicht durch eigene Variablennamen ersetzt werden können.

| Variable | Beschreibung | Gültig für |
| ------------- |:------------- | :------------ |
| points | Punktestand des Teams | story |
| teamcode | Teamcode des Teams | story |
| teamname | Name (Bezeichnung) des Teams | story |
| public_teamscodes | Listet alle öffentlichen Teamcodes auf (funktioniert auch in event.json => registration => body) | story, event |
| path_story | Pfad zum aktuellen Story-Verzeichnis | story |
|path_quest | Pfad zur aktuellen Quest | quest |

# Medieninhalte

Die unterschiedlichen Medieninhalte können durch einen Platzhalter eingebettet werden. Das Format lautet:

[image|video|audio|...:{parameter1:value1}{parameter2:value2}...{parameter:value}]

Die Einleitung der Formats bestimmt, welche Inhalte und Funktionen in die Ausgabe an der Stelle der Definition eingebettet wird. Ebenso sind durch die Wahl des Medienformats die Anzahl und die Art der Parameter bestimmt. Werden Parameter angebene, die nicht für die Mediendatei anwendbar sind oder nicht als Parameter gültig sind, werden diese ignoriert.

Grundsätzlich muss sich die Mediendatei innerhalb der Story-Definition befinden und wird von dort eingebettet.

## Vorbedingungen

### precondition

Bedingungen zur Anzeige einer Mediendatei können über den Parameter `{precondition:<chapter>,<chapter>,...}`angegeben werden. <chapter> beschreibt dabei den internen Namen eines ein Kapitels, welches erreicht/gespielt worden sein muss. Ist dieses Kapitel noch nicht erreicht worden, ist die Voraussetzung nicht erfüllt und die Mediendatei wird nicht eingebunden. Durch die Angabe mehrere Kapitel müssen alle angegebenen Kapitel erreicht worden sein, damit die Mediendatei eingebettet wird.

### precondition-none

Die `precondition-none` Bedingung definiert, dass die Mediendatei nicht angezeigt wird, sobald eines der angegebenen Kapitel gespielt wurde. Diese Bedingung muss lediglich für ein angegebes Kapitel zutreffen, damit die Grafik nicht angezeigt wird. Dies kann beispielsweise hilfreich sein, wenn mit anderen `precondition` Bedingungen eine alternative Grafik angezeigt werden soll.

Beispiel:

```
[image:{filename:0.png}{precondition-none:ch1-done,ch2-done,ch3-done,ch4-done}]
[image:{filename:1.png}{precondition:ch1-done}{precondition-none:ch2-done,ch3-done,ch4-done}]
[image:{filename:2.png}{precondition:ch2-done}{precondition-none:ch3-done,ch4-done}]
[image:{filename:3.png}{precondition:ch3-done}{precondition-none:ch4-done}]
[image:{filename:4.png}{precondition:chgegenwart-done}]
```

Dieses Beispiel zeigt, dass die Grafik `0.png` angezeigt wird, sollte noch kein Kapitel `1.png`, `2.png` `3.png` oder `4.png` angezeigt worden sein. Die übrigen Grafiken werden erst angezeigt, wenn die korrespondierenden Kapitel angezeigt wurden, aber noch nicht die nachfolgenden Kapitel aufgerufen wurden. Beispielsweise benötigt die Grafik `1.png` ein zuvor angezeigtes Kapitel `ch1-done`, allerdings wird diese nur angezeigt, wenn nicht schon `2.png`, `3.png` oder `4.png` bereits angezeigt wurden. 

### precondition-one (noch nicht implementiert!)

Eine `precondition-one` Bedingung zeigt die Mediendatei an, sobald eines der angegebenen Kapitel gespielt wurde.

### precondition-none-all (noch nicht implementiert!)

Die `precondition-none` Bedingung definiert, dass die Mediendatei nicht angezeigt wird, sobald alle der angegebenen Kapitel gespielt wurden. Diese Bedingung muss für alle angegeben Kapitel zutreffen, damit die Grafik nicht angezeigt wird. Dies kann beispielsweise hilfreich sein, wenn mit anderen `precondition` Bedingungen eine alternative Grafik angezeigt werden soll.

Folgende Medienformate werden unterstützt:

## [image: ...]

Es wird eine Bilddatei eingebunden.

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| description | ... | Beschreibung der Bilddatei |
| width | ... | Breite der Bilddatei |
| credits | ... | Hinweise zu Autoren oder Copyrights |

## [audio: ...]

Mit Hilfe des Platzhalters `audio` wird eine Audio-Datei im Hintergrund abgespielt. Um eine unerwünschte Ausgabe für den Spielenden zu vermeiden, wird an der Stelle der Einbettung eine Schaltfläche eingeblendet, mit der die Ausgabe stumm oder nicht-stumm geschaltet werden kann.

Folgende Einstellungen sind möglich:

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| description | ... | Beschreibung zu der Audio-Ausgabe, die als Hinweistext auf der Schaltfläche ausgegeben wird |
| volume | 0..1 | Initiale Audio-Lautstärke |
| autoplay | true | Gibt an, ob die Audio-Ausgabe automatisch starten soll |
| controls | true | gibt an, ob Bedienelemente für die Audio-Ausgabe angezeigt werden sollen |
| loop | true | Bestimmt, ob die Audio-Ausgabe in einer Endlosschleife wiedergegeben werden soll |
|type | mp3/ogg/wav | Bestimmt, in welchem Format die Audio-Ausgabe vorliegt; diese Einstellung kann für die Browser-Unterstützung hilfreich sein |
| credits | ... | Angabe der Quelle bzw. des Autors der Audio-Datei |
| notoggle | true | Gibt an, ob die Kontrollelemente zum ein- und Ausschalten des Audiowiedergabe angezeigt werden sollen. Achtung: werden diese mit `false` ausgeschaltet, kann dies bei Medieninhalten mit Audio-Ausgabe zu einer schlechten Benutzererfahrung führen!|


## [video: ...]


| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| controls | true | |
| loop | true | |
| autoplay | true | |
| volume | 0..1 | |
| description | ... | |
| credits | ... | |
| type | mp4/ogg/webm | |
| muted | true | |
| width | ... | |
| height | ... | |
| zoom | ... | |
| crop | ... | Gibt an, ob das Video in der vertikalen verschoben werden soll, um so den angezeigten Ausschnitt zu verändern. Ein negativer Wert verschiebt das Video nach oben, ein positiver nach unten. Die Angabe ist sinnvoll, sofern der sichtbare Bereich des Videos kleiner als die Originalhöhe ist.|
| notoggle | true | Gibt an, ob die Kontrollelemente zum ein- und Ausschalten des Audiowiedergabe angezeigt werden sollen. Achtung: werden diese mit `false` ausgeschaltet, kann dies bei Medieninhalten mit Audio-Ausgabe zu einer schlechten Benutzererfahrung führen!|


## [handout: ...]

Der Platzhalter `handout` stellt ein angegebenes Dokument als Download-Link dar. Das Dokument wird als Link, welcher sich in einem gesonderten Fenster öffnent, dargerstellt.

**HINWEIS**: Die Option `merge` stellt der Handout ein PDF dar, welches sich aus den in der Story angegebenen Quests die jeweiligen Handouts ermittelt und in einem dynamisch zusammengesetzten Handout bereitstellt. Dadurch können Handout-Informationen (z.B. Teile eines Rätsels) zu der jeweiligen Quest angegeben werden, die dann gesamtheitlich bei Start eines Spiels dem Spieler als Download angeboten werden. Die Handouts werden dynamisch auf Basis einer eindeutigen ID zum Download angeboten. Die Erzeugung erfolgt immer sobald sich der Umfang der einzubindenden Dateien oder der Inhalt einer der eingebundenen Dateien ändert. Sind die Inhalte unverändert, erfolgt keine Neuerzeugung der zum Download angebotenen Handout-Datei.

Werden keine Dokumente gefunden oder enthält das zusammengesetzte Dokumente keine Seiten, wird die Datei nicht zum Download angeboten und der Platzhalter aus der Anzeige gelöscht.

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| description | ... | Die Description beschreibt den angezeigten Text für den Download-Link der PDF-Datei. Diese Angabe wird in den Metadaten der PDF auch für den Titel und das Thema gesetzt. |
| credits | ... | Die Credits beschreiben in den Metadaten der PDF den Author. |
| type | pdf | Gibt an, welchen Typ die angezeigte Mediendatei haben soll. Hier wird bisher nur PDF unterstützt. |
| merge | true | Gibt an, ob aus referenzierten Quests der Story die in den Quest-Verzeichnissen enthaltenen `handout.pdf` in einer PDF-Datei zusammengetragen werden sollen. Ist in der Story ebenfalls eine `handout.pdf` enthalten, wird diese als Deckblatt verwendet. Die Quest werden in der Reihenfolge innerhalb der Story integriert. |
| icon | true | Zeigt das Icon standardmäßig für das Handout an. Die Anzeige des Icon kann mit `false` ausgeblendet werden. |

## [playarea: ...]

Der Platzhalter `playarea` erzeugt einen Bereich mit interkagtiven Elementen. Die Anzahl der Elemente wird durch die angegebenen Parameter bestimmt. Diese Elemente können verschoben, in der Größe geändert oder rotiert werden. Mit diesen Elemente lassen sich zum Beispiel Puzzles oder Rätsel umsetzen, bei denen mehrere visuelle Bestandteile zusammengebracht werden müssen.

**Hinweis**: Es werden Grafiken für die Elemente eingebunden. Hier empfehlen sich Dateiformate mit Transparenz (z.B. das PNG-Format). Mehrere Formate werden mit "," getrennt.

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| width | 100% | Breite der Playarea. Angabe in Prozent (%) oder Pixel (px).|
| height | 600px | Höhe der Playarea. Angabe in Prozent (%) oder Pixel (px).|
| image | ... | Hintergrundbild der Playarea (geplant)|
| color | ... | Hintergrundfarbe der Playarea |
| opacity | 1.0 | Durchsichtigkeit der Playarea |
| default_size | | #random |
| default_left | | (abgelöst) #random |
| default_top | | (abgelöst) #random |
| default_rotation | | (abgelöst) #random |
| default_option_drag | all | "all" \| "none" \| "x-axis" \| "y-axis" |
| default_option_resize | true | |
| default_option_rotation | true | |

  Jeder der nachfolgenden Parameter gilt für ein eingebundenes Elemente und ist durch einen Präfix `item{id}}_` anzugeben. Beispiel: `item1_filename`, `item2_size`,... Alle Elemente mit einer identischen Nummer gehören zusammen.
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| item{id}_filename | ... | Dateiname des Element|
| item{id}_rotation | 0 | (abgelöst) #random |
| item{id}_size | | Prozentuale Größe des Elements |
| item{id}_left | 0 | (abgelöst) #random |
| item{id}_top | 0 | (abgelöst) #random |
| item{id}_option_drag | all | "all" \| "none" \| "x-axis" \| "y-axis" |
| item{id}_option_resize | true | |
| item{id}_option_rotation | true | |


## [voice: ...]

Der Platzhalter `voice` ermöglicht die Audio-Ausgabe von Text (text-to-speech). Der als Parameter angegebene Text wird hierbei über die Browser-Funktion des Spieldenden wiedergegeben. An der Stelle des Platzhalters wird eine Schaltfläche eingeblendet, mit die Ausgabe gestartet werden kann.

**Hinweis**: Die Ausgabe kann (Stand: 07/2021) nicht interaktiv beendet werden. Hierzu ist bis zur Implementierung entsprechender Möglichkeiten die Seite neu zu laden  oder die Seite zu wechseln.

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| label | ... | Beschriftung der Schaltfläche |
| content | ... | Inhalt der Sprachausgabe |

Für die Ausgabe können bis zu 10 Stimmen definiert werden, zu denen im `content`mit `!voice=>{id}!` gewechselt werden kann. `{id}`kann hierbei einen Wert von 0 bis 9 annehmen. Es werden für die Stimme die nachfolgenden Definitionen herangezogen.

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| voice{id}_volume | 0..1 | Lautstärke der Wiedergabe |
| voice{id}_rate | 0..2 | Geschwindigekit der Wiedergabe |
| voice{id}_pitch | 1..10 | Tonhöhe der Wiedergabe |
| voice{id}_language | de_DE | Sprache/Slang der Stimme |
| voice{id}_voice | 0..x | Stimme (4=Deutsch) |
| voice{id}_description | ... | Beschreibung der Stimme |

Folgende Einstellungen haben sich als ideale Einstellungen erwiesen. Für die nicht gannten Einstellkungen wird Volume=1, Sprache =de_DE und Voice=4 angenommen. 

Mit der Option `rate` kann die Geschwindigkeit beeinflusst werden. Mit `pitch` kann die Tonhöhe der Stimme beeinflusst werden. 

| Bezeichnung     | Rate          | Pitch | 
| ------------- |:-------------:| :----------- |
| Anna normal| 1 | 1 |
| Alter Mann | 0.5 | 0.1 |
| "Rezepthinweise" | 1.4 | 0.5 |
| tba | 1 | 1 |
| tba | 1 | 1 |
| tba | 1 | 1 |

## [fetch: ...]
  
Mit dem Fetch-Platzhalter werden alle Teammitglieder zu dem aktuellen Kapitel geholt, in dem sich der aufrufende Spielende befindet. Dadurch können Teammitglieder, die eine Quest nicht lösen können oder verspätet dem Spiel beitreten, zum aktuellen Kapitel geholt werden. Diese Funktion ist nur für Teammitglieder funktionsfähig, die sich mit dem identischen Teamcode registriert haben.
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| label | ... | Beschriftung des Links |
  
## Lobby

Der Lobby-Modus ermöglicht die Spielenden nach der Regristrierung in einem gemeinsamen Raum (Kapitel) warten zu lassen. Erst wenn ein Lobby-Administrator die Lobby auflöst, werden alle Teilnehmer automatisch zu dem ersten Kapitel der Story geleitet.

Die Defintionen für die iNhalte der Lobby lehnen sich an das Format der Inhaltsdefinitionen eines Kapitels an und werden in dem Zweig `lobby`-> `content` der `story.json` definiert. Die unter diesem Pfad enthaltenen Schlüssel-Wert-Paare werden dynamisch gelesen und in die entsprechenden Platzhalter der Templates eingefügt.

Bekannte Platzhalter sind:

| Platzhalter     | Beschreibung  |
| ------------- |:-------------:|
| header | Titel im Kopfbereich |
| title | Titel im Inhaltsbereich |
| body | Inhalt der Seite |

Die Inhalte der Platzhalter werden gelesen und Platzhalter (u.a. Variablen oder dynamische Median-Inhalte) ersetzt.
