# Spielverlauf

TicTacToe oder Drei gewinnt (auch Kreis und Kreuz, Dodelschach) ist ein klassisches, einfaches Zweipersonen-Strategiespiel, dessen Geschichte sich bis ins 12. Jahrhundert v. Chr. zurückverfolgen lässt.

![TicTacToe-8](uploads/d76a3886db5453dc43fd56bcf0d4fe59/TicTacToe-8.png){width=200}

Auf einem quadratischen, 3×3 Felder großen Spielfeld setzen die beiden Spieler abwechselnd ihr Zeichen (ein Spieler Kreuze, der andere Kreise) in ein freies Feld. Der Spieler, der als Erster drei Zeichen in eine Zeile, Spalte oder Diagonale setzen kann, gewinnt (Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Tic-Tac-Toe)).

Im Spiel sind folgende Teilaufgaben zu erledigen:
* Spiel initialisieren (Spielfeld und Spieler)
* Stein (Zeichen) setzen
* Prüfen ob der Spieler gewonnen hat
* Prüfen ob es noch weitere Möglichkeiten gibt um einen Stein zu setzen
* Spielerwechsel

Wenn man diese Teilaufgaben miteinander verknüpft und den logischen Programmablauf festlegt, dann erhält man folgenden Programmablauf (Flussdiagramm):

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

# Die Klassen im Detail

## Player

Der Konstruktor soll den Namen sowie das Zeichen des Spielers übernehmen. Beide Attribute sollen von außen nur lesend erreichbar sein. 

Die Methode **toString()** soll eine passende Repräsentation des Spielernamens (inklusive Symbol) zurückgeben.

## Field

In der Klasse **Field** wird lediglich der Spieler, der das Feld besetzt, gespeichert. Initial soll das Feld nicht belegt sein.

* **isEmpty()** ermittelt ob das Feld frei ist - sprich ob es NICHT von einem Spieler besetzt ist.
* **setPlayer()** versucht das Feld mit dem übergebenen Spieler zu besetzten. ACHTUNG: das ist nur möglich, wenn das Feld leer ist. Der Rückgabewert gibt an, ob der Spieler erfolgreich gesetzt werden konnte.
* **isTakenByPlayer()** überprüft ob das Feld mit vom übergebenen Spieler besetzt ist
* **getToken()** liefert das Zeichen des Spielers auf dem Feld zurück. Ist das Feld leer, so soll ein entsprechendes Zeichen (z.B. ein Leerzeichen) zurückgegeben werden.

## Board

Die Klasse **Board** repräsentiert das ganze 3x3 Spielfeld. Die einzelnen Felder sollen mit Objekten der Klasse **Field** belegt sein.

* **isFieldEmpty()** überprüft ob das Feld der angegebenen Indizes leer ist. Die Übergabeparameter sollen - wie in allen anderen Methoden auch - auf ihre Gültigkeit überprüft werden.
* **placeToken()** versucht den Spieler auf dem entsprechenden Feld zu setzen. War das setzen erfolgreich, so soll **true** zurückgegeben werden, wenn nicht dann **false**.
* **emptyFieldExists()** überprüft ob zumindest ein Feld des Spiels noch leer ist.
* **getRow()**, **getCol()**, **getMainDiagonal()**, **getSecondaryDiagonal()** liefern jeweils die 3 relevanten Felder als **Field** Array zurück
* **print()** gibt das Spielfeld auf der Commandline aus.

## Game

Die Klasse **Game** fügt die anderen Klassen zusammen und ist für den Spielablauf zuständig. Die Attribute der Klasse sind das Spielfeld (**board**), die Spieler (**firstPlayer**, **secondPlayer**) und der aktuelle Spieler (**currentPlayer**). Zusätzlich gibt es noch 2 Konstante (**TOKEN_FIRST_PLAYER**, **TOKEN_SECOND_PLAYER**), die das Zeichen (den Token) der Spieler zur Verfügung stellen.

* **getPlayerName()** und **getPlayerToken()** geben Namen und Zeichen des aktuellen Spielers zurück
* **placeToken()** versucht das Feld der übergebenen Indizes mit dem aktuellen Spieler zu besetzen
* **checkIfStoneWinsGame()** überprüft ob der letzte Zug das Spiel zugunsten des aktuellen Spielers entschieden hat
* **noFurtherMovesPossible()** überprüft ob es zumindest noch eine Möglichkeit gibt ein Feld am Spielbrett zu besetzten. Mit Hilfe dieser Methode kann überprüft werden, ob das Spiel mit einem Unentschieden endet.
* **changePlayer()** wechselt den aktuellen Spieler
* **play()** fürt das Spiel aus. Im wesentlichen entspricht der Ablauf dieser Methode dem Flussdiagramm von oben.

Mit diesen Informationen soll es möglich sein, das Spiel TicTacToe entsprechend des Klassendiagramms umzusetzen.

# Die Java Swing GUI

Die Java Swing GUI wird Schritt für Schritt basierend auf dem soeben programmierten Spiel aufgebaut. Als erstes brauchen wir eine eigene Klasse für unsere GUI. Die Klasse repräsentiert unser Hauptfenster und leitet daher von **java.swing.JFrame** ab. **JFrame** basiert auf **AWT (Abstract Windows Toolkit)** und bietet die notwendigen Grundfunktionen für unsere Anwendung.

```java
package beispiele.tictactoeoop;

import javax.swing.*;

public class TicTacToeGUI extends JFrame {
    public TicTacToeGUI() {
        super("TicTacToe das Spiel !!!");
    }

    public static void main(String[] args) {
        JFrame frame = new TicTacToeGUI();
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(500, 300);
        frame.setVisible(true);
    }
}
```

![GUI_JFrame](uploads/4f6098a2da15f9e0f18ee40af56fbaea/GUI_JFrame.png)

Aus dem Programm lassen sich unterschiedliche Elemente ablesen:
* Dem Superkonstruktor wird der Titel des Frames übergeben
* **setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)** sorgt dafür, dass mit einem Klick auf das "x" Symbol das Fenster geschlossen wird
* **setSize()** setzt die Fenstergröße in Pixel
* Abschließend zeigt **setVisible(true)** das Fenster an.

Nachdem wir jetzt ein lauffähiges Java Swing Fenster haben, wollen wir dieses schrittweise zu unserer TicTacToe-GUI ausbauen.

## Der Aufbau des Fensters:

Am Ende soll unsere GUI wie folgt aussehen:

![GUI_Beispiel](uploads/1da798ff12a7faff67a89753a0ca3624/GUI_Beispiel.png)

Das Fenster ist in 2 Teile aufgeteilt:
1. Den Bereich für das Spielfeld: Das Spielfeld setzt sich aus Buttons zusammen, die in einem 3x3 Grid angeordnet sind. Die Zeichen werden mit Hilfe von Grafiken (Icons) angezeigt.
2. Den Bereich für die Kontrollbuttons: Es gibt lediglich 2 Buttons
    - **Exit**: Beendet das Programm mit **System.exit(0)**
    - **Reset**: Startet zu jedem Zeitpunkt (egal ob das Spiel beendet oder nicht) ein neues Spiel

Damit die Implementierung des Spiels 1:1 mit den Anweisungen übereinstimmt, findest du hier eine Beispielversion des Spiels:

[TicTacToe_Game.tar](uploads/0aac7ab675b0f7e228ca93c10b40dda7/TicTacToe_Game.tar)
