Schreiben Sie ein Programm das die Rate einer einfachen Haushaltsversicherung berechnet. Die entscheidenden Faktoren für die Höhe der Prämie sind die im Haushalt lebenden Personen und die Wohnfläche. Die Prämie soll wie folgt berechnet werden:

| Anzahl Personen  | Prämie                |
|------------------|-----------------------|
| 1-2 Personen     | 10 + Wohnfläche / 2   |
| 3 Personen       | 15 + Wohnfläche       |
| 4 Personen       | 15 + 1.5 * Wohnfläche |
| > 4 Personen     | 25 + 2 * Wohnfläche   |

Die Anzahl der Personen und die Wohnfläche sollen über die CommandLine eingelesen werden. Die Ausgabe des Programms soll wie folgt laugen:

```
[IN] Wohnfläche:          300
[IN] Anzahl der Bewohner: 2
Prämie der Haushaltsversicherung: 160
```

**Achtung:** Überlegen Sie Sich welche Werte für die Eingaben gültig sind und stellen Sie sicher dass keine ungültigen Werte eingegeben wurden.