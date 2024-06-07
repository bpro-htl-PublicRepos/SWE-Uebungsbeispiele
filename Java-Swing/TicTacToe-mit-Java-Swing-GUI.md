# Spielverlauf

TicTacToe oder Drei gewinnt (auch Kreis und Kreuz, Dodelschach) ist ein klassisches, einfaches Zweipersonen-Strategiespiel, dessen Geschichte sich bis ins 12. Jahrhundert v. Chr. zurückverfolgen lässt.

![TicTacToe-8](uploads/d76a3886db5453dc43fd56bcf0d4fe59/TicTacToe-8.png){width="200"}

Auf einem quadratischen, 3×3 Felder großen Spielfeld setzen die beiden Spieler abwechselnd ihr Zeichen (ein Spieler Kreuze, der andere Kreise) in ein freies Feld. Der Spieler, der als Erster drei Zeichen in eine Zeile, Spalte oder Diagonale setzen kann, gewinnt (Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Tic-Tac-Toe)).

Im Spiel sind folgende Teilaufgaben zu erledigen:

* Spiel initialisieren (Spielfeld und Spieler)
* Stein (Zeichen) setzen
* Prüfen ob der Spieler gewonnen hat
* Prüfen ob es noch weitere Möglichkeiten gibt um einen Stein zu setzen
* Spielerwechsel

Wenn man diese Teilaufgaben miteinander verknüpft und den logischen Programmablauf festlegt, dann erhält man folgenden Programmablauf (Flussdiagramm):

![Flussdiagramm](uploads/dac801791294847c9b770f787760d333/Flussdiagramm.png){width="330"}

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

![Klassen_und_Beziehungen](uploads/4e93b1d975468c219bad05a54758b4b8/Klassen_und_Beziehungen.png){width="550"}

Da TicTacToe sehr einfach ist, verzichten wir auf die Klasse Token und lassen den Spieler direkt das Feld besetzen.

# Das Klassendiagramm

![Beispiel_OOP_TicTacToe_Klassendiagramm](uploads/8a1d50ce32d97180c48892b08cc06038/Beispiel_OOP_TicTacToe_Klassendiagramm.png)

[Beispiel_OOP_TicTacToe_Klassendiagramm.pdf](uploads/eee9d72895bd0a7b070d6ee6f154507f/Beispiel_OOP_TicTacToe_Klassendiagramm.pdf)

# Die Klassen im Detail

## Player

Der Konstruktor übernimmt den Namen sowie das Zeichen des Spielers. Beide Attribute sind von außen nur lesend erreichbar.

Die Methode **toString()** gibt eine passende Repräsentation des Spielernamens (inklusive Symbol) zurück.

## Field

In der Klasse **Field** wird lediglich der Spieler, der das Feld besetzt, gespeichert. Initial soll das Feld nicht belegt (frei) sein.

* **isEmpty()** ermittelt ob das Feld frei ist.
* **setPlayer()** versucht das Feld mit dem übergebenen Spieler zu besetzten. ACHTUNG: das ist nur möglich, wenn das Feld leer ist. Der Rückgabewert gibt an ob das Feld erfolgreich besetzt werden konnte.
* **isTakenByPlayer()** überprüft ob das Feld vom übergebenen Spieler besetzt ist
* **getToken()** liefert das Zeichen des Spielers auf dem Feld zurück. Ist das Feld leer, so soll ein entsprechendes Zeichen (z.B. ein Leerzeichen) zurückgegeben werden.

## Board

Die Klasse **Board** repräsentiert das ganze 3x3 Spielfeld. Die einzelnen Felder sind Objekte der Klasse **Field**.

* **isFieldEmpty()** überprüft ob das Feld der angegebenen Indizes leer ist. Die Übergabeparameter sollen - wie in allen anderen Methoden auch - auf ihre Gültigkeit überprüft werden.
* **placeToken()** versucht den Spieler auf dem entsprechenden Feld zu setzen. War das setzen erfolgreich, so wird **true** zurückgegeben, wenn nicht dann **false**.
* **emptyFieldExists()** überprüft ob zumindest ein Feld des Spiels noch leer ist.
* **getRow()**, **getCol()**, **getMainDiagonal()**, **getSecondaryDiagonal()** liefert die 3 jeweils relevanten Felder als **Field** Array zurück
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
import javax.swing.*;

public class TicTacToeGUI extends JFrame {

    private static final int GAP = 5;
    private static final int BUTTON_SIZE = 100;

    public TicTacToeGUI() {
        super("TicTacToe das Spiel !!!");
    }

    public static void main(String[] args) {
        JFrame frame = new TicTacToeGUI();
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(500, 500);
        frame.setVisible(true);
    }
}
```

![GUI_JFrame](uploads/fb4ba9c47149bddfb5e499ff70e36387/GUI_JFrame.png)

Aus dem Programm lassen sich unterschiedliche Elemente ablesen:

* Dem Superkonstruktor wird der Titel des Frames übergeben
* **setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)** sorgt dafür, dass mit einem Klick auf das "x" Symbol das Fenster geschlossen wird
* **setSize()** setzt die Fenstergröße in Pixel
* Abschließend zeigt **setVisible(true)** das Fenster an.

Nachdem wir jetzt ein lauffähiges Java Swing Fenster haben, wollen wir dieses schrittweise zu unserer TicTacToe-GUI ausbauen.

Die Dokumentation zu den verwendeten GUI Elementen steht unter folgenden Links zur Verfügung (Java 20):

[Java AWT](https://docs.oracle.com/en/java/javase/20/docs/api/java.desktop/java/awt/package-summary.html)

[Java Swing](https://docs.oracle.com/en/java/javase/20/docs/api/java.desktop/javax/swing/package-summary.html)

Zusätzlich zu den Beschreibungen der einzelnen Klassen sind in der Dokumentation teilweise auch Tutorials zur Verwendung der Klassen verlinkt.

## Der Aufbau des Fensters:

Am Ende soll unsere GUI wie folgt aussehen:

![GUI_Beispiel](uploads/1da798ff12a7faff67a89753a0ca3624/GUI_Beispiel.png)

Das Fenster ist in 2 Teile aufgeteilt:

1. Den Bereich für das Spielfeld: Das Spielfeld setzt sich aus Buttons, die in einem 3x3 Grid angeordnet sind, zusammen. Die Zeichen werden mit Hilfe von Grafiken (Icons) angezeigt.
2. Den Bereich für die Kontrollbuttons: Es gibt lediglich 2 Buttons
   - **Exit**: Beendet das Programm mit **System.exit(0)**
   - **Reset**: Startet zu jedem Zeitpunkt (egal ob das Spiel beendet wurde oder nicht) ein neues Spiel

Damit die Implementierung des Spiels 1:1 mit den Anweisungen übereinstimmt, findest du hier eine Beispielversion des Spiels:

[TicTacToe_Game.tar](uploads/0aac7ab675b0f7e228ca93c10b40dda7/TicTacToe_Game.tar)


## Grundlayout

GUI Elemente werden in Swing häufig mit Hilfe des Standardcontainers [JPanel](https://docs.oracle.com/en/java/javase/20/docs/api/java.desktop/javax/swing/JPanel.html) gruppiert und angeordnet. Diesem Prinzip wollen wir auch in unserem Tutorium folgen und zuerst das Grundlayout (die Struktur) unserer GUI mit Hilfe von Containern erstellen. Damit das Layout gut sichtbar ist, sind den Containern vorerst leicht unterscheidbare Farben zugewiesen. Für eine bessere Übersichtlichkeit werden zusammengehörende Aufgaben jeweils in eigene Methoden auslagert.

Die Anordnung der 2 Bereiche (Spielfeld und Kontrollbereich) erfolgt mit Hilfe des [BorderLayouts](https://docs.oracle.com/en/java/javase/20/docs/api/java.desktop/java/awt/BorderLayout.html), dass den jeweiligen Bereich (bei uns `mainPanel`) in 5 Bereiche aufteilt: oben (`NORTH`), unten (`SOUTH`), links (`WEST`), rechts (`EAST`) und die Mitte (`CENTER`). Da unsere Bereiche untereinander liegen, haben wir oben (`NORTH`) und unten (`SOUTH`) gewählt. `GAP` ist der Abstand zwischen den Elementen.

```java
private void initFrame() {
    JPanel mainPanel = new JPanel();
    mainPanel.setLayout(new BorderLayout(TicTacToeGUI.GAP, TicTacToeGUI.GAP));
    mainPanel.setBackground(Color.YELLOW);
    mainPanel.setBorder(new EmptyBorder(TicTacToeGUI.GAP, TicTacToeGUI.GAP, TicTacToeGUI.GAP, TicTacToeGUI.GAP));
    this.add(mainPanel);

    JPanel boardPanel = new JPanel();
    boardPanel.setBackground(Color.BLACK);
    mainPanel.add(boardPanel, BorderLayout.NORTH);

    JPanel ctrlPanel = new JPanel();
    ctrlPanel.setBackground(Color.RED);
    mainPanel.add(ctrlPanel, BorderLayout.SOUTH);
}
```

Unsere neue Methode wird direkt im Konstruktor der GUI aufgerufen.
```java
public TicTacToeGUI() {
    super("TicTacToe das Spiel !!!");

    this.initFrame();
}
```

![GUI_BaseLayout](uploads/170a1577975b5b4e9317c34bdf5def79/GUI_BaseLayout.png)

## Das Spielfeld

Das Spielfeld besteht aus 3x3 Feldern, die in unserer GUI mit Hilfe von [JButtons](https://docs.oracle.com/en/java/javase/20/docs/api/java.desktop/javax/swing/JButton.html) dargestellt werden. Während des Spielens von TicTacToe ist es notwendig zu wissen welcher Button gedrückt wurde (Position am Spielfeld). Da der Standardbutton diese Funktionalität nicht bietet, müssen wir ihn um diese Funktionalität erweitern. Dafür erstellen wir unsere eigene Button Klasse `JButtonTicTacToe` und ergänzen die fehlende Funktionalität (eigene Attribute für die Position - Zeile bzw. Spalte - des Buttons).

Im Zuge dessen, können wir auch die Darstellung der Felder anpassen. Die Zustände mit Hilfe von Symbolen (Bilder für leer, Kreuz, Kreis) angezeigt werden. Für die Zustandsänderungen wollen wir 3 Methoden zur Verfügung stellen:
1. **setFree()**: zeigt einen leeren Button an
2. **setPlayer1()**: zeigt das Symbol für den 1. Spieler an
3. **setPlayer2()**: zeigt das Symbol für den 2. Spieler an
Die Bilder für die Anzeige kannst du in hier downloaden:

[TicTacToe_Images.tar](uploads/3160fa40d9bbe6797aea3d51a70f7da9/TicTacToe_Images.tar)

Der Code für unsere eigene `JButtonTicTacToe` Klasse schaut wie folgt aus:
```java
public class JButtonTicTacToe extends JButton {

    private final  Icon iconEmpty;
    private final  Icon iconFirstPlayer;
    private final  Icon iconSecondPlayer;

    public final int ROW;
    public final int COL;

    public JButtonTicTacToe(int row, int col, int size) {
        this.ROW = row;
        this.COL = col;

        this.setText("");
        this.setBackground(Color.WHITE);
        this.setBorderPainted(false);
        this.setPreferredSize(new Dimension(size, size));

        this.iconEmpty = this.createImageIcon("resources/empty.png");
        this.iconFirstPlayer = this.createImageIcon("resources/cross.png");
        this.iconSecondPlayer = this.createImageIcon("resources/circle.png");

        this.setFree();
    }

    private ImageIcon createImageIcon(String filename) {
        ImageIcon imageIcon = new ImageIcon(filename);
        Image image = imageIcon.getImage();
        Image newImg = image.getScaledInstance(this.getPreferredSize().width, this.getPreferredSize().height, java.awt.Image.SCALE_SMOOTH);
        return new ImageIcon(newImg);
    }

    public void setFree() {
        this.setIcon(this.iconEmpty);
    }

    public void setPlayer1() {
        this.setIcon(this.iconFirstPlayer);
    }

    public void setPlayer2() {
        this.setIcon(this.iconSecondPlayer);
    }
}
```

Jetzt müssen wir unsere `JButtonTicTacToe` Buttons nur noch der GUI hinzufügen. Das passiert in der `initFrame()` Methode. Da wir die Buttons Später noch brauchen, legen wir sie in einem 3x3 Feld als Attribut der Klasse ab.

```java
private JButtonTicTacToe[][] boardButtons;
```

```java
int size = 3;
this.boardButtons = new JButtonTicTacToe[size][size];
boardPanel.setLayout(new GridLayout(size, size, TicTacToeGUI.GAP, TicTacToeGUI.GAP));
for (int i = 0; i < size; i++) {
    for (int j = 0; j < size; j++) {
        JButtonTicTacToe newButton = new JButtonTicTacToe(i, j, TicTacToeGUI.BUTTON_SIZE);
        this.boardButtons[i][j] = newButton;
        //newButton.addActionListener(e -> this.actionOnBoardButtonPressed(newButton));
        boardPanel.add(newButton);
    }
}
```

Im Gegensatz zum `BorderLayout` kann man beim [GridLayout](https://docs.oracle.com/en/java/javase/20/docs/api/java.desktop/java/awt/GridLayout.html) die Anzahl der Felder (Zeilen und Spalten) selber definieren. Da TicTacToe auf einem 3x3 Spielfeld gespielt wird, hat auch unser Grid eine größe von 3x3. Die hinzugefügten Buttons werden dann automatisch Feld für Feld zeilenweise hinzugefügt. Der `ActionListener` ist noch auskommentiert und wird später im Tutorium beschrieben.

Unser GUI schaut jetzt wie folgt aus:

![GUI_Grid](uploads/49c4517d47aa5c8b2c00973e8623a4cc/GUI_Grid.png)

## Die Control Buttons

Die Buttons für die Spielsteuerung werden wie die Buttons des Spielfelds in der `initFrame()` Methode hinzugefügt. Wir haben 2 Buttons:
1) **RESET**: startet ein neues Speil
2) **EXIT**: beendet das Programm mit **System.exit(0)**

```java
ctrlPanel.setLayout(new GridLayout(1, 2, TicTacToeGUI.GAP, TicTacToeGUI.GAP));
JButton resetButton = new JButton();
resetButton.setText("Reset");
resetButton.setPreferredSize(new Dimension(1, TicTacToeGUI.BUTTON_SIZE / 2));
//resetButton.addActionListener(e -> this.resetGame());
ctrlPanel.add(resetButton);

JButton exitButton = new JButton();
exitButton.setText("Exit");
exitButton.setPreferredSize(new Dimension(1, TicTacToeGUI.BUTTON_SIZE / 2));
exitButton.addActionListener(e -> System.exit(0));
ctrlPanel.add(exitButton);
```

Auch hier wird der `ActionListener` für das Zurücksetzen des Spiels erst später behandelt. Der **Exit** Button kann das Programm aber schon jetzt beenden.

![GUI_CTRL](uploads/506583b85710a925d13549bfc1a58df9/GUI_CTRL.png)

## Kosmetische Verbesserungen

Irgendwie schaut unser Design - obwohl wir sowohl beim Spielfeld, wie auch im Kontrollbereich, Größen für die Buttons angegeben haben - verzerrt aus. Das liegt daran, dass sich Swing Layouts automatisch an die Größe des Fensters anpassen, d.h. sie ignorieren die Vorgaben, die wir in unserer Implementierung vorgegeben haben. Das kann aber durch wenige Einstellungen unseres `JFrames` in der **main()** Methode angepasst werden:

```java
public static void main(String[] args) {
    JFrame frame = new TicTacToeGUI();
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    //frame.setSize(500, 500);
    frame.pack();
    frame.setResizable(false);
    frame.setLocationRelativeTo(null);
    //frame.setLocationByPlatform(true);
    frame.setVisible(true);
}
```

Anstatt der fixen Fenstergröße (500x500) geben wir mit  **frame.pack()** an, dass sich unser Frame der Größe des Inhalts anpassen soll. Zusätzlich wollen wir, dass der Benutzer die Größe unseres Fensters nicht ändern darf (**frame.setResizable(false)**) und das Fenster zentriert am Monitor geöffnet werden soll (**frame.setLocationRelativeTo(null)**). 

Da wir mit dem Design jetzt fertig sind, können wir die Farben, die wir nur für die Sichtbarkeit des Layouts eingeführt haben (Gelb und Rot), auskommentieren.

Zu allerletzt wollen wir das Icon links oben im Fenster ändern:
```
public TicTacToeGUI() {
    super("TicTacToe das Spiel !!!");
    
    ImageIcon img = new ImageIcon("resources/HTBLuVA_Salzburg_Logo.jpg");
    this.setIconImage(img.getImage());

    this.initFrame();
}
```

Nach diesen Änderungen hat unser Fenster jetzt das gewünschte Aussehen:

![GUI_Final](uploads/1ae033d69733b6a18c84b19c963d4be3/GUI_Final.png)

## Die Spiellogik

Nachdem wir die passende GUI für unser Spiel erstellt haben, können wir uns der Spiellogik widmen. Wir brauchen:
1) Ein Attribut für unsere TicTacToe Klasse **Game**:
```java
private Game game;
```
2) Eine Methode die das Spiel für uns initialisiert:
```java
private void initGame() {
    this.game = new Game("Spieler 1", "Spieler 2");
}
```
3) Einen `ActionListener`, der auf Klicks auf die Felder des Spielfelds reagiert:
4) Eine Methode **resetGame()** die das Spiel zurücksetzt:
5) Die Initialisierung des Spiels im Konstruktor:
```java
public TicTacToeGUI() {
    super("TicTacToe das Spiel !!!");

    ImageIcon img = new ImageIcon("resources/HTBLuVA_Salzburg_Logo.jpg");
    this.setIconImage(img.getImage());

    this.initFrame();
    this.initGame();
}
```

### `ActionListener` für Klicks auf das Spielfeld

Die Klicks auf die Buttons des Spielfelds sind für den [Ablauf des Spiels](#Spielverlauf) zuständig. Nach jedem Klick werden folgende Schritte ausgeführt:
1) Prüfen ob das Feld vom Spieler belegt werden darf
2) Überprüfen ob nach dem Belegen eines Feldes das Spiel gewonnen oder verloren wurde
3) Den Spieler wechseln

Wir wollen diesen Ablauf schrittweise in unsere Benutzeroberfläche einbauen.

### Spiellogik Schritt 1: Setzen von Spielsteinen

Als erstes wollen wir auf Klicks des Spielers reagieren und das Symbol des jeweiligen Spielers anzeigen. Dafür erstellen wir eine Funktion **actionOnBoardButtonPressed()**, die den jeweiligen Button als Argument übernimmt. Wenn das Feld noch frei ist, so soll das Zeichen gesetzt, und der nächste Spieler ausgewählt werden. Die dafür notwendigen Methoden stellt uns die Klasse **Game** zur Verfügung:
```java
private void actionOnBoardButtonPressed(JButtonTicTacToe button) {
    if (this.game.placeToken(button.ROW, button.COL)) {
        if (this.game.getPlayerToken() == Game.TOKEN_FIRST_PLAYER) {
            button.setPlayer1();
        } else {
            button.setPlayer2();
        }
        this.game.changePlayer();
    }
}
```

**ACHTUNG** nicht vergessen den `ActionListener` beim Anlegen der Buttons zu aktivieren (Kommentar entfernen)!

### Spiellogik Schritt 2: Prüfen ob das Spiel zu Ende ist

Im nächsten Schritt wollen wir prüfen ob das Spiel zu Ende ist (Sieg oder Unentschieden). Diese Überprüfung muss vor dem Spielerwechsel eingefügt werden:
```java
if (this.game.checkIfStoneWinsGame(button.ROW, button.COL)) {
    JOptionPane.showConfirmDialog(null, String.format("%s hat gewonnen!!!", this.game.getPlayerName()), "SIEG", JOptionPane.DEFAULT_OPTION);
    this.disableBoardButtons();
} else if (this.game.noFurtherMovesPossible()) {
    JOptionPane.showConfirmDialog(null, "Unentschieden", "UNENTSCHIEDEN", JOptionPane.DEFAULT_OPTION);
    this.disableBoardButtons();
} else {
    this.game.changePlayer();
}
```

Für die Anzeige ob ein Spiel Gewonnen wurde, oder es ohne Sieger geendet hat wird ein eigenes Fenster vom Typ [JOptionPane](https://docs.oracle.com/en/java/javase/20/docs/api/java.desktop/javax/swing/JOptionPane.html) verwendet.

`JOptionPane` ist das Standardialogfenster, der verschiedene Standardoptionen wir z.B.
- nur ein OK Button
- OK und Abbrecken
- ...
anbietet. In unserem Fall haben wir die Defaultoption mit OK Button gewählt.

![GUI_WIN](uploads/c4aa809b2cd00fc430d14ca3cdb2f26c/GUI_WIN.png)

Damit das Spiel nach dem Spielende nicht weiter verändert werden kann, werden die Buttons des Spielfelds deaktiviert. Für die Übersichtlichkeit des Codes wird diese Aufgabe in eine eigene Methode ausgelagert:
```java
private void disableBoardButtons() {
    for (JButton[] row : this.boardButtons) {
        for (JButton button : row) {
            button.setEnabled(false);
        }
    }
}
```

### Neues Spiel erstellen

Wann immer der Spieler auf den Reset-Button drückt soll - unabhängig vom Spielstand - ein neues Spiel erstellt werden. Dafür muss ein neues Spiel initialisiert werden (dafür haben wir schon eine Funktion) und die Buttons in ihren Ausgangszustand (leere Felder) gebracht werden.

```java
private void resetGame() {
    this.resetBoardButtons();
    this.initGame();
}
```

Das zurücksetzen der Buttons in den Ausgangszustand wurde dabei wieder in eine eigene Funktion ausgelagert:
```java
private void resetBoardButtons() {
    for (JButtonTicTacToe[] row : this.boardButtons) {
        for (JButtonTicTacToe button : row) {
            button.setFree();
            button.setEnabled(true);
        }
    }
}
```

**ACHTUNG** nicht vergessen den `ActionListener` für den Reset Button zu aktivieren (Kommentar entfernen)!

Jetzt sollte unsere GUI voll einsatzbereit sein. Die Files für die GUI können hier heruntergeladen werden:

[TicTacToe_GUI.tar](uploads/5eeb8c331fc5e617677f1d0c7aefa204/TicTacToe_GUI.tar)