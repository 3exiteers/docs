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

### variable set

```variable set: <Variable>=<Inhalt>```

Mit der Aktion `variable set:<key>=<value>` können Variablen für das Team gesetzt werden. Die Angabe erfolgt dabei unter Angabe eines Variablennamens `<key>` und des zuzuweisenden Wertes `<value>`. Anstelle `variable` kann auch `variables`, `var` oder `vars` verwendet werden.

Beispiel:

`variable clear: variable=value`

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

### report send

Hinweis: Funktion befindet sich in Entwicklung und wird später beschrieben.

