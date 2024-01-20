# Abschlussprojekt: E-Ladesäulen in Deutschland und ihre Anbindung an die deutschen Autobahnen

### Alexander Radünz (950795), Nico Haupt (956450), Tara Richter (934172) und Tilman Frauenstein (956182)

&nbsp;

## Datengrundlange
* Die Daten der Ladesäulen basieren auf den Daten von [ESRI](https://hub.arcgis.com/maps/bc3c97f73d6b4be4921be8560fbc325a) aus 2023. [DOWNLOAD](https://github.com/s92854/Datenmodellierung/files/13966254/LadesA4ulen_in_Deutschland.zip), entpackt ca. 78MB groß.
* Zusätzlich wurden die Highways von OSM verwendet. [DOWNLOAD](https://github.com/s92854/Datenmodellierung/files/13966279/Strassen.Deutschland.zip), entpackt ca. 112MB groß.

&nbsp;

## Operationen/Vorgehensweise
1. Um die Performance der Highways zu verbessern wurden alle Spalten, bis auf *id* und *ref*, gelöscht. Die gelöschten Spalten beinhalteten hauptsächlich *NULL*-Werte, sowie Daten, die für unsere Untersuchungen nicht notwendig sind. Zusätzlich wurden die Autobahnen A1 - A10 in jeweils einzelne, A20 - A29, A30 - A39 und alle ab A40 in eigene Shapefiles exportiert.
2. Um die Schnellladeeinrichtungen von den normalen zu separieren wurden alle drei Arten ('Normalladeeinrichtung' und 'Schnellladeeinrichtung', welche ab 150kW als 'High-Power-Ladeeinrichtung' gilt) in neue Shapefiles exportiert. Dazu wurde in QGIS die Funktion **Objekte über Ausdruck wählen** verwendet: ```"Art_der_La" = 'Schnellladeeinrichtung'```
3. Weiterführend wurde mithilfe der AHP-Methode die Gewichtung der ausgewählten Kriterien bestimmt. Abbildung 1 beschreibt die genutzte Skala. Um die Werte zu ermitteln, wurde für die einzelnen Felder der Vergleichsmatrix.
4. Die Gewichtung wurde anhand von eigener Einschätzung bestimmt (Abb. 2).
5. Für die einzelnen Kriterien werden nun die einzelnen Spalten zusammengerechnet (Abb. 3)
6. Normierung der Daten (Abb. 4) -> Wir haben nun unsere finale Gewichtung
7. Deutschlandkarte von Natural Earth [herunterladen](https://www.naturalearthdata.com/downloads/10m-cultural-vectors/)
8. Vektor zu Raster mithilfe von gdalwarp_rasterize – Für Autobahnen sowie Schnellladesäulen (Code 1) &rarr; es wurden anhand der Daten 6 Klassen definiert (Abb. 5).
9. Um die Rasterdaten (Autobahn & Schnelllader) zu bekommen, wurden zunächst die Koordinatensysteme auf 4839 gebracht, um ein einheitliches zu haben. Anschließend wurden Abstände von Autobahnen und Schnellladesäulen erzeugt (Code 2).
10. Nun müssen die Layer noch auf Deutschland zugeschnitten werden, da sie die Abstände über die Landesgrenzen hinaus messen (Code 3).
11. Es werden die Daten der erstellten Rasterlayer mit dem Verarbeitungstool „nach Tabelle neuklassifiziert“ nach Abb. 5 sortiert.
12. Nun muss man die Vektordaten (Bevölkerung&Elektroautozahlen) in Rasterdaten umwandeln, um sie mit den restlichen Rasterdaten interagierbar zu machen: Raster &rarr; Konvertierung &rarr; Rastern
13. Die Ergebnisse können nun projiziert werden (Code 4) &rarr; es kam jedoch zu einer Fehlermeldung, welche mit **gdalwarp** behoben wurde (Code 5). Die Dimensionen der verschiedenen Karten wurden auf die der Bevölkerungsdichte angepasst (Abb. 6).
