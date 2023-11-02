## Begriffe
Isotropie = in alle Richtungen gleich ausbreitend

## Abkürzungen
Spatial Analyst Tool = SAT

## Höhenmodell in ArcGIS Pro erstellen
1. Projekt mit Karte und Geodatenbase erstellen > Werkzeug: Raster in Geodatabase > .tiff als Eingabe, .gdb als Ausgabe > Katalog > Datenbanken > Aktualisieren > ausschnitt_harz_utm32 in Darstellungsreihenfolge ziehen
2. Werkzeug fill "Füllung" (SAT) anwenden > neue .tiff importieren
3. Fließrichtung "flow", auch D8 Methode gen., (SAT) berechnen lassen
Zu XY wechseln > Meter einstellen > für X: ```609.286,5```, für Y: ```5.732.838,5``` > z.B. Marker mit Koordinaten für die Darstellung auswählen

<img width="958" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/30bb8258-9b9b-47af-9f35-ee9ccf056ee0">

Auffällig ist, dass die Werte der Farbcodierung der Form 2<sup>0</sup> bis 2<sup>7</sup> entsprichen. Es ist in diesem Fall jedoch nicht anzunehmen, dass ein Zusammenhang zur Bittiefe besteht.

4. Die Werte werden durch den Vergleich von Höhendaten berechnet. Der Wert 4 für die Koordinate ```609.286,5, 5.732.838,5``` weist auf die Flussrichtung nach Süden hin - nach der Logik: 1 = Osten, 2 = Südosten, 4 = Süden, usw.

<img width="162" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/1d86d001-52c9-41da-bb18-abfd5b20fb61">

Der Wert 16 des nördlichen Pixels bedeutet eine Fließrichtung nach Westen.

5. Folgende Pixel sind die 2 niedrigsten:

<img width="162" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/10348066-4925-42af-be5b-8368a04c5a56">

> hier ist die Steigung angegeben, daher negatives Vorzeichen

Beim Nordwestlichen Pixel muss der Satz des Pythagoras angewendet werden. $\frac{20}{\sqrt{25^2+25^2}}*100 = 56,57%$

Die Höhen sind jedes Pixels sind ablesbar und hier einmal eingezeichnet:

<img width="229" alt="Screenshot 2023-10-13 150045" src="https://github.com/s92854/Datenmodellierung/assets/134683810/e1f9f60f-9848-4aab-9d8d-094910d9a641">

> in rot sind die Höhendifferenzen eingetragen

Gefälle in %: $Gefälle = \frac{\Delta Höhe}{horizontale Strecke}*100$

Gefälle in °: $Gefälle = arctan(\frac{\Delta Höhe}{horizontale Strecke})$

&nbsp;

6. Die zwei Pixel mit dem stärksten Gefälle liegen in Nordwest und Süd-Richtung vom Zentrumspixel.

<img width="349" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/60ae47c5-f5d3-4586-a847-708e0cb62d82">

Auffällig ist, dass die Werte aus ArcGIS deutlich kleiner sind als die selbst errechneten Werte. Die Prozentwerte aus ArcGIS in etwa 54% der Werte, die ich extern errechnet habe, entsprechen und die Gradwerte um die 60% des Wertes, der extern errechnet wurde entspricht.

7. In ArcGIS Pro ist der errechnete Wert des Zentrumspixels 18,75° und 33,95%.
8. Das python-Script:

```python
import numpy as np

original_array = ([[695, 717, 718],
                  [705, 715, 716],
                  [699, 699, 701]])



x = ((718 + 2*716 + 701 )*4/4 - (695 + 2*705 + 699)*4/4) / (8*25)
print(x)

y = ((699+2*699+701)*4/4 - (695 + 2* 717 + 718)*4/4)/(8*25)
print (y)

rise_run = np.sqrt ((x)**2 + (y)**2)

slope_degrees = np.arctan (rise_run) * 57.29578

print (slope_degrees)
```

9. Der wesentliche Unterschied zwischen dem Pythonscript und den geometrischen Berechnungen in Aufgabe 7 und 8 ist, dass wir in 7 & 8 die Steigung in % und ° jeweils einzeln mit den gegebenen Werten errechnet haben und das Pythonscript erst die Steigung in Grad berechnet und anschließend diese in Prozent umrechnet.

10. Beim Neigungsoperator handelt es sich um einen fokalen Operator, da er nur die nächstliegenden Pixel in seinem Umkreis-Fenster/Kernel mit in seiner Analyse mit einbezieht.

11. Es handelt sich hierbei um eine "Voronoi-Nachbarschaft", auch "Queen's Case Nachbarschaft" genannt. Bei dieser Art von Nachbarschaft werden alle Pixel in Betracht gezogen, die mindestens einen gemeinsamen Punkt mit der Zelle haben. Die Anzahl der Pixel in der Voronoi-Nachbarschaft hängt von der Anordnung und Verteilung der Pixel im geografischen Raum ab und kann somit variieren.

12. Die Nachbarschaft bei nur einer gemeinsamen Kante wird als "rook-Nachbarschaft" bezeichnet. In dieser hat jede Zelle genau 4 Nachbarn: oben, unten, links und rechts.

13. Man wählt das SAT: Abflussakkumulation (flow accumulation) und gibt das in Aufgabe 3 erstellte flow-Raster als Eingabe ein.

Das Ergebnis ist vorerst ein schwarzes Bild. Anschließend wählt man unter der Registerkarte "Raster-Layer" Streckungstyp und zieht den rechten Slider im Histogramm nach links, bis die Flussverläufe gut zu erkennen sind. Danach haben wir das blaue Farbschema ausgesucht, da es einen guten, aber nicht beißenden Kontrast gibt. Unser Ergebnis sieht dann so aus:

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/651b5cf1-4bcb-4018-b531-57e89f2eac8a">

[//]: <> (Die Zellen, die einen prozentual hohen Zufluss haben, wird ein anderer Farbwert zugewiesen.)

14. Die Werte stellen die kumulierte Anzahl der Zuflusszellen, die Wasser in diese bestimmte Zelle leiten, dar. Zellen mit niedrigen Werten im Abflussakkumulations-Raster erhalten weniger Wasserzulauf aus ihrer Umgebung. Das sind oft Zellen in höher gelegenen Gebieten, die weniger Wasser abfließen lassen.
Zellen mit hohen Werten im Abflussakkumulations-Raster erhalten mehr Wasserzulauf aus ihrer Umgebung. Das sind typischerweise Zellen in niedriger gelegenen Gebieten oder in der Nähe von Wasserquellen, die einen großen Beitrag zum Wasserabfluss leisten.

15. Es handelt sich um einen globalen Operator.

16. Es sind mehrere Tools möglich: das If-Else-Bedinungen Tool, das Set Null Tool und der Raster Calculator. Im If-Else-Bedinungen Tool kann folgende SQL Formel verwendet werden, um das Flusssystem zu extrahieren:

```
VALUE <= 50000
```

Das Tool ist unter den Image-Analyst-Tools zu finden.

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/369a2fbb-e008-45b5-8642-73d8459be649">

17. Im Raster-Calculator verwendet man einen lokalen Operator.

18. Das Tool heißt Wasserlauf-Abschnitte, das Eingabe-Wasserlauf-Raster ist wieder das flow-Raster aus Aufgabe 3 und das Eingabe-Fließrichtungs-Raster ist das If-Else-flow-Raster aus Aufgabe 16.

Die Ganzzahlen haben ausnahmsweise keine Bedeutung, sondern sind lediglich durchnummerierte Zahlen.

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/76294aa7-3828-4c92-8a96-ab9210f79c9e">

19. Wir benötigen das SAT Wasserlauf-Ordnung. Als Wasserlauf-Raster geben wir das gerade erstellte If-Else Raster ein und als Fließrichtungs-Raster das flow-Raster aus Aufgabe 3. Wir erhalten ein Raster mit einer Gliederung von 1 - 8. Dabei bedeutet die 1, dass wenig (am geringsten) Wasser dort zusammenläuft und die 8, dass viel (am meisten) Wasser dort in diesem Punkt zusammenläuft. 1 können dabei Wasserquellen symbolisieren.

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/c5d65c7c-c4f6-4eb7-8d54-770baa9b1c8f">

