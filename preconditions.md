# Preconditions

`prconditions` erlauben die Steuerung von Anzeigen über die Abfrage bestimmer Zustände. Es können damit vorrangig mediale Inhalte, die über die Tags `image`, `audio`, oder auch `html` eingebettet sind, steuern.

## precondition-list-len

Über diese Precondition wird abgfragt, ob die Länge der Liste einem bestimmten Längen-Zustand entspricht). Eine Llere Liste entspricht einer Länge von Null (0). Sobald ein Element in der Liste enthalten ist, entspricht die Länge Eins (1). Die Elemente der Liste werden mit Komma voneinander getrennt, so dass Listenwerte mit enthaltenem Komma nicht listen-sicher sind!

### = (-eq)

Es wird geprüft, ob die Länge der Liste dem angegeben Wert entspricht.

Beispiel:

`{precondition-list-len: variable -eq 3}`

### = (-ne)

Es wird geprüft, ob die Länge der Liste nicht dem angegeben Wert entspricht.

Beispiel:

`{precondition-list-len: variable -eq 3}`


### <= (-le)

Es wird geprüft, ob die Länge der Liste kleiner oder gleich dem angegebenen Wert entspricht.

Beispiel:

`{precondition-list-len: variable -le 3}` wird als `variable <= 3` interpretiert

### < (-lt) 

Es wird geprüft, ob die Länge der Liste kleiner dem angegebenen Wert entspricht.

Beispiel:

`{precondition-list-len: variable -lt 3}` wird als `variable < 3` interpretiert


## >= (-ge)

Es wird geprüft, ob die Länge der Liste größer oder gleich dem angegebenen Wert entspricht.

Beispiel:

`{precondition-list-len: variable -ge 3}` wird als `variable >= 3` interpretiert

### > (-gt)

Es wird geprüft, ob die Länge der Liste kleiner oder gleich dem angegebenen Wert entspricht.

Beispiel:

`{precondition-list-len: variable -gt 3}` wird als `variable > 3` interpretiert

### in (-in)

Es wird geprüft, ob die Liste den angegebenen Wert enthält. Diese Prüfung ist eine Ausnahmefunktion, da mit `-in` nicht auf die Länge der Liste abgefragt wird.

Beispiel:

`{precondition-list-len: variable -in 3}` wird als `3 in variable` interpretiert


### not-in (-nin)

Es wird geprüft, ob die Liste den angegebenen Wert nicht enthält. Diese Prüfung ist eine Ausnahmefunktion, da mit `-in` nicht auf die Länge der Liste abgefragt wird.

Beispiel:

`{precondition-list-len: variable -nin 3}` wird als `3 not in variable` interpretiert


## precondition-list

...