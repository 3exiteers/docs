# Tipps & Tricks

## Inhalt bei Erreichen eines Fortschritts

Der Inhalt eines Formats kann dynamisch gesteiuert werden, in dem Variablen und bedingte Inhalte angewendet werden. Soll zum Beispiel der Inhalt bei erreichen eines Kapitels abhängig von den zuvor gelösten Aufgaben angezeigt werden, kann dies über zwei Wege erreicht werden: `junction` im Navigationsbereich und/oder `preconditions` im Inhaltsbereich.

Genutzte Funktionen:
- `action`
- Feature `html` mit Option `precondition`
- `junction` (optional)

Vorgehen:

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

## Inhalte für bestimmte Teams 

tbc