# Quest

> Quest descriptions.

## Quest Einstellungen

### Mehrere valide Antwortmöglichkeiten

Die Angabe von mehreren frei einzugebenden Lösungsmöglichkeiten zu einer Quest erfolgt über das Feld `solutions`. Dies kann zum Beispiel bei nicht eindeutigen Lösungen hilfreich sein, wenn zum Beispiel Operanden einer mathematischen Abfolge oder Singular/Plural nicht eindeutig für den Spieler sind. 

| Parameter     | Standard          | Beschreibung |
| ------------- |:-------------:| :----------- |
| solutions | [..., ..., ...] | Angabe einer Liste mit den validen Lösungen. Auf diese Lösungen werden die Regeln zur Harmonisierung angewendet. Durch die Angabe unterschiedlicher Lösungen können Variationen in der Lösung abgefangen werden, ohne das die exakte Schreibweise (z.B. bei mathematischen Operationen) strikt eingehalten werden müssen. |
| body | ... | Bereich für Angaben zur Anzeige der Herausforderung |

### Inhalte der Anzeige

Für die Anzeige der Inhalte der Herausforderung wird der Abschnitt `content` genutzt, der verschiedene Unterelemente verwendet. Notwendig ist nur `body` um die Aufgabe dem Spielenden zu präsentieren. Die übrigen Angaben sind optional und brauchen nicht angegeben zu werden. Es wird empfohlen, nicht benötigte ELemente nicht anzugeben, um so die Komplexität für den Spielenden gering zu halten und Standards zu nutzen.

| Parameter     | Standard          | Beschreibung |
| ------------- |:-------------:| :----------- |
| body | $ | Inhalt der Herausforderung |
| solutiontitle | $ | Überschrift des Eingabefeldes für die Lösung |
| solutionplaceholder | $ | Platzhalter im Eingabefeld für die Lösung (wird bei Eingabe durch Spielenden überschrieben) |

### Hinweise zu Herausforderungen

Zu Herausforderungen können Hinweise angegeben werden, die von den Spielenden bei Bedarf abgerufen werden können. Die Einstellungen werden unter dem Knoten `hints` -> `<hintid>` vorgenommen. `<hintid>` ist dabei eine fortlaufende eindeutige ID des Hinweises, der die Reihenfolge der Hinweise beschreibt. Folgende Einstellungen werden unterstützt: 

| Parameter     | Standard          | Beschreibung |
| ------------- |:-------------:| :----------- |
| text | $ | Hinweistext |
| points | # | Punkte, die der Hinweis kostet (Malus=negative Nummer, Bonus=positive Nummer) |
| supportlevel | 0|1|2|3 | Level der Unterstützung des Hinweises (0=keine Unterstützung, 1=geringe Unterstützung, 2=hohe Unterstützung, 3=sehr hohe Unterstützung)  |
| solution | true|false | Angabe, ob Hinwies die Lösung offenbart |

**Hinweis**: Wird `solution:true` angegeben, wird beim Abruf dieses Hinweise der Spielende darauf hingewiesen, dass bei Anzeige des Hinweises die Lösung offenbart wird.

#### Lösungstext

In dem Parameter `text` kann die Variable `%%%variable:solution%%%` genutzt werden, um den ersten Eintrag aus der Option `solutions` anzuzeigen.

### Optionen: Auswahl möglicher Antworten

Dem Spieler kann eine vorgegeben Auswahl von Antworten bereitgestellt werden, aus denen die richtige Antwort ausgewählt werden muss. Die Angabe erfolgt in dem Feld `solutions`einer Quest.

Beispiel:

> #options:[{value:value1}{label:Option #1}{solution:true},
> {value:value2}{label:Option #2},{value:value3}{label:Option #3},
> {value:1234}{label:Option #4}{solution:true}]


In dem oben dargestellten Beispiel sind die Auswahlmöglichkeiten `Option #1`und `Option #4` richtig. Dies wird durch die Kennzeichnung `{solution:true}` deutlich gemacht. 

Folgende Angaben sind erforderlich/möglich:

| Parameter     | Standard          | Beschreibung |
| ------------- |:-------------:| :----------- |
| value | ... | Gibt den Lösungswert dieser Option an.  |
| label | ... | Gibt die Beschriftung der Auswahl an |
| solution | false | Gibt an, ob dieses Elemente eine gültige Lösung (`solution:true`) darstellt. Entspricht diese Option keiner richtigen Lösung, kann die Angabe von `solution` auch entfallen.|

Die Lösung kann innerhalb eines Tipps mit dem Platzhalter `%%%variable:solution%%%` dynamisch eingebettet werden. Der Platzhalter wird mit dem ersten Elemente der Liste gültiger Lösungen aus dem Feld `solutions:[...,...]` ersetzt. Diese Variable ermöglicht eine gleichbleibende Definition über verschiedene Quests, in der lediglich eine valide Lösungsoption dargestellt wird.