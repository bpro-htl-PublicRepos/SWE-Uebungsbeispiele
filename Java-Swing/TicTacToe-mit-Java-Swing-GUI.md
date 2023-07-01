# Spielverlauf

TicTacToe oder Drei gewinnt (auch Kreis und Kreuz, Dodelschach) ist ein klassisches, einfaches Zweipersonen-Strategiespiel, dessen Geschichte sich bis ins 12. Jahrhundert v. Chr. zurückverfolgen lässt.

![TicTacToe-8](uploads/d76a3886db5453dc43fd56bcf0d4fe59/TicTacToe-8.png){width=200}

Auf einem quadratischen, 3×3 Felder großen Spielfeld setzen die beiden Spieler abwechselnd ihr Zeichen (ein Spieler Kreuze, der andere Kreise) in ein freies Feld. Der Spieler, der als Erster drei Zeichen in eine Zeile, Spalte oder Diagonale setzen kann, gewinnt.[1]

[1] Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Tic-Tac-Toe)

Im Spiel sind folgende Teilaufgaben zu erledigen:
* Spiel initialisieren (Spielfeld und Spieler)
* Stein (Zeichen) setzen
* Prüfen ob der Spieler gewonnen hat
* Prüfen ob es noch weitere Möglichkeiten gibt um einen Stein zu setzen
* Spielerwechsel

Wenn man diese Teilaufgaben miteinander verknüpft und den logischen Programmablauf festlegt, dann erhält man folgendes Flussdiagramm:

![Flussdiagramm](uploads/dac801791294847c9b770f787760d333/Flussdiagramm.png){width=330}

# Objektorientiertes Design

Ein objektorientiertes Design kann bei einer vereinfachten Vorgehensweise durch folgende Schritte erstellt werden:

1. Benötigte Klassen identifizieren (primäre Objekte des Systems identifizieren und benennen = Klassenname)
2. Klassen in Beziehung setzen und grafisch darstellen
3. Klassendiagramm zeichnen

Folgende Klassen wurden identifiziert:
* Das Spiel selbst (Game)
* Das Spielbrett (Board)
* Die Felder auf dem Spielbrett (Field)
* Die Spieler (Player)
* Die Steine, die von den Spielern gesetzt werden (Token)

Die gefundenen Klassen stehen wie folgt in Beziehung zueinander:
* Das Spiel wird auf einem Spielbrett gespielt
* Das Spielbrett besteht aus mehreren Feldern
* Das Spiel wird von Spielern gespielt
* Der Spieler setzt den Token auf ein Feld

Die Klassen können mit ihren Beziehungen grafisch wie folgt dargestellt werden:

![Klassen_und_Beziehungen](uploads/4e93b1d975468c219bad05a54758b4b8/Klassen_und_Beziehungen.png){width=550}

Da TicTacToe sehr einfach ist, werden wir auf die Klasse Token verzichten und den Spieler direkt das Feld besetzen lassen.

# Das Klassendiagramm

![Beispiel_OOP_TicTacToe_Klassendiagramm](uploads/ddb941ad2cd3f3cae76d567e12c6a0dc/Beispiel_OOP_TicTacToe_Klassendiagramm.png)

[Beispiel_OOP_TicTacToe_Klassendiagramm.pdf](uploads/32ab11b6cc3ee5c17a65d1949abfa51d/Beispiel_OOP_TicTacToe_Klassendiagramm.pdf)

