# EVENT

> Event descriptions.

## Teamcode

Der Teamcode ist das entscheidende Merkmal für den Zugang der Spielenden zu einem Event. Der Teamcode ist in der Regel ein 8-stelliger alphanumerischer Code, der einen eindeutigen Zugang darstellt. Doppelte Nennungen innerhalb eines Events führen zu einem Fehler; in diesem Fall wird lediglich der erstgenannte Teamcode genutzt. Verwendungen eines Teamcodes über verschiedene Events sind möglich.

Der Schutz des Teamcodes ermöglicht die Eingabe eines alphanumerischen Wertes durch die SPielenden, während der Teamcode selber in allen persistierten Dateien über die Referenz erfolgt. Die Eingabe der Referenz selber ist, solange die Kennzeichnung `md5:...` als Präfix zum Teamcode verwendet wird, nicht zulässig. Ein Teamcode mit vorangestelltem `md5:` kann nicht durch Eingabe dieses Strings als gültiger Teamcode genutzt werden, es wird lediglich die nach einem Doppelpunkt `:` folgende Zeichenkette als verschlüsselter Teamcode verstanden.

Da Teamcodes in Repositories gespeichert werden, können diese (für das System) sensiblen Informationen geschützt werden. Der 8-stellige Teamcode kann unter Angabe von `md5:<md5-teamcode>` geschützt werden. 

Der `md5-teamcode` stellt dabei den MD5 Hash-Wert des Teamcodes dar. Dieser wird auf der Computer-Konsolen über den Befehl `echo -n TEAMCODE|md5` gebildet. `TEAMCODE` ist hierbei der zu schützende Teamcode. In diesem Beispiel ergibt dies den Hash-Wert `a03e4f7892cf21d5be086fcaf75d1c88`, der mit `md5:a03e4f7892cf21d5be086fcaf75d1c88` als Teamcode anzugeben ist. Sollte der Teamcode als sogenannter Creator genutzt werden, ist in dem Bereich Creator ebenmfalls der MD5-Hash anzugeben, um den ursprünglichen Wert auch hier zu schützen.

Ein weiter Schutzmechanismus stellt die Nutzung der `teamcodes.json` dar, in der die Übersetzung des Teamcodes in einen frei wählbaren Code ermöglicht wird. Hierbei kann die Übersetzung über den Bereich `eventid` -> `TEAMCODE` -> neuer Teamcode bzw. `global` -> `TEAMCODE` -> neuer Teamcode erfolgen. `TEAMCODE` ist hier der zu schützende Teamcode und `neuer Teamcode` der anstelle dessen zu nutzende Teamcode.

## Einstellungen

`name`: ausgeschriebener Name des Teams  
`active`: Gibt an, ob das Team aktiv ist und sich anmelden darf  
`from`: Gibt den Start-Zeitpunkt an, ab dem das Team an dem angegebenen Event teilnehmen darf. Das Format lautet "YYYY-MM-DD HH:MM:SS.mmmmm"  
`to`: Gibt den Ende-Zeitpunkt an, bis zu dem das Team an dem angegebenen Event teilnehmen darf. Das Format lautet "YYYY-MM-DD HH:MM:SS.mmmmm"  
`maxplayer`: Gibt die Anzahl der unterschiedlichen Spieler an, die unter dem Teamcode an dem Event teilnehmen dürfen. Die Angabe "0" definiert eine unbegrenzte Anzahl von Spielern. Die Anzahl wird über den gesamten Zeitraum gemessen und beschreibt eine Gesamtanzahl auch bei ansynchroner Nutzung.  
`deletable`: Gibt an, ob der Teamcode gelöascht werden kann (Default: true)  
`template`: Gibt das zu nutzende Template an, welches unterhalb von /templates/ existieren muss (Default: 3exiteers)
`lobby`: Gibt mit true/false an, ob für den Event die Lobby aktiviert werden soll. Die Lobby stellt sicher, dass alle Nutzer nach ihrer Registrierung gesammelt in das Spiel einsteigen können. Die Lobby wird dabei aus der story.json wie ein Kapitel verarbeitet, d.h. es können eigene Grafiken und Texte verwendet werden.

## Cretors

Der Bereich `creators` ermöglicht die Definition von besonderen Rechten, die durch Veränderungen an Rechten und dem Aktivitätssstatus nicht beeinflusst werden.Zudem kann über den Creator-Bereich die Kontakt- und Feedbackmöglichkeit bestimmt werden:

| Einstellung | Beschreibung |
| --- | --- |
|`email`|Kann den Story-Ablauf als Diagramm anzeigen lassen (Defaul: `none`)|  
|`request`|Gibt eine einzelne E-Mail-Adresse an, die bei einem fehlerhaften Anmeldeversuch an das Event angezeigt werden soll, um einen Zugang zu erfragen (Default: `access@3exiteers.de`)|  
|`feedback`|Gibt eine Liste von E-Mail-Adressen an, die bei der Abgabe eines Feedbacks von Spielenden benachrichtigt werden sollen. (Default: `none`)|  
|`team`|Liste von Teamcodes, die durch verändernde Befehle NICHT beeinflusst werden sollen. Beispiel, wenn hier ["`TEST`", "`DUMMY`"] definiert ist, werden die Teamcodes `TEST` und `DUMMY` nicht beeinflusst und bestehen unverändert weiter. Damit bleibt z.B. der Zugang zum Event weiterhin für diese Teamcodes erhalten.|  


## Rechte

Unter `<teamcode>`->`permissions` sind folgende Rechte für das Team definierbar:

| Recht | Beschreibung |
| --- | --- |
|`storyflow`|Kann den Story-Ablauf als Diagramm anzeigen lassen (Defaul: False)|  
|`teamreset`|Kann den Fortschritt des angemeldeten Teams zurücksetzen (Default: False)|  
|`gitimport`|Kann die Ressourcen aus dem verknüpften Github-Repository aktualisieren (Default: False)|  
|`editor`|Kann den integrierten JSON-Editor aufrufen (Default: False)|  
|`eventreset`|Kann den Fortschritt aller Teams im aktuellen Event zurücksetzen (Default: False)|  
|`timerreset`|Kann die server-seitig gespeicherten Timer zurücksetzen (Default: False)|  
|`noquests`|Alle Kapitel mit Quests werden ohne Quests angezeigt (für Debugging der Story) (Default: False)|  
|`lobbyadmin`|Kann eine Lobby beenden und für die Teilnehmer der Lobby zum ersten Kapitel weiterleiten (Default: False)|  
|`lobbywait`|Gibt an, dass Spielende dieses Teams nach der Registrierung in die Lobby warten. (Default: False) Die Lobby ist standardmäßig ausgeschaltet, damit Einzelspieler oder Teams außerhalb eines Events nicht in der Lobby festgehalten werden. Für Events empfiehlt sich, den Teilnehmern den Link zu Registrierung vorab bekannt zu geben und die Lobby zu aktivieren. Die Teilnehmer können dann vorab sich registrieren und den Aufruf technisch ausprobieren, ohne die Story bereits zu spielen. (obsolete)|
|`event_activate`|Setzt das gesamt Event auf aktiv, damit kann es von allen angegeben Teamcodes grundsätzlich aufgerufen werden (Default: False)|  
|`event_deactivate`|Setzt das gesamt Event auf inaktiv, damit kann es nicht weiter genutzt werden. Auch Creators können das Event nicht mehr aufrufen. Diese Option ist nur umkehrbar, in dem die JSON über das Repository wieder auf aktiv gesetzt wird. (Default: False)|  
|`team_activate`|Setzt alls Teams, die nicht als Creator definiert wurden, auf aktiv. Dies kann nützlich sein, um zuvor inaktiv gesetzt Teams zu einem identischen Zeitpunkt für den Aufruf des Events freizuschalten (Default: False)|  
|`team_deactivate`|Setzt alls Teams, die nicht als Creator definiert wurden, auf inaktiv. Diese Teams können das Event damit nicht mehr nutzen. Alle Zugriffe werden blockiert und bestehende Events damit unterbrochen! (Default: False)|
|`statistic-teams`|Erlaubt den Aufruf der Statistik für die Übersicht der Teams (Default: True)|
|`statistic-quests`|Erlaubt den Aufruf der Statistik für die Übersicht der Herausforderungen (Default: True)|
|`statistic-players`|Erlaubt den Aufruf der Statistik für die Übersicht der Spieler (Default: True)|
