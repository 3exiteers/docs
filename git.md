# GIT

> Dieser Bereich beschreibt die Aktualisierung von Bestandteilen über ein Code Versionierungs System. Die Aktualisierung erfolgt automatisch bei jeder Aktualisierung eines berechtigten Repository unterhalb der Organisation 3Exiteers.

## Einstellungen

### config.json

(Details folgen)

### Typen

#### event

Ein Repository mit den Markern für ein Event (z.B. `event-` oder `.event`) beinhaltet alle Inhalte für die Event-Definition. Hierbei ist für ein in das Framework einbindbares Event die Datei `event.json` zwingend erforderlich. Alle für die Anzeige des Events erforderlichen Dateien sind in diesem Repository ebenfalls beinzufügen.

#### story

Ein Repository mit den Markern für eine Story (z.B. `story-` oder `.story`) beinhaltet alle Inhalte für die Story-Definition. Hierbei ist für ein in das Framework einbindbare Story die Datei `story.json` zwingend erforderlich. Alle für die Anwendung der Story erforderlichen Dateien sind in diesem Repository ebenfalls beinzufügen.

#### quest

Ein Repository mit den Markern für eine Quest (z.B. `quest-` oder `.quest`) beinhaltet alle Inhalte für die Quest-Definition. Hierbei ist für ein in das Framework einbindbare Quest die Datei `quest.json` zwingend erforderlich. Alle für die Anzeige der Quest erforderlichen Dateien sind in diesem Repository ebenfalls beinzufügen.

#### style

Ein Repository mit den Markern für Stylesheets (z.B. `style-` oder `.style`) beinhaltet alle Inhalte für die Stylesheet-Definition. Hierbei ist für ein in das Framework einbindbare Stylesheet die Datei `style.json``zwingend erforderlich. Ergänzende Dateien (z.B. Grafiken) könnend em Repository beigefügt werden. Die Referenzierung innerhalb der Stylesheets kann mit Platzhaltern erfolgen, die nach dem Import einmalig in die Pfade auf dem Server übersetzt werden.

| Parameter     | Beschreibung |
| ------------- |:----------- |
| `{eventdir}` | (derzeit ohne Funktion)) |
| `{storydir}` | Ersetzung mit dem Pfad zu der aktuellen Story (= Name des Repository) |
| `{questdir}` | (derzeit ohne Funktion)) |
| `{styledir}` | Ersetzung mit dem Pfad zu dem aktuellen Style-Definition |
| `{repodir}` | Ersetzung mit dem Repository-Namen |

