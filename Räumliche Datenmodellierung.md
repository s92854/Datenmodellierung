## Begriffe
Isotropie = in alle Richtungen gleich ausbreitend

## Abkürzungen
Spatial Analyst Tool = SAT

## Höhenmodell in ArcGIS Pro erstellen
1. Projekt mit Karte und Geodatenbase erstellen
2. .tiff Datei unter Darstellungsreihenfolge ziehen
3. fill "Füllung" (SAT) tiff erstellen 
4. Fließrichtung "flow", auch D8 Methode gen., (SAT) berechnen lassen
5. Zu XY wechseln > Meter einstellen > für X: ```609.286,5```, für Y: ```5.732.838,5``` > z.B. Marker mit Koordinaten für die Darstellung auswählen

<img width="958" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/30bb8258-9b9b-47af-9f35-ee9ccf056ee0">

Auffällig ist, dass die Werte der Farbcodierung der Form 2<sup>0</sup> bis 2<sup>7</sup> entsprichen. Es ist in diesem Fall jedoch nicht anzunehmen, dass ein Zusammenhang zur Bittiefe besteht.

6. Die Werte werden durch den Vergleich von Höhendaten berechnet. Der Wert 4 für die Koordinate ```609.286,5, 5.732.838,5``` weist auf die Flussrichtung nach Süden hin - nach der Logik: 1 = Osten, 2 = Südosten, 3 = Süden, usw.

<img width="162" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/1d86d001-52c9-41da-bb18-abfd5b20fb61">

Der Wert 16 des nördlichen Pixels bedeutet eine Fließrichtung nach Westen.

7. 
