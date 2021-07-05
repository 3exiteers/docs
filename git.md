# GIT

> Dieser Bereich beschreibt die Aktualisierung von Bestandteilen über ein Code Versionierungs System. Die Aktualisierung erfolgt dabei vorrangig über zwei Angaben: in der event.json und in einer gesonderten Datei namens `git.json'.

## Einstellungen

### Ablauf

Aus einem Event heraus wird  - sofern die nötigen Rechte für den Benutzer/Teamcode angegeben sind - die Möglichekit einer Aktualisierung der Event, Story oder Quests gegeben. In dem Event-Menü erscheint für berechtigte Nutzer der Eintrag "Aktualisierung durchführen". 

In den Konfigurationen von Event, Story und Quest wird dabei ein Konfigurationsbereich `repository` erwartet, mit dem die Aktualisierung des jeweiligen Typs durchgeführt werden kann. Folgende Angaben sind dabei möglich:

repository
type
organization
private

Es wird als Basis immer github.com angenommen. Über die `organization` wird die Organisation in Github beschrieben (dies können auch private Konten sein). Die Einstellung `repository`beschreibt das eigentliche Repository, in dem die Quellen abgelegt sind.

### Bundles

Bei einem Bundle werden die Definitionen von Event, Story und Quests in einem Reposiutory vorgenommen. Dies hat die Vorteile in einer zentralen Definition der Elemente und einer einmaligen und einheitlichen Rechtevergabe bei Mitwirknden auf Github.

Allerdings birgt dieser Ansatz auch das POtential von redundanten Definitionen, in dem zum Beispiel Quests durch mehrere Quellen beschrieben werden. Daher werden "Bundles" typischerweise in der ersten Kollaborations-Phase eines Projekts genutzt und nach Fertigstellung die einzelnen Elemente in eigene Repositories überführt.

Der Aufbau eines Bundles folgt dabei nicht dem Aufbau eines Event-, Story, oder Quest-Repository. Bei iesen Formaten liegen die Quellen in dem HAuptverzeichnis des Repository. Bei den Bundles werden diese Definitionen in Unterverzeichnisse mit den Namen des jeweiligen Typs und einem jeweils eindeutigen Unterordner eingeordnet.

So ist in dem Verzeichnis `/event/test-event-de/` beispielsweise der Inhalt eines Event mit den Namen `test-event-de` vom Typ `event` enthalten. Gleiches gilt für `story`und `quest`. Andere Ordner werden bei einer Aktualisierung nicht berücksichtigt.

**Hinweis**: Da durch diese flexible Definition der Verzeichnisstrukturen das Risiko einer  Beeinflussung von dritten Events, Stories oder Quests besteht, wird ein Bundle nur in der Aufbauphase für vertrauensvolle Creators zugelassen.

Für ein Bundle ist der Name des Repository weniger ausschlaggebend für die Ablage in dem Framework. Das Repository muss vom Typ `bundle` sein und das Repository muss mit der Zeichenkette `bundle-`beginnen. Die danachfolgende Bezeichnung kann frei gewählt werden. Für die Ablage sind die Verzeichnisnamen unterhalb der Verzeichisse `/event, `/story`und `/quest`entscheidend.

Beispiel:

```json
repository: {
    "type": "event",
    "repository": "event-sample-de",
    ...
}
```


### Nicht-Bundles

#### Event

Für ein Event ist der Name des Repository ausschlaggebend für die Ablage in dem Framework. Das Repository muss vom Typ `event` sein und das Repository muss mit der Zeichenkette `event-`beginnen. Die auf diese Zeichenette folgenden Bezeichnung beschreibt den internen Namen des Events.

Beispiel:

```json
repository: {
    "type": "event",
    "repository": "event-sample-de",
    ...
}
```

Der Typ und der Angfang der  Bezeichnung müssen identisch sein, da sonst die Aktualisierung abgebrochen wird. Hintergrund dieses Namenskonzepts ist, dass in einer Organisation somit gleichlautende Namen für Event und Story verwaltet werden können, bei denen eine 1:1 Beziehung besteht. Der Präfix stellt sicher, dass diese unterschieden werden können und zu keinem Namenskonflikt führen. Solte diese Trennung nicht gewünscht sein oder auf Grund der Rechteverwaltung in Github nicht gewünscht, kann alternativ der "Bundle"-Ansatz genutzt werden.

#### Story

siehe Event, jedoch anstelle der Schlküsselbegriffs `event`ist hier `story`zu nutzen.

#### Event

siehe Event, jedoch anstelle der Schlküsselbegriffs `event`ist hier `event`zu nutzen.

## git.json

Die `git.json`ist eine von den Administratoren erstellte Konfigurationsdatei zur Aktualisierung von Inhalten. Für ein Event muss in dem korrespondierenden Event-Verzeichnis eine `git.json` manuell angelegt werden, damit eine Aktualisierung möglich ist. In dieser wird der Benutzername und der Zugriffs-Token für einen Zugriff auf die Repositories beschrieben.

**Warnung**: Eine Veröffentlichung dieser Informationen in einem Github-Repository wird auf Grund der Sicherheitsrisikos nicht empfohlen. Dritte können diese Informationen missbrauchen! Es wird die Definition einer `.gitignore` mit Ausschluss von Dateien mit dem Namen `git.json` angeraten.

**Hinweis**: Um eine missbräuchliche Definition dieser Datei zu verhindern werden diese Dateien vor Aktualisierung entfernt.

Folgender Aufbau der `git.json` ist erforderlich:

```json
{
    "username": "my_name",
    "access_token": "ABCMYTOKENXYZ"
}
```
