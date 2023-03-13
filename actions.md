# Actions

`Actions` erlauben die Steuerung und Verkettung von internen Aktionen des Frameworks bei Interaktion durch den Spielenden. Es werden dabei alle angegeben Aktionen der Reihe nach abgearbeitet.

## Angabe

`Actions` werden in einem seperaten Block `actions` innerhalb der `story.json` auf erster Ebene angegeben. Die Struktur des Aufgabes lautet `story.json` -> `actions` -> `<Name der Action>` -> `<Liste der Aktionen>`.

```json
{
    "chapters":{
        ...
    },
    "actions": {
        "action01": [
            "action#1",
            "action#2",
            ...,
            "action#999"
        ]
    }
}
```

Es können beliebige viele Aktionen verkettet werden. Die Aktionen werden in der angegebenen Reihenfolge ausgeführt. Die Ausführung wird beendet, wenn keine weizteren Aktionen angegeben sind oder eine Aktion ein sogenanntes STOP-Kommando ist.

### STOP-Kommandos

STOP-Kommandos unterbrechen die Interpretation und Ausführumng von Aktionen. Zumeist ist die Unterbrechung technisch bedingt, wenn zum Beispiel die beim Spielenden dargestellte Website umgebrlendet wird (zum Beispiel Aktion `redirect ...`).

## team

### team lock

Mit der Aktion `team lock:<key>` wird da smit dem Wert `<key>` angegebenen Teamcode gesperrt (`active: false`).

## permission

### permission set

Mit der Aktion `permission set <format>:<key>=<value>` können Rechte für das Team gesetzt werden. Die Angabe erfolgt dabei unter Angabe eines Rechtenamens `<key>` und des zuzuweisenden Wertes `<value>`. Anstelle `permission` kann auch `permissions`, `right`oder `rights`verwendet werden.

`<format>` definiert, in welchem Format der Wert `value` in der Konfiguration gespeichert werden soll. Möglich sind `bool`und `boolean` für boolische Werte, sowie `int` oder `integer` für numerische Werte. Wird keine Angabe zum Format getätigt oder eine andere Angabe, wird `string` angenommen (Default).

Beispiel:

`permission set bool: right=true`

### permission clear

Mit der Aktion `permission clear:<key>` können Rechte für das Team entfernt werden. Die Angabe erfolgt dabei unter Angabe eines Rechtenamens `<key>`. Anstelle `permission` kann auch `permissions`, `right` oder `rights` verwendet werden.

Beispiel:

`permission clear: right`

## variable

### variable init

```variable init: <Variable>=<Inhalt>```

Mit der Aktion `variable init:<key>=<value>` können Variablen für das Team initial gesetzt werden, sollten diese nicht zuvor gesetzt worden sein. Die Angabe erfolgt dabei unter Angabe eines Variablennamens `<key>` und des zuzuweisenden Wertes `<value>`. Anstelle `variable` kann auch `variables`, `var` oder `vars` verwendet werden.

Ist die Variable bereits gesetzt, behölt diese den bereitrs gespeicherten Wert. Nur falls die Variable nicht existiert, wird diese initialisiert. Hierbei muss die Variable für das Team existieren, egal welchen Wert diese zugewiesen bekommen hat (auch eine leere Zeichenfolge ist zulässig).

Beispiel:

`variable init: variable=value`

### variable set

```variable set: <Variable>=<Inhalt>```

Mit der Aktion `variable set:<key>=<value>` können Variablen für das Team gesetzt werden. Die Angabe erfolgt dabei unter Angabe eines Variablennamens `<key>` und des zuzuweisenden Wertes `<value>`. Anstelle `variable` kann auch `variables`, `var` oder `vars` verwendet werden. Die Variable wird in jedem Fall mit dem angegebenen Wert gesetzt.

Beispiel:

`variable clear: variable=value`

### variable set len

```variable set len: <Variable>```

Mit der Aktion `variable set set:<key>=<list>` wird der Wert der Variabölen `key`auf die Länge de rListe der Variable `list` gesetzt. Mit dieser Angabe kann somit die Länge ermittelt und als numerischer Wert in einer Variablen gespeichert werden.

Beispiel:

`variable set len: variable=list` wobei `list` auf `1,3,7,9,10` gesetzt ist

Die Längenbestimmung ermittelt 5 Elemente der Liste `list` und setzt dadurch die Variable `variable`auf den Wert `5`.

### variable increment|inc

```variable increment: <Variable>```

Mit der Aktion `variable increment:<key>` wird der Wert der Variable als numerischer Wert angenommen und dieser um eins (1) im Wert erhöhrt.

Beispiel:

`variable increment: variable`
`variable inc: variable`

### variable decrement|dec

```variable decrement: <Variable>```

Mit der Aktion `variable decrement:<key>` wird der Wert der Variable als numerischer Wert angenommen und dieser um eins (1) im Wert verringert. Es können mit dieser Funktion auch negative Werte berechnet werden.

Beispiel:

`variable decrement: variable`
`variable dec: variable`

### variable dec0

```variable dec0: <Variable>```

Mit der Aktion `variable dec0:<key>` wird der Wert der Variable als numerischer Wert angenommen und dieser um eins (1) im Wert verringert, jedoch nur bis zum kleinsten zulässigen Wert Null (0). Mit dieser Angabe werden keine negativen Werte berechnet.

Beispiel:

`variable dec0: variable`

### variable clear

```variable clear: <Variable>```

Mit der Aktion `variable clear:<key>` können Variablen für das Team entfernt werden. Die Angabe erfolgt dabei unter Angabe eines Variablennamens `<key>`. Anstelle `variable` kann auch `variables`, `var` oder `vars` verwendet werden.

Beispiel:

`permission clear: right`

### list add

```list add: <Variable>=<Inhalt>```

Die Aktion `list add <option>:<key>=<value>` ermöglicht das Hinztufügen eines Wertes zu einer Liste. Das Standardtrennzeichen der Liste ist das Komma `,`, mit dem die Listeinträge voreinander getrennt werden. Wird als `<option>` der Begriff `unique` angegeben, wird der angegebene Wert `<value` nur der Liste `<key>` hinzugefügt, sofern dieser noch nicht enthalten ist.

Beispiel:

`list add [unique]: variable=value`

### list remove

```list clear: <Variable>=<Inhalt>```

Die Aktion `list remove <option>:<key>=<value>` erlaubt das Entfernen des angegeben Listenelements `<value>`aus der Liste `<key>`. Wird `<options>` nicht angeben, wird werden alle Elemente `<value>` aus der Liste entfernt. Dies entspricht der `<option>` von `all`. Alternaiv könenn auch `first` für das erste oder `last` für das letzte Elemente angegeben werden.

Beispiel:

`list remove [all|first|last]:variable=value`

### list clear

```list clear: <Variable>```

Die Aktion `list clear:<key>` erlaubt das Löschen der unter `<key>` angegeben Liste.

Beispiel:

`list clear:variable`

### redirect url

```redirect url: <URL>```

Die Aktion `redirect url:<destination>` leitet des Spielenden auf die unter `<destinaltion>` vollqualifizierten angegeben URL weiter (inkl. Protokollangabe). Die Aktion wird umgehend ausgeführt, so dass weitere Aktionen durch das Verlassen der vom Framework bereitgestellten Inhalte nicht mehr ausgeführt werden. Diese Aktion ist ein sogenanntes STOP-Kommando, das die weitere Verarbeitung der Aktionen abbricht. Es wird daher empfohlen, diese Aktion am Ende einer Liste von Aktionen zu nutzen.

Beispiel:

`redirect url:http://www.google.com`

### redirect chapter

```redirect chapter: <Kapitel>```

Die Aktion `redirect chapter:<destination>` leitet den Spielenden auf das unter `<destination>` angegebene Kapitel um. Dieses Aktion ist ein sogennantes STOP-Kommando, da durch den Wechsel der angezeigten Seite die nachfolgenden Aktionen nicht mehr ausgeführt werden können. Es wird daher empfohlen, diese Aktion am Ende einer Liste von Aktionen zu nutzen.

Beispiel:

`redirect chapter:chapter-01`

### flash (alternativ: flash-dialog, flash-message)

```flash: <Nachricht>```

Diese Aktion sendet eine Nachricht an den aktuellen Spielenden nach dem Laden einer Seite. Typischerweise wird diese Art der Benachrichtigung angewendet, um den Spielden über den Erfolg pder Misserfolg einer Aktion zu informieren. Alternativ können amstelle `flash` auch `flash-dialog` oder `flash-message` genutzt werden. Es können in dem Nachrichtentext auch Variablen verwendet werden.

Beispiel:

`flash: Du hast die Aufgabe '%%%variable:chapter1%%%' erfolgreich gelöst!`


### flash-notification

```flash-notification <Dauer>: <Nachricht>```

Diese Aktion ist eine Unterart von `flash` und sendet eine Nachricht an den aktuellen Spielenden nach dem Laden einer Seite, stellt diese aber als Notification im Popup-Stil dar. Typischerweise wird diese Art der Benachrichtigung angewendet, um den Spielden über den Erfolg pder Misserfolg einer Aktion zu informieren. Es können in dem Nachrichtentext auch Variablen verwendet werden.

Als Parameter kann die Dauer der Anzeige der Benachrichtigung in Milisekunden angebenenm werden. Fehlt diese Angabe, wird der Standardwert von 2500 Milisekunden (2.5 Sekunden) verwendet.

Beispiel:

`flash-notification 5000: Du hast die Aufgabe '%%%variable:chapter1%%%' erfolgreich gelöst!`


### notification (alternativ: broadcast)

```notification <Empfänger>: <Nachricht>```

Diese Aktion `notification (all|team}: <Nachricht>` sendet eine `Nachricht` über eine Benachrichtigung am unteren Bildschirmrand, die nach wenigen Sekunden anzeige verschwindet. Die Benachrichtigung kann dabei an verschidene Spielende gesendet werden: `all` sendet an alle zur Zeit aktivebn Spielenden, `team` sendet an alle Teammitglieder, die den identischen Teamcode nutzen. Der aktuelle Spieler erhält ebenfalls diese Benachrichtigung, so dass dieser ebenfalls informiert wird. Die Nachricht wird bei den Empfänger für 2.5 Sekunden angezeigt.

Beispiel:

`notification team: Ein Spielender hat die Aufgabe '%%%variable:chapter1%%%' erfolgreich gelöst!`

### fetch

```fetch <Empfänger>: <Teamcode>```

Die Aktion `fetch (all|team}: <Teamcode>` holt alle Spielenden in das aktuelle Kapitel des Spielers zusammen, der diese Aktion ausgelöst hat. Die anderen Spielenden laden die aktuelle Adress ein ihrem Browser. Es können mit Angabe `all` alle Spielenden des Events oder mit Angabe `team` die lediglich die Mitglieder der eigenen Teams zu der Adresse geholt werden. 

Hinweis: Wird der Parameter `all` genutzt, ist derzeit noch ein (nicht existenter) Teamcode anzugeben. Diese Angabe wird in späteren Versionen des Frameworks entfallen. Dieser Hinweis wird dann entfernt.

Beispiel:

`fetch all:all`
`fetch team: team1234`

### points

```points add <Modus> <Schlüssel>: <Punkte>```

Die Aktion `points add [(unique|multiple)] <Schlüssel>: <Punkte>` fügt dem Team die angegebenen `<Punkte>` hinzu. Die Punkte werden unter dem Wert `<Schlüssel>` gespeichert. Dieser ist vergleichbar mit dem Namen eines Kapitels und sollte innerhalb der Story eindeutig sein. Wird unter `<Modus>` die Option `unique` angegeben, werden keine Punkte gespeichert, sollte dieser `<Schlüssel>` bereits vorhanden sein. Ist unter `<Modus>` die Option `multiple` angegeben, werden die Punkte bei jeder Ausführung gespeichert. `unique` ist die Standardoption.

Die Punkte werden dem Punktekonto des Teams zugeordnet und bei der Punkteberechnung verwendet.

Hinweis: Die Option `multiple` ist beim Einsatz einer Story mit mehreren Spielenden oder bei häufigen Aufrufen der Aktion mit Vorsicht zu genießen, da die Punkte mehrfach gespeichert werden.

Beispiel:

`points add unique raum1:10`
`points add multiple raum2:11`
`points add raum1: 12`

### database (in Entwicklung)

```database (load|save) (team|player): <Teamcode>|<Spielercode>```

Die Aktion `database` speichert die Variablen des Teams (`team`) oder der Spielers (`player`) in die Datenbank zur Persistierung. Im Modus `load` werden die Angaben gelesen und als Variablen wieder zur Verfügung gestellt. Dieser Mechanismus dient der Sicherung der Variablen, um diese bei einer entwicklungsbedingten Aktualisierung zu persistieren und abrufbar zu gestalten. Die Nutzung ist für den normalen Betrieb eines Spiels nicht zwingend erforderlich, kann jedoch die Nutzererfahrung erhöhen.

Hinweis: Die aus der Datenbank gelesenen Variablen werden den Variablen hinzugefügt. Bestehende Variablen werden überschrieben! Es werden nur vorhandene Variablen im Schreib- oder Lesevorgang verarbeitet.

Hinweis 2: Sofern der Modus `player` verwendet wird kann die Benutzerkennung nur gelsen werden, wenn die Session des Benutzers noch aktiv ist. Sollten zuvor Aktionen wie zum Beispiel `team lock` verwendet worden sein, kann auf die Benutzerkennung nicht mehr zugegriffen werden. Das Speichern ist in diesem Fall nicht möglich.

Hinweis 3: Derzeit ist nur die Option `team` implmenetiert. Die Unterstützung für `player` ist in Vorbereitung (11.2022)

`database save: team`
`database load: player`

### report send

Hinweis: Funktion befindet sich in Entwicklung und wird später beschrieben.

