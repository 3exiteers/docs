# Wie wird man Creator?

Die nachfolgende Dokumentation beschreibt, wie das Creator-Prinzip des 3Exiteers Framework funktioniert und man ein Creator wird.

## Vorbereitung

### Konto bei github.com erzeugen

- Private oder geschäftliche Adresse verwenden
- Profilname vergeben (sprechend, nicht-sprechend, Alter-Ego, …) – alle Referenzen erfolgen später mit diesem Namen
- MFA (2-Faktor) aktivieren
- Name an 3Exiteers melden

### Git Client installieren

Die Installation eines lokalen Git Clients ist empfohlen, da mit einem solchen Client die Entwicklung gegenüber der Web Oberfläche deutlich vereinfacht wird. Wir empfehlen folgende freie Software zu nutzen.

- (Atlassian Sourcetree)[https://desktop.github.com]

#### Atlassian Sourcetree

- https://www.sourcetreeapp.com


### Software VS Code installieren (oder anderer bevorzugter Texteditor)

- Speichern von reinen Textdateien ohne Sonderzeichen oder zusätzlichen „Interpretationen“ erforderlich
- https://code.visualstudio.com

## Entwicklung

1. Repositories befinden sich unter https://github.com/3exiteers 
2. Repositories sind geschützt und auf privat eingestellt, d.h. erst sichtbar, sobald das/die Repositories dem Github-Konto zugeordnet wurden. Daher Kontoname (sichtbar über Profil in der rechten oberen Ecke per Klick auf Foto. Hinter „Signed in as … steht der selbstgewählte Profilname)
3. Nachdem Repositories von 3Exiteers zugeordnet wurden, können diese  im Webbrowser aufgerufen werden
4. Durch Auswahl der grünen Schaltfläche „Code“ kann „Open with Github Desktop“ ausgewählt werden
5. Die Nachfrage, ob der Link mit Github Desktop geöffnet werden darf, ist zu bestätigen
6. Danach wird das Repository von Github geladen und unter die Verwaltung von Github Desktop gestellt
7. Die Dateien und Ordner in dem Pfad, in dem das geladene Repository gespeichert wurde, kann nun verändert werden. Das unsichtbare Verzeichnis „.git“ darf nicht angepasst werden, da ansonsten die Verwaltung des Repository nicht garantiert werden kann („know your actions“).
8. Nachdem Änderungen durchgeführt wurden, werden die lokalen Änderungen durch Github Desktop erkannt und ein „Push“ ermöglicht.
    a. Alle Änderungen sollten so kleinteilig wie möglich sein, um diese bei Bedarf auch wieder zurücknehmen zu können
    b. Alle Änderungen erfolgen an einem zentral gespeicherten Repository ggf. auch mit mehreren Teilnehmenden – in einem solchen Fall kann es zu Konflikten kommen. Hier gibt es Verfahren, dies zu vermeiden, aber für ein einfaches Repository mit wenigen Teilnehmenden („Contributoren“) kann da jetzt erst einmal drauf verzichtet werden
9. Jede Änderung muss zuerst durch einen sogenannten „Commit“ festgeschrieben werden. Solang die Änderungen nicht festgeschrieben sind, können diese verloren gehen. Auf der anderen Seite können die Dateien aber in diesem Zustand noch beliebig geändert werden.
    a. Es können beliebig viele Commits geschrieben werden, bevor diese an den zentralen Server zurück übertragen werden. Erst mit dem Überragen auf den Server stehen diese der 3Exiteers Framework und anderen Teilnehmenden zur Verfügung.
    b. Jeder Commit ist mit einer möglichst sprechenden (englischen) Beschreibung der Änderung zu kommentieren. Die Beschreibung sollte als Imperativ (Befehl) formuliert sein (z.B. „Update README“), so dass durch Dritte erkannt werden kann, was diese Änderung bewirkt.
10. Sollen die Änderungen auf den Server und in das Framework übertragen werden, ist ein sogenannter „Push“ oder „Publish branch“ (Github Desktop) durchzuführen. Bei Auswahl dieser Aktion werden die Commits (alle, nicht nur der letzte Zustand) an den Server übertragen und festgeschrieben.
11. Wird auf Seiten Github diese Änderung erkannt, erfolgt eine automatische Übertragung an das 3Exiteers Framework und die Änderungen (der letzte Zustand der Dateien) werden an den Server übertragen.
    a. Die Änderungen benötigen je nach Umfang der Datenmenge entsprechend Zeit
    b. Die Änderungen stehen nach erfolgreichem Import umgehend zur Verfügung und könnend dadurch umgehen getestet werden
    c. Bestimmte (gefährliche) Dateien werden bei dem Import gefiltert und nicht bereitgestellt
12. Für den Test ist ggf. ein Reload der Website erforderlich, um Änderungen angezeigt zu bekommen
13. Wird die Seite nicht oder mit einem Fehler angezeigt, sind die typischsten Fehlerquellen (noch nicht alle mit sprechender Fehlermeldung versehen):
    a. Fehlformatierte Struktur von JSON-Dateien
    b. Fehlende referenzierte Dateien

## Aufbau der Repositoiries:

1. Jedes Repository besteht mindestens aus einer JSON-Datei. Diese hat den Namen des Typs des Repository (`event.json`, `story.json` oder `quest.json`)
2. Der Aufbau der JSONs unterscheidet sich je nach Typ.
3. Ein Template (und ggf. weitere Dateien) befindet sich idealerweise bereits im Repository
4. Die JSON ist mit dem oben installierten Editor zu bearbeiten
5. Alle Änderungen sind wie oben beschrieben zu aktualisieren
