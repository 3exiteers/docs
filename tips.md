# Tipps & Tricks

## Inhalt bei Erreichen eines Fortschritts

### Annahme

Der Inhalt eines Formats kann dynamisch gesteuert werden, in dem Variablen und bedingte Inhalte angewendet werden. Soll zum Beispiel der Inhalt bei erreichen eines Kapitels abhängig von den zuvor gelösten Aufgaben angezeigt werden, kann dies über zwei Wege erreicht werden: `junction` im Navigationsbereich und/oder `preconditions` im Inhaltsbereich.

### Genutzte Funktionen

- Setzen von Variablen über `action`
- Inhalte anzeigen über `html` mit Option `precondition`
- Setzen von Variablen über `variable`
- Anzeige von Navigation über `junction` (optional)

### Vorgehen

- Innerhalb der Geschichte wird eine `quest` durch den Spielenden erreicht
- in dem Kapitel wird als `next` Angabe eine `action` angegeben
- wird die Aufgabe der Quest durch den Spielenden gelöst, wird die `action` ausgelöst
- innerhalb der `action` wird eine Listen-Variable (`list add unique`) gesetzt, die der Quest entspricht (z.B. Quest-Nummer)
- für das Beispiel wird die Liste `quest_finished` angenommen
- Der Befehl würde demnach lauten: `list add unique: quest_finished = 1`
- durch den Zusatz `unique` wird sichergestellt, das mehrmaliges Aufrufen und Lösen der Quest (z.B durch andere Teammitglieder) nicht zu doppelten Einträgen in der Liste führt
- dieses Vorgehen wird bei verschiedenen anderen Quests umgesetzt, die jeweils ihren eigen Inhalt zu der Liste hinzufügen
- sollen nun Inhalte vom erreichten Fortschritt (hier: Anzahl der erfolgreich gelösten Aufgaben) angezeigt werden, muss lediglich die Länge der Liste geprüft werden
- sind beispielsweise fünf (5) Quests in der Geschichte enthalten, wäre auf die Länge fünf (5) zu prüfen
- für eine bedingte Anzeige (hier: über das `html` Feature) wäre der Befehl ```[html:{precondition-list-len:quest_finished -eq 5}{filename:all_quests_finished.txt}]``` zu nutzen
- über das `html` Feature könnend ie Spielenden über HTML-Inhalte - idealerweise ebenso über die Referenzierung auf eine `action` - zu dem gewünschten Kapitel gelenkt werden

## Inhalte für bestimmte Teams anzeigen

### Annahme 

tbc (Funktion Teamcode als Variablen inhalt prüfen/implementieren, Abfrage auf Teamcode/Rolle/Recht oder in Geschichte erreichte Eigenschaft)

### Genutzte Funktionen

tbc

### Vorgehen

tbc

## Inventar nutzen

### Annahme

Für ein Format soll ein Inventar genutzt werden, welches durch das Lösen der Aufgaben aufgebaut wird. So können beispielsweise bestimmte Gegenstände erspielt werden, die entweder Voraussetzung für andere Aufgaben oder das Voranschreiten im Spiel sein können. Das Inventar hat die Eigenschaft, dass Gegenstände hinzugefügt, benutzt und wieder entfernt werdden können.

### Genutzte Funktionen

- Setzen von Variablen über `action`
- Setzen von Variablen über `variable`
- Inhalte anzeigen über `html` mit Option `precondition`
- Abfragen über `precondition-list-in` und `precondition-list-nin`

### Vorgehen

In einem Kapitel ist bei Lösen einer Aufgabe im Feld `next` die entsprechende `action` anzugeben, in der das Inventar über die Funktion `list add unique: inventory = doorkey` gesetzt wird. In unserem Beispiel wird ein Türschlüssel mit der Bezeichnung `doorkey` gesetzt. Der Parameter `unique` sorgt dafür, dass der Eintrag in der List nur einmal hinterlegt wird, so dass durch mehrere Aufrufe (z.B. durch andere Teammitglieder) dieser lediglich einmal vorhanden ist. Im späteren Verlauf wird eine Schaltfläche zum Öffnen der Tür mittels der `html` Funktion eingeblendet, um die Tür durch den Spielenden Öffnen zu können: 

```[html:{precondition-list-in:inventory = doorkey}{filename:open_door.txt}]```

Soll hingegen ein alternativer Inhalt eingeblendet werden, der erscheint, solange der Türschlüssel nicht im Inventar liegt, ist folgender Inhalt anzugeben (beide Fälle abgedeckt): 

```
[html:{precondition-list-nin:inventory = doorkey}{filename:missing_key.txt}]
[html:{precondition-list-in:inventory = doorkey}{filename:open_door.txt}]
```

## Eigene Navigation implementieren

### Annahme

Die Schaltflächen zur Navigation zwischen den Kapiteln sind durch das Framework bzw. die Templates und Stylesheets definiert. Möchte ein Content Creator eigene Möglichkeiten nutzen, zwischen den Kapiteln zu navigieren oder andere Ziele erreichen, kann dies über eigenen HTML-Code und die Nutzung von `action` erreicht werden. In diesem Beispiel wird die Anzeige von Nutzungshinweisen angenommen, die auf jeder Seite des Formats angezeigt und durch den Spielenden als gesonderte Seite aufgerufen werden sollen

### Genutzte Funktionen

- Setzen von Variablen über `action`
- Setzen von Variablen über `variable`
- Anzeige von HTML-Inhalten über `html` mit Option `precondition`

- !!! Letztes aufrufende Kapitel als Variable speichern, hier ggf. auch Spieler-beziogene Variablen ermöglichen, die unabhängig vom Team sind, um so den Rücksprung durch den Aufruf durch verschiedene Spielende an verschiedenen Stellen nicht zu verändern

### Vorgehen

tbc

## Teamcodes automatisch erzeugen

### Annahme

Für ein Event soll eine eindeutige URL vergeben werden, die (öffentlich) verteilt werden soll. In diesem Fall sind Schnell-Links (`quicklinks`) nicht nutzbar, da diese den Teamcode enthalten. Ein generischer Teamlink hat aber den Nachteil, dass alle Nutzenden als ein Team spielen. Daher soll die Funktion `generator` genutzt werden, die aus einem generischen Teamcode einen individuellen Teamcode erzeugt, der den Spielenden dann wieder ermöglicht, als eigenees Team zu spielen.

### Genutzte Funktionen

tbc

### Vorgehen

tbc