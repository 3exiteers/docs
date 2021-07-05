# 3Exiteers Framework

The furture of exit game is open.

!> In dieser Dokumentation wird an manchen Stelle noch aus Gründen der besseren Lesbarkeit das generische Maskulinum verwendet. Weibliche und anderweitige Geschlechteridentitäten werden dabei ausdrücklich mitgemeint, soweit es für die Aussage erforderlich ist.

# Beschreibung

Bei dem 3Exiteers Framework ("Framework") handelt es sich um eine von [3Exiteers](https://3exiteers.de) bereitgestellte SaaS-Lösung, die das Bereitstellen und Spielen von sogenannten Exit Games, oder auch Escape Rooms genannt, ermöglicht (vereinfach "Spiele" im Folgenden genannt). Das Framework fokussiert sich dabei auf die einfache Bereistellung von Exit Games, die über strukturierte Dateiformate und -Schnittstellen bereitgestellt werden können.

## Exit Games

Unter Exit Games fassen wir in dieser Beschreibung verschiedene Spielformate zusammen, bei denen Spielende in einer Geschichte Aufgaben lösen müssen, um die Geschichte abschließen zu können. Das Framework erlaubt dabei einen felxiblen und dynamischen Spielverlauf, bei dem an bestimmten Stellen in der Geschichte Herausforderungen zu lösen sind.

Das Framework erlaubt durch seine Flexibilität aber auch artverwandete oder sogar andere Einsatzgebiete. So sind neben Exit Rooms oder auch Escape Rooms beispielsweise auch Schnitzjagden oder Schultests möglich, bei denen Eingaben zur Fortführung erforderlich sind. Die Komplexität kann dabei von einzelnen Herausforderungen bis zu komplexen Abläufen mit mehreren Herausfordferungen, Abzweigungen und alternativen Enden reichen.

# Bestandteile

Das Framework trennt zur einfacheren Pflege und dem flexibleren Zusammensetzen der Elemente verschiedene Bestandteile, die das letztendliche Spiel darstellen.

## Quest

Hauptbestandteil der Spiele besteht aus den Rätseln oder auch Herausforderungen, um in der Geschichte voranzukommen. Die Rästel, oder auch "Quests" im Folgenden genannt, beschreiben Herausforderungen, die durch die Spielenden zu lösen sind. Erst wenn die richtige Lösung zu der jeweiligen Quest angegeben wurde, könnend ie Spielenden fortfahren.

Die Definition der Quest erfolgt in den [Quest](quest)-Dateien.

### Tips

Als Bestandteil der Quest können auch Lösungshinweise (im Folgenden auch "Tips" genannt) angegeben werden, die die Spielenden nutzen können. Diese Tips geben Hinweise, wie das Rätsel zu lösen ist. Die Anzahl und der Umfang der Tips ist flexibel, so dass auch komplexe Lösungswege über diese Funktion aufgezeigt werden können.

Die Definition der Tips erfolgt als Bestandteil der [Quest](quest)-Dateien.

## Story

Die Geschichte ist der inhaltliche rote Faden, den die Spielenden beim Spielen beschreiten. Die Geschichte ("Story" im Folgenden genannt) kann inhaltlich sehr detailliert ausgeführt werden oder auch sich auf wesentliche Informationen beschränken. Die Geschichte wird anhand von Kapiteln erzählt, zwischen denen sich die Spielenden bewegen.

Der Ablauf kann dynamisch und flexibel gestaltet sein und wird im Rahmen der Geschichte definiert. So können beispielsweise lineare Abläufe genauso wie Abzweigungen umgesetzt werden. Alle Abläufe haben aber gemeinsam, dass die Geschichte sich mindestens aus einem Kapiel zusammensetzt

Die Definition der Story erfolgt in den [Story](story)-Dateien.

## Chapter

Innerhalb der Geschichte stellen Kapitel die Etappen dar, an denen die Spielenden vorbei kommen können. Diese Kapitel (im Folgenden auch "Chapter" genannt) stellen den Inhalt der Geschichte dar. Es können zudem Quests eingebunden werden, die die Eingabe einer Lösung von dem Spieler verlangen. Chapters können somit reinen Inhalt der Geschichte darstellen, als auch 

Die Definition der Chapter erfolgt als Bestandteil der [Story](story)-Dateien.

## Event

Dein Ergeignis (oder auch "Event" im Folgenden genannt) beschreibt den Kontext, in dem eine Geschichte gespielt wird. Ein Ereignis kann zum Beispiel ein Treffen im privaten Kreis, eine Firmenveranstaltung oder ein anderes Ereignis sein. Der Unterschied zu einer Story ist, dass das Event die organisatorischen Vorgaben definiert. Dies können zum Beispiel die spielberechtigten Spielenden, die Gültigkeit des Spiels oder eine allgemeine Beschreibung der Veranstaltung sein.

Diese Funktion ist für Einzelspielende oder das Spielen im privaten Umfeld weniger relevant, bei größeren Veranstaltungen mit mehr als 50 Spielern bietet diese Form eine Unterstützung in der Organisation.

Die Definition eines Event erfolgt in den [Event](event)-Dateien.

# Mitwirkende

An einem Spiel wirken verschiedene Protagonisten mit. Die nachfolgenden Rollen können durch unterschiedliche Personen wahrgenommen werden.

## Spieler

Die Spielenden sind die zentralen Protagonisten bei einem Exit Game. Die Spielenden tauchen in die Story ein und lösen die Quests. Um die Spielenden angemessen zu unterhalten gilt es das richtige Maß an inhaltlicher Story und Schwierigkeit der Quests zu finden. Nicht jeder Spielende ist gleich, daher sind auch unterschiedliche Schwierigkeitsgrade denkbar.

Das Framework ist darauf ausgelegt, die technische Spielerfahrung für die Spielenden so angenehm wie möglich zu gestalten. Für den Inhalt der Geschichte, die Schwierigkeit oder Logik der Quests sind die produzierenden Mitwirkenden, die sogannten "Creators" zuständig.

## Quest Creators

Ein Quest Creator erstellt und pflegt die Quests, die die Spielenden zu lösen haben. Die Definition eines Event erfolgt in den [Quest](quest)-Dateien.

## Story Creators

Ein Story Creator erstellt und pflegt die Geschichte, die sich aus verschiedenen Chapter zusammensetzt. Die Definition einer Story erfolgt in den [Story](story)-Dateien.

## Event Creators

Ein Event Creator erstellt und pflegt die organisatorischen Vorgaben zu dem Ereignis. Die Definition eines Event erfolgt in den [Event](event)-Dateien.

# Funktionen

## Eingaben

## Auswahl

(noch nicht implementiert)

## Mehrfachauswahl

(noch nicht implementiert)

## Auswahl auf Bild

(noch nicht implmenentiert)

## Puzzle

(noch nicht implementiert)
