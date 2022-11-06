# STORY

> Die Geschichte des Exit Game ist die inhaltliche Erzählung, mit denen sich die Spielenden fortbewegen.

**TIPP**: Die Komplexität und der Umfang der Geschichte ist an den Spielenden auszurichten. Zu viel Text kann in einem Team mit verschiedenen Charakteren zu unterschiedlichen Spielgeschwindigkeiten führen. Daher ist es ratsam, die Geschichte anhand der Veranstaltung unter Umständen unterschiedlich zu beschreiben.

## Benutzeroberfläche

`chapter` -> `<chapterid>` -> `userinterface`

Die Benutzeroberfläche kann in einigen Teilen angepasst werden. So könnne bestimmte grafische Elemente situativ je Kapitel angezeigt bzw. nicht angezeigt werden. Die Vorgabe erfoilgt dabei in der Regel durch das genutzte Template des Event bzw. der Story.

Folgende Einstellungen sind implementiert und müssen vom jeweiligen Template unterstützt werden:

| --- | --- |
| progressbar | Aktiviert die Anzeige der Fortschrittsanzeige (progressbar) mit `true` oder blendet diese aus (`false`)) |
| hint | Aktiviert die Anzeige der der Schaltfläche für Hinweise mit `true` oder blendet diese aus (`false`)) |
| help | Aktiviert die Anzeige der der Schaltfläche für die Hilfe mit `true` oder blendet diese aus (`false`)) |
| fetch | Aktiviert die Anzeige der der Schaltfläche für das Zusammenholenb der Teammitglieder mit `true` oder blendet diese aus (`false`)) |
| sketchpad | Aktiviert die Anzeige der der Schaltfläche für das Sketchpad mit `true` oder blendet diese aus (`false`)) |

Grundsätzlich sind im Zusammenspiel mit einer Unterstützung im Template weitere hier nicht beschriebene Einstellungsmöglichkeiten denkbar. In den von 3Exiteers unterstützten Template sind jedoch die oben beschrieben Einstellungsmöglichkeiten vorgesehen.

## Handhabung von Lösungseingaben

### Ergänzende Lösungen

`chapter` -> `<chapterid>` -> `solution` -> `solutions`

Es können ergänzend zu den Lösungen der Quest in einem Kapitel weitere Lösungen angegeben werden. Standardeinstellung sind keine weiteren Lösungen.

### Erweiterungsmodus für ergänzende Lösungen

`chapter` -> `<chapterid>` -> `solution` -> `expandmode`

Es kann für ergäzende LÖsungen definiert werden, wie diese verwendet werden sollen. Hierbei wird der Umfang der Lösungen zumeist verändert und je nach Modus ebenso die Stabndard-Lösung. Die Standard-Lösung ist dabei die erste Lösung in der Liste der als valide definierten Lösungen, die als Variableninhalt für `%%%variable:solution%%%` verwendet wird und damit zum Beispiel in dem Hilfesystem angezeigt wird.

Mögliche Werte:

| --- | --- |
| 0 | keine Ergänzung von Lösungen |
| 1 | Ergänzungen werden vor die Lösungen der Quest gesetzt. Hiermit ändert sich die erste Lösung, die an vielen Stellen als Standard-Lösung angezeigt wird (u.a. im Hilfedialog). |
| 2 | Ergänzungen werden nach den Lösungen der Quest gesetzt. damit wird die Liste der validen Lösungen erweitert und die Standard-Lösung bleibt von der Quest erhalten. (Standard)|
| 3 | Ergänzungen ersetzen die Lösungen der Quest und verändern damit die validen Lösungen, sowie die Standard-Lösung. |

### Schreibweise

`chapter` -> `<chapterid>` -> `solution` -> `casesensitive`

Die Eingabe einer Lösung durch den Spielenden kann unter Beachrung der Schreibweise (`true`) oder ohne Berücksichtigung der Schreibweise (`false`) interpretiert werden. Standardeinstellung ist `false`.

### Kürzen der Eingabe

`chapter` -> `<chapterid>` -> `solution` -> `trim`

Leerzeichen zu Beginn und am Ende von Eingaben werden entfernt (`true`) oder wie vom Spielenden eingeben behalten (`false`). Standardeinstellung ist `false`.

### Teilzeichenkette

`chapter` -> `<chapterid>` -> `solution` -> `substring`

Ist die EIngae ein Teil der Lösung, wird diese akzeptiert (`true`). Altermativ muss die Lösung exakt eingegeben werden (`false`). Standardeinstellung ist `false`.

### Entfernen von Leerzeichen

`chapter` -> `<chapterid>` -> `solution` -> `strip_whitespaces`

Leerzeichen innerhalb von Eingaben werden entfernt (`true`) oder wie vom Spielenden eingeben behalten (`false`). Standardeinstellung ist `false`.

## Punktesystem

### Minimale und maximale Punktestände

Für eine Geschichte können minimale und maximale Punktestände definiert werden, die nicht unter- bzw. überschritten werden können. Diese Angabe erfolgt in der `story.json` unter `point_limits` -> `min`, sowie `point_limits` -> `max`.

Während die Spielenden Punkte erspielen kann der Punktestand durch verschiedene Aktionen unter bzw. über diese Definitionen gelangen. In diesem Fall wird der Punktestand auf das angegebene Limit begrenzt und der anzuwendende (und alle späteren) Aktionen , die zu einer Unter- oder Überschreitung führen, nicht gewertet. Der anzuwendende Malus oder Bonus wird auf den (Teil-)Wert reduziert, der zum Erreichen den Limits ausreicht. Ist das Limit bereits erreicht, wird der Malus bzw. Bonus auf den Wert Null reduziert.

### Punkte für Aktionen

Innerhalb von Geschichten können Punkte für bestimmte Aktionen vergeben werden.

- Das erreichen eines Kapitels (meistens Bonus)
- Das Nutzen von Hinweisen (meistens Malus)
- Die Eingabe von nicht korrekten Lösungen (meistens Malus)

Diese Malus- und Bonus-Werte können über folgende Einstellungen innerhalb der `story.json` unterhalb einer für eine angegebene `chapterid` definiert werden. Punkte verändern sich in der Regel nur beim ersten Auftreten des Ereignis, so dass den Teams kein Nachteil durch spätere Aufrufe oder Vorteile durch wiederholte Aufrufe entstehen. Ausnahme ist die inkorrekte Eingabe von Lösungen, die durch jeden Spielenden jederzeit erfolgen können.

Bonuspunkte werden mit positiven Werten (zum Beispiel 1,4,8,100) angegeben, Maluspunkte mit negativen Werten (zum Beispiel -1, -4, -8, -100).

### Eintritt in Kapitel

`chapter` -> `<chapterid>` -> `points` -> `enter`

Der angegebene Wert wird auf den aktuellen Punktestand angewendet, wenn das erste Spielende des Teams das unter `<chapterid>` angegebene Kapitel erreicht. Nachfolgende Spielende verändern den Punktestand nicht.

### Abruf von Hinweisen

`chapter` -> `<chapterid>` -> `points` -> `hints` -> `<hintid>` ...

Für die Nutzung des Hinweises `<hintid>` wirr der angegebene Wert auf den aktuellen Punktestand angewendet. Ist kein Wert in der `story.json` für einen existierenden Hinweis `<hintid>` angegeben, wird der in der angewendeten `quest.json` zu der `<hintid>`angegebene Punktewert auf den Punktestand angewendet. 

Die Ziffer 0 als Wert bewirkt, dass der Hinweis kostenfrei erhalten wird und dadurch keine Anzeige einer Abfrage dem Anwender angezeigt wird. Die Anzeige erfolgt jedoch, sollte `solution:true` für einen Hinweis angegeben sein.

Ergänzend kann der Wert `null` angegeben werden, um die Punkte für einen Hinweis aus der `quest.json` zu nutzen. Dies kann hilfreich sein, wenn zum Beispiel der erste Hinweis mit `null` definiert wird, der zweite aber nur einem Maluswert. In diesem Fall kann aus die generische Angabe der Maluspunkte durch `nonsolution_hint`/`solution_hint` verzichtet werden.

### Abruf eines Lösungshinweises

`chapter` -> `<chapterid>` -> `points` -> `nonsolution_hint`

Ist der Wert `nonsolution_hint` angegeben, wird für einen Hinweis, für den nicht `solution: true` (entweder ist der Parameter nicht angegeben oder explizit auf `false` gesetzt) angegeben wurde, dieser Wert auf den Punktestand angewendet. Diese Angabe überschreibt alle übrigen Punkteangaben aus der `quest.json` und der `story.json`.


`chapter` -> `<chapterid>` -> `points` -> `solution_hint`

Ist der Wert `solution_hint` angegeben, wird für einen Hinweis, der mit `solution: true` angegeben wurde, dieser Wert auf den Punktestand angewendet. Diese Angabe überschreibt alle übrigen Punkteangaben aus der `quest.json` und der `story.json`.

### Eingabe einer inkorrekten Lösung

`chapter` -> `<chapterid>` -> `points` -> `incorrect_solution`

Der Wert unter `incorrect_solution` wird immer dann angewendet, wenn ein Spielender des Teams eine inkorrekte Lösungseingabe vornimmt. Diese wird für das gesamte Team gewertet und kann beliebig oft durch jedes Teammitglied erfolgen. Dies birgt die Gefahr, den Punktestand ohne Kenntnis der anderen Teammitglieder zu verändern.

## Timer

In einem Chapter kann ein Timer für das Lösen der Quest angegeben werden. Dieser Timer wird als überlagernder Dialog in der oberen rechten Ecke des Browser-Fensters angezeigt. Folgende Einstellungsmöglichkeiten gibt es:

| Parameter     | Standard          | Beschreibung |
| ------------- |:-------------:| :----------- |
| show | true | Definiert, ob der Timer dem Benutzer angezeigt werden soll. |
| delay | 0 | Verzögert den Start des Timers um die angegebene Anzahl Minuten. Um eine Verzögerung unter einer Minute zu erreichen ist ein Wert zwischen 0 und 1 anzugeben.  |
| init_sound | ... | Gibt die Audio-Datei an, die bei Start des Timers (nach dem Delay) abgespielt werden soll. |
| tick_sound | ... | Gibt die Audio-Datei an, die in der Warnphase jede Sekunde abgespielt werden soll. |
| minutes | ... | Definiert die Anzahl der Minuten, die der Timer (Countdown) umfassen soll. |
| next | ... | Definiert das Kapitel, welches bei Ablauf des Timers aufgerufen werden soll. |


## Platzhalter

**HINWEIS**: Platzhalter können sowohl in Story als auch Event eingesetzt werden. Platzhalter implementieren Features in eine `Story` oder eine `Quest`.

### Grundsätzlicher Aufbau

#### {file: }

Der angegeben Dateinamen wird geladen und anstelle des Platzhalters `file` als Ausgabe festgelegt. Wird der Platzhalter in einem anderen Text eingebettet, wird der geladene Text in den Text eingefügt.

Beispiel:  
> {file:output.html}

#### {variable: }

Mit dem Platzhalter `variable` können Inhalte aus der Event-Definition in die Ausgabe eingebracht werden. Hierbei wird zuerst versucht die Variable aus der Team-Definition (event.json->team->teamcode->variables->`variable`:`inhalt`) zu ermitteln. Wenn dies nicht erfolgreich ist, wird die Variable versucht aus der Event-Definition (event.json->variables->`variable`:`inhalt`) zu ermitteln.

Der Platzhalter `{variable:master}` bewirkt, dass die Variable `master` gesucht wird und der gesamte Platzhalter ({...}) mit dem Inhalt `inhalt` ersetzt wird.

##### Vordefinierte (interne) Variablen
Ergänzend zu den eigendefinierten Variablen sind auch interne Variablen definiert. Diese internen Variablen sind reservierte Begriffe, die nicht durch eigene Variablennamen ersetzt werden können.

| Variable | Beschreibung | Gültig für |
| ------------- |:------------- | :------------ |
| eventid | Event ID | event |
| storyid | Story ID | story |
| questid | Quest ID | quest |
| team_points | Punktestand des Teams | story |
| team_points | Punktestand des Teams | story |
| team_chapters | Absolvierte Kapitel des Teams | story |
| team_solutions | Gesamtanzahl der bisher eingegebenen Lösungsversuche des Teams | story |
| team_hints | Gesamtanzahl der in Anspruch genommenen Hinweise des Teams | story |
| team_time | Spielzeit des Teams (im Format hh:mm:ss). Es wird nur die beste Zeit des Teams gewertet, d.h. spätere oder wiederholte Aufrufe von Kapiteln werden nicht gewertet | story |
| teamcode | Teamcode des Teams | story |
| teamname | Name (Bezeichnung) des Teams | story |
| public_teamscodes | Listet alle öffentlichen Teamcodes auf (funktioniert auch in event.json => registration => body) | story, event |
| path_story | Pfad zum aktuellen Story-Verzeichnis | story |
|path_quest | Pfad zur aktuellen Quest | quest |
|solution | Lösung der Quest (erster Eintrag der Liste) | quest |

##### Sub-Variable

Eine Sub-Variable wird als `[...]` innerhalb einer Variablen-Ersetzung angegeben. So können verschachtelte Variablen eingesetzt werden, die sich anhand des Wertes anderer Variablen ergeben. Als Beispiel sei eine Variable genannt, die im Laufe der Geschichte aktualisiert wird, im Inhalt aber eine feste Definition als Variable angegeben wurde. Beispiel:

```
...
"chapter" = "1",
"content_chapter" = "%%%variable:content_[chapter]%%%"
"content_1": "This is chapter %%%variable:chapter%%% and you have started your journey",
"content_2": "This is chapter %%%variable:chapter%%%. You have reached the next chapter",
"content_3": "This is the last chapter %%%variable:chapter%%%. You have finished your journey",
...
```

Die Variable `chapter` wird während des Fotschritts aktualisiert (z.B. durch `action`) und verändert dadurch die Variable `content_chapter`. Diese wiederum bewirkt durch die Angabe einer Sub-Variable, dass je nach Inhalt der Variable `chapter` entweder die Inhalte aus Variable `content_1`, `content_2` oder `content_3`  eingesetzt werden.


## Medieninhalte

Die unterschiedlichen Medieninhalte können durch einen Platzhalter eingebettet werden. Das Format lautet:

[image|video|audio|...:{parameter1:value1}{parameter2:value2}...{parameter:value}]

Die Einleitung der Formats bestimmt, welche Inhalte und Funktionen in die Ausgabe an der Stelle der Definition eingebettet wird. Ebenso sind durch die Wahl des Medienformats die Anzahl und die Art der Parameter bestimmt. Werden Parameter angebene, die nicht für die Mediendatei anwendbar sind oder nicht als Parameter gültig sind, werden diese ignoriert.

Grundsätzlich muss sich die Mediendatei innerhalb der Story-Definition befinden und wird von dort eingebettet.

### Vorbedingungen

#### precondition

Bedingungen zur Anzeige einer Mediendatei können über den Parameter `{precondition:<chapter>,<chapter>,...}`angegeben werden. <chapter> beschreibt dabei den internen Namen eines ein Kapitels, welches erreicht/gespielt worden sein muss. Ist dieses Kapitel noch nicht erreicht worden, ist die Voraussetzung nicht erfüllt und die Mediendatei wird nicht eingebunden. Durch die Angabe mehrere Kapitel müssen alle angegebenen Kapitel erreicht worden sein, damit die Mediendatei eingebettet wird.

#### precondition-none

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

#### precondition-one (noch nicht implementiert!)

Eine `precondition-one` Bedingung zeigt die Mediendatei an, sobald eines der angegebenen Kapitel gespielt wurde.

#### precondition-none-all (noch nicht implementiert!)

Die `precondition-none` Bedingung definiert, dass die Mediendatei nicht angezeigt wird, sobald alle der angegebenen Kapitel gespielt wurden. Diese Bedingung muss für alle angegeben Kapitel zutreffen, damit die Grafik nicht angezeigt wird. Dies kann beispielsweise hilfreich sein, wenn mit anderen `precondition` Bedingungen eine alternative Grafik angezeigt werden soll.

Folgende Medienformate werden unterstützt:

### [image: ...]

Es wird eine Bilddatei eingebunden.

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| description | ... | Beschreibung der Bilddatei |
| id | ... | ID der Bilddatei (ist unter anderem für den `magnify` Platzhalter erforderlich) |
| width | ... | Breite der Bilddatei |
| credits | ... | Hinweise zu Autoren oder Copyrights |
| vignette | true, false | Gibt an, ob das Bild mit einer Vignette angezeigt werden soll |
| optimize | true, false | Gibt an, ob das Bild für Geräte mit geringeren Bildschirmauflösungen optimiert werden soll. Standardeinstellung ist `true`. Die Optimierung kann bewusst mit angabe `{optimize:false}` ausgeschaltet werden. |

Für die Grafiken können ergänzend zu der Originalversion auch Varianten mit unterschiedlichen Pixelbreiten bereitgestellt werden, die auf Geräten bereitgestellt werden, deren maximale Bildschirmbreite den nachfolgenden Angaben entspricht. Dem Dateinamen wird die Pixelbreite angefügt. Die Angaben beziehen sich auf eine beispielhafte Datei mit der Dateinamen-Angabe `quest.png`:

| Maximale Bildschirmbreite | Pixelbreite Bild | Dateiname (Beispiel) |
| ------------- |:-------------:| :----------- |
| 1200 | 1140 | quest1140.png |
| 992 | 960 | quest960.png |
| 768 | 720 | quest720.png |
| 576 | 540 | quest540.png |

Überschreitet die Bildschirmauflösung die hier angegebenen höchten Wert, wird die ursprünglich angegebene Grafikdatei vom Broweser des Nutzenden geladen und dargestellt. Der Browser des Nutzenden entscheidet dann, welche der Grafiken geladen wird. In jedem Fall steht die ursprünglich angegebene Datei bereit, so dass immer eine Grafik angezeigt werden sollte.

Die Dateien werden in der bereitgestellten HTML-Code nur eingebunden, sofern diese als Datei bereitstehen. Diese Optimierung kann bewusst durch den Bereitsteller durch Angabe `optimize:false` ausgeschaltet werden.

### [audio: ...]

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


### [video: ...]


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


### [handout: ...]

Der Platzhalter `handout` stellt ein angegebenes Dokument als Download-Link dar. Das Dokument wird als Link, welcher sich in einem gesonderten Fenster öffnent, dargerstellt.

**HINWEIS**: Über die Option `merge` stellt der Platzhalter `handout` ein PDF dar, welches sich aus der Story und den in der `Story` referenzierten `Quests` die jeweiligen Handouts ermittelt und in einem dynamisch zusammengesetzten Handout bereitstellt. Dadurch können Handout-Informationen (z.B. Teile eines Rätsels) zu der jeweiligen Quest angegeben werden, die dann gesamtheitlich bei Start eines Spiels dem Spieler als Download angeboten werden. Die Handouts werden dynamisch auf Basis einer eindeutigen ID zum Download angeboten. Die Erzeugung der Handout-Datei und ihrer ID erfolgt immer sobald sich der Umfang der einzubindenden Dateien oder der Inhalt einer der eingebundenen Dateien ändert. Sind die Inhalte unverändert, erfolgt keine Neuerzeugung der zum Download angebotenen Handout-Datei. Diese steht damit dann umgehend zum Download zur Verfügung.

Werden keine Handout-Dokumente oder -Bestandteile gefunden oder enthält das zusammengesetzte Dokumente keine Seiten, wird die Datei nicht zum Download angeboten und der Platzhalter aus der Anzeige gelöscht.

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| description | ... | Die Description beschreibt den angezeigten Text für den Download-Link der PDF-Datei. Diese Angabe wird in den Metadaten der PDF auch für den Titel und das Thema gesetzt. |
| credits | ... | Die Credits beschreiben in den Metadaten der PDF den Author. |
| type | pdf | Gibt an, welchen Typ die angezeigte Mediendatei haben soll. Hier wird bisher nur PDF unterstützt. |
| merge | true | Gibt an, ob aus referenzierten Quests der Story die in den Quest-Verzeichnissen enthaltenen `handout.pdf` in einer PDF-Datei zusammengetragen werden sollen. Ist in der Story ebenfalls eine `handout.pdf` enthalten, wird diese als Deckblatt verwendet. Die Handouts der `Quest` werden nach dem Deckplatt in der Reihenfolge ihrer Einbindung in der `Story` integriert. Ist in der Story zudem eine `handout_last.pdf` oder alternativ eine `handout_end.pdf` Datei enthalten, wird diese am Ende des zusammengestellten PDF eingefügt. Dies kann zum Beispiel für Abschlussseiten mit Adress-, Kontakt- oder Copyright-Angaben genutzt werden. |
| icon | true | Zeigt das Icon standardmäßig für das Handout an. Die Anzeige des Icon kann mit `false` ausgeblendet werden. |

### [playarea: ...]

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


### [voice: ...]

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

### [fetch: ...]
  
Mit dem Fetch-Platzhalter werden alle Teammitglieder zu dem aktuellen Kapitel geholt, in dem sich der aufrufende Spielende befindet. Dadurch können Teammitglieder, die eine Quest nicht lösen können oder verspätet dem Spiel beitreten, zum aktuellen Kapitel geholt werden. Diese Funktion ist nur für Teammitglieder funktionsfähig, die sich mit dem identischen Teamcode registriert haben.
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| label | ... | Beschriftung des Links |

### [html: ...]
  
Mit dem `html`-Platzhalter wird HTML-Code in die Seite eingebunden. 
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| content | ... | HTML-Code |
| filename | ... | Lädt eine externe Datei mit dem HTML-Code |
| raw | false | definiert, dass der HTML-Code im Rohformat dargestellt wird |
| replace | true | Ersetzt im HTML-Code enthaltene Platzhalter |
| storyfallback | true | Prüft, ob ion einer Quest alternativ nach der unter `content` angegebenen Datei in der Story gesucht werden darf. Falls dies nicht gewünscht ist, muss explizit `false` gesetzt werden! |


### [link: ...]
  
Mit dem `link`-Platzhalter wird ein HTML-Link in die Seite eingebunden. 
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| url | ... | URL des Links bzw. der Grafik (bei lightbox=true) |
| description | ... | Test des HTML-Links |
| target | _blank | Ziel-Frame des Browsers, in dem der Link geöffnet werden soll |
| lightbox |false | Bei Links oder Grafiken werdne diese in einer Bootstrap Lightbox (Dialog) angezeigt |


### [markdown: ...]
  
Mit dem `markdown`-Platzhalter wird Markdown-Code in die Seite eingebunden. 
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
| content | ... | HTML-Code |
| filename | ... | Lädt eine externe Datei mit dem HTML-Code |
| raw | false | definiert, dass der HTML-Code im Rohformat dargestellt wird |
| replace | true | Ersetzt im HTML-Code enthaltene Platzhalter |

Weitere Details über den Syntach können beispielsweise über die externe Übersicht bei [Daring Fireball](https://daringfireball.net/projects/markdown/syntax) als Syntax-Referenz eingesehen werden.

### Lobby

Der Lobby-Modus ermöglicht die Spielenden nach der Registrierung in einem gemeinsamen Raum (Kapitel) warten zu lassen. Erst wenn ein Lobby-Administrator die Lobby auflöst, werden alle Teilnehmer automatisch zu dem ersten Kapitel der Story geleitet.

Die Definitionen für die iNhalte der Lobby lehnen sich an das Format der Inhaltsdefinitionen eines Kapitels an und werden in dem Zweig `lobby`-> `content` der `story.json` definiert. Die unter diesem Pfad enthaltenen Schlüssel-Wert-Paare werden dynamisch gelesen und in die entsprechenden Platzhalter der Templates eingefügt.

Bekannte Platzhalter sind:

| Platzhalter     | Beschreibung  |
| ------------- |:-------------:|
| header | Titel im Kopfbereich |
| title | Titel im Inhaltsbereich |
| body | Inhalt der Seite |

Die Inhalte der Platzhalter werden gelesen und Platzhalter (u.a. Variablen oder dynamische Median-Inhalte) ersetzt.

### [confetti: ...]
  
Mit dem Confetti-Platzhalter werden Konfetti-Partikel nach Anzeige der Website angezeigt. Die Darstellung kann mit folgenden Parametern angepasst werden: 
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
|particleCount|50|Anzahl der Konfettis, mit denen gestartet werden soll
|angle|90|Winkel, mit denen die Konfettis gestartet werden sollen. 90 Grad meint direkt nach oben.|
|spread|45|How far off center the confetti can go, in degrees. 45 means the confetti will launch at the defined angle plus or minus 22.5 degrees.|
|startVelocity|45|Angabe in Pixel, wie schnell die Konfettis vom Startpunkt aus starten.|
|decay|0.9|How quickly the confetti will lose speed. Keep this number between 0 and 1, otherwise the confetti will gain speed. Better yet, just never change it.|
|gravity|1|Angabe, wie schnell die Partikel sich absenken. 1 meint volle Gravitation, 0.5 meint halbe GRavitation, etc.|
|drift|0|Angabe, wie stark zur Seite die Konfettis abdriften. Der Standard ist 0, was angibt, dass die Partikel direkt nach unten fallen. Negative Nummern  für Links und positive Nummer für rechts.|
|ticks|200|How many times the confetti will move. This is abstract... but play with it if the confetti disappear too quickly for you.|
|originx|0.5|Die x-Position auf der sichtbaren Seite, wobei 0 den linken Rand und 1 den rechten Rand meint. Angaben außerhalb dieses Bereichs möglich.|
|originy|0.5|Die y-Position auf der sichtbaren Seite, wobei 0 den oberen Rand und 1 den unten Rand meint. Angaben außerhalb dieses Bereichs möglich.|
|colors|Array<String>|An array of color strings, in the HEX format... you know, like ['#bada55', '...'].|
|shapes|Array<String>|An array of shapes for the confetti. The possible values are square and circle. The default is to use both shapes in an even mix. You can even change the mix by providing a value such as ['circle', 'circle', 'square'] to use two third circles and one third squares.|
|scalar|1|Scale factor for each confetti particle. Use decimals to make the confetti smaller. Go on, try teeny tiny confetti, they are adorable!|
|zIndex|100|The confetti should be on top, after all. But if you have a crazy high page, you can set it even higher.|
|disableForReducedMotion|false|Disables confetti entirely for users that prefer reduced motion. The confetti() promise will resolve immediately in this case.|
  

### [snow: ...]
  
Mit dem Snow-Platzhalter werden Schneeflocken zur Anzeige der Website angezeigt. Die Darstellung kann mit folgenden Parametern angepasst werden: 
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
|particleCount|200|Anzahl der Schneeflocken, mit denen gestartet werden soll. Mit der Anzahl der Partikel erhöht sich die Belastung auf den anzeigenden Systemen. Es wird empfohlen, die Anzahl NICHT über 300 einzustellen!
  
### [link: ...]
  
Mit dem Link-Platzhalter wird ein Link dargestellt, der die angegebene URL in einem separaten Fenster aufruf. Vor dem Link ist ein Icon eingeblendet, um den Aufruf eines externen Links deutlich zu machen.
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
|url|$|Link, der aufgerufen werden soll|
|description|$|Beschreibung, die für den Link angezeigt werden soll. Wenn diese Angabe fehlt, wird anstelle dessen die Angabe unter ?url` verwendet|
|target|$|Name des Zielfensters, das bei Aufruf der `url` verwendet werden soll. Sofern diese Angabe fehlt oder leer ist, wird `_blank` verwendet|
|class|$|CSS-Klasse, die bei Anzeige des Links verwendet werden soll|

### [magnify: ...]
  
Mit dem `magnify` Platzhalter wird auf einer angegeben Bilddatei eine Lupen-Funktion angeboten, mit der Teile der Bilddatei vergrößert dargestellt werden können. Mit Hilfe des Mausrads besteht zudem die Möglichkeit den vorgegebenen Zoom-Level zu verändern (bei `wheelsupport:true`). Die Zu Grunde liegende Bilddatei sollte größer dimensioniert sein, damit der höhere Zoom weniger Pixelfragmente darstellt.
  
| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
|target|$|ID der Bilddatei, für die der Effekt angezeigt werden soll (`id`-Parameter des `image` Platzhalter|
|scale|#|Zoom-Level, der initial verwendet werden soll|
|width|#|Breite der Lupe in Pixel|
|height|#|Höhe der Lupe in Pixel|
|wheelsupport| true, false |Gibt an, ab das Mausrad zum Ändern der `scale` genutzt werden darf. Default: false.|

### [action: ...]

Mit dem `action` Platzhalter können aus dem Inhalt heraus Aktionen ausgeführt werden. Es wird nur der Einsatz bestimmer Funktionen empfohlen, da mit der Ausführung bestimmter Aktionen sich ein unerwünschtes Verhalten ergeben kann (z.B. Redirects durch eine so eingebettete `action`). Aktionen werden in der Reihenfolge des Erscheinens ausgeführt.

Beispiel: Beispielsweise können Abfragen aif Platzhalter auf den Wert einer Variable durchgeführt werden, die im folgenden Code dann dann durch diesen Platzhalter `action` zurückgesetzt wird. Dies hätte zum Beispiel zur Folge, dass die Abfrage nur einmal ausgeführt werden kann.

| Parameter     | Wert          | Beschreibung |
| ------------- |:-------------:| :----------- |
|name|$|Name der auszuführenden Aktion|
