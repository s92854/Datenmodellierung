## Begriffe
Isotropie = in alle Richtungen gleich ausbreitend

## Abkürzungen
Spatial Analyst Tool = SAT

## Höhenmodell in ArcGIS Pro erstellen
1. Projekt mit Karte und Geodatenbase erstellen > .tiff Datei unter Darstellungsreihenfolge ziehen
2. fill "Füllung" (SAT) tiff erstellen 
3. Fließrichtung "flow", auch D8 Methode gen., (SAT) berechnen lassen
Zu XY wechseln > Meter einstellen > für X: ```609.286,5```, für Y: ```5.732.838,5``` > z.B. Marker mit Koordinaten für die Darstellung auswählen

<img width="958" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/30bb8258-9b9b-47af-9f35-ee9ccf056ee0">

Auffällig ist, dass die Werte der Farbcodierung der Form 2<sup>0</sup> bis 2<sup>7</sup> entsprichen. Es ist in diesem Fall jedoch nicht anzunehmen, dass ein Zusammenhang zur Bittiefe besteht.

4. Die Werte werden durch den Vergleich von Höhendaten berechnet. Der Wert 4 für die Koordinate ```609.286,5, 5.732.838,5``` weist auf die Flussrichtung nach Süden hin - nach der Logik: 1 = Osten, 2 = Südosten, 4 = Süden, usw.

<img width="162" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/1d86d001-52c9-41da-bb18-abfd5b20fb61">

Der Wert 16 des nördlichen Pixels bedeutet eine Fließrichtung nach Westen.

5. Folgende Pixel sind die 2 niedrigsten:

<img width="162" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/70dffd86-d2ee-4d4b-9a69-be9f19a990ed">

> hier ist die Steigung angegeben, daher negatives Vorzeichen

Die Höhen sind jedes Pixels sind ablesbar und hier einmal eingezeichnet:

<img width="229" alt="Screenshot 2023-10-13 150045" src="https://github.com/s92854/Datenmodellierung/assets/134683810/e1f9f60f-9848-4aab-9d8d-094910d9a641">

> in rot sind die Höhendifferenzen eingetragen

Gefälle in %: $Gefälle = \frac{\Delta Höhe}{horizontale Strecke}*100$

Gefälle in °: $Gefälle = arctan(\frac{\Delta Höhe}{horizontale Strecke})$

&nbsp;

6. Die zwei Pixel mit dem stärksten Gefälle liegen in Nordwest und Süd-Richtung vom Mittelpixel

<img width="349" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/60ae47c5-f5d3-4586-a847-708e0cb62d82">

Auffällig ist, dass die Werte aus ArcGIS deutlich kleiner sind als die selbst errechneten Werte. Die Prozentwerte aus ArcGIS in etwa 54% der Werte, die ich extern errechnet habe, entsprechen und die Gradwerte um die 60% des Wertes, der extern errechnet wurde entspricht.
