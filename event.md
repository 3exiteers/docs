# EVENT

> Event descriptions.

## Einstellungen

`name`: ausgeschriebener Name des Teams  
`active`: Gibt an, ob das Team aktiv ist und sich anmelden darf  
`from`: Gibt den Start-Zeitpunkt an, ab dem das Team an dem angegebenen Event teilnehmen darf. Das Format lautet "YYYY-MM-DD HH:MM:SS.mmmmm"  
`to`: Gibt den Ende-Zeitpunkt an, bis zu dem das Team an dem angegebenen Event teilnehmen darf. Das Format lautet "YYYY-MM-DD HH:MM:SS.mmmmm"  
`maxplayer`: Gibt die Anzahl der unterschiedlichen Spieler an, die unter dem Teamcode an dem Event teilnehmen dürfen. Die Angabe "0" definiert eine unbegrenzte Anzahl von Spielern. Die Anzahl wird über den gesamten Zeitraum gemessen und beschreibt eine Gesamtanzahl auch bei ansynchroner Nutzung.  
`deletable`: Gibt an, ob der Teamcode gelöascht werden kann (Default: true)  
`template`: Gibt das zu nutzende Template an, welches unterhalb von /templates/ existieren muss (Default: 3exiteers)
`lobby`: Gibt mit true/false an, ob für den Event die Lobby aktiviert werden soll. Die Lobby stellt sicher, dass alle Nutzer nach ihrer Registrierung gesammelt in das Spiel einsteigen können. Die Lobby wird dabei aus der story.json wie ein Kapitel verarbeitet, d.h. es können eigene Grafiken und Texte verwendet werden.

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
|`lobbywait`|Gibt an, dass Spielende dieses Teams nach der Registrierung in die Lobby warten. (Default: False) Die Lobby ist standardmäßig ausgeschaltet, damit Einzelspieler oder Teams außerhalb eines Events nicht in der Lobby festgehalten werden. Für Events empfiehlt sich, den Teilnehmern den Link zu Registrierung vorab bekannt zu geben und die Lobby zu aktivieren. Die Teilnehmer können dann vorab sich registrieren und den Aufruf technisch ausprobieren, ohne die Story bereits zu spielen.|  