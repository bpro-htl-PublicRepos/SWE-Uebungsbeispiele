Erstellen Sie 2 Methoden, die ein quadratische Gleichung mit Hilfe der **pq-Formel** bzw. der **ABC-Formel** berechnet. Die Faktoren der Gleichungen sollen als Parameter übergeben werden. Die Ausgabe soll folgendes umfassen:

- die Gleichung an sich
- die Faktoren der Gleichung
- die Lösungen

Beispiel-Output für (**pq-Formel)**:

```
Gleichung:
x^2 - 2 * x - 40 = 0

Faktoren:
p = -2
q = -40

Lösungen:
x1 = 7.4
x2 = -5.4
```

Für den Fall dass es keine reelen Lösungen gibt soll die Ausgabe wie folgt aussehen (**ABC-Formel**):

```
Gleichung:
3 * x^2 - 5 * x + 1 = 0

Faktoren:
A = 3
B = -5
C = 1

Lösungen:
Komplex
```

# pq-Formel (kleine Lösungsformel)

Format:

```math
x^2 + p \cdot x + q = 0
```

Lösungsformel:

```math
x_{1,2} = -\frac{p}{2} \pm\sqrt{\left(\frac{p}{2}\right)^2 - q}
```

# ABC-Formel (große Lösungsformel)

Format:

```math
A \cdot x^2 + B \cdot x + C = 0
```

Lösungsformel:

```math
x_{1,2} = \frac{-B \pm \sqrt{B^2 - 4 \cdot A \cdot C}}{2 \cdot A}
```