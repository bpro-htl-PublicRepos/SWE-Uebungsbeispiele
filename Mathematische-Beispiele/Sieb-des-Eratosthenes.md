Das Sieb des Eratosthenes ist ein Algorithmus zur Bestimmung einer Liste oder Tabelle aller Primzahlen kleiner oder gleich einer vorgegebenen Zahl. Es ist nach dem griechischen Mathematiker Eratosthenes benannt. Allerdings hat Eratosthenes, der im 3. Jahrhundert v. Chr. lebte, das Verfahren nicht entdeckt, sondern nur die Bezeichnung „Sieb“ für das schon lange vor seiner Zeit bekannte Verfahren eingeführt.

# Funktionsweise

Zunächst werden alle Zahlen 2, 3, 4, … bis zu einem frei wählbaren Maximalwert S aufgeschrieben. Die zunächst unmarkierten Zahlen sind potentielle Primzahlen. Die kleinste unmarkierte Zahl ist immer eine Primzahl. Nachdem eine Primzahl gefunden wurde, werden alle Vielfachen dieser Primzahl als zusammengesetzt markiert. Man bestimmt die nächstgrößere unmarkierte Zahl. Da sie kein Vielfaches von Zahlen kleiner als sie selbst ist (sonst wäre sie markiert worden), kann sie nur durch eins und sich selbst teilbar sein. Folglich muss es sich um eine Primzahl handeln. Diese wird dementsprechend als Primzahl ausgegeben. Man streicht wieder alle Vielfachen und führt das Verfahren fort, bis man am Ende der Liste angekommen ist. Im Verlauf des Verfahrens werden alle Primzahlen ausgegeben.

Da mindestens ein Primfaktor einer zusammengesetzten Zahl immer kleiner gleich der Wurzel der Zahl sein muss, ist es ausreichend, nur die Vielfachen jener Primzahlen zu streichen, die kleiner oder gleich der Wurzel der Schranke S sind.

Ebenso genügt es beim Streichen der Vielfachen, mit dem Quadrat der Primzahl zu beginnen, da alle kleineren Vielfachen bereits markiert sind.

Das Verfahren beginnt also damit, die Vielfachen 4, 6, 8, … der kleinsten Primzahl 2 durchzustreichen. Die nächste unmarkierte Zahl ist die nächstgrößere Primzahl, die 3. Anschließend werden deren Vielfache 9, 12, 15, … durchgestrichen, und so weiter. 

Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Sieb_des_Eratosthenes)