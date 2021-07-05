# Quest

> Quest descriptions.

## Quest Einstellungen

### Mehrere valide Antwortmöglichkeiten

Neben dem Feld `solution` ist die Angabe von mehreren frei einzugebenden Lösungsmöglichkeiten über das Feld `solutions` möglich. Dabei ergänzt `solutions` das Feld `solution` und bildet eine Liste von möglichen Eingabewerten. Dies kann zum Beispiel bei nicht eindeutigen Lösungen hilfreich sein, wenn zum Beispiel Operanden einer mathematischen Abfolge oder Singular/Plural nicht eindeutig für den Spieler sind. 

| Parameter     | Standard          | Beschreibung |
| ------------- |:-------------:| :----------- |
| solutions | [...], [...], ... | Angabe einer Liste mit den validen Lösungen. Auf diese Lösungen werden die Regeln zur Harmonisierung angewendet. Durch die Angabe unterschielicher Lösungen können Variationen in der Lösung abgefangen werden, ohne das die exakte Schreibweise (z.B. bei mathematischen Operationen) strikt eingehalten werden müssen. |

### Optionen: Auswahl möglicher Antworten

Dem Spieler kann eine vorgegeben Auswahl von Antworten bereitgestellt werden, aus denen die richtige Antwort ausgewählt werden muss. Die Angabe erfolgt in dem Feld `solution`einer Quest.

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

