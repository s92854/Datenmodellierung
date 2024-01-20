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
3. Weiterführend wurde mithilfe der AHP-Methode die Gewichtung der ausgewählten Kriterien bestimmt. Folgende Tabelle (Abbildung 1) beschreibt die genutzte Skala. Um die Werte zu ermitteln, wurden für die einzelnen Felder der Vergleichsmatrix $\frac{Row Element}{Column Element}$ gerechnet.

|Zahl|Wichtigkeit|
|--|--|
|1|Gleichwichtig|
|3|Moderate Wichtigkeit|
|5|Hohe Wichtigkeit|
|7|Sehr hohe Wichtigkeit|
|9|Extrem hohe Wichtigkeit|
|2,4,7,8|Zwischenwerte|
|$\frac{1}{3}$, $\frac{1}{5}$, $\frac{1}{7}$, $\frac{1}{9}$|Werte für umgedrehte Vergleiche|

4. Die Gewichtung wurde anhand von eigener Einschätzung bestimmt (Abb. 2).

<img title="Abbildung 2" src="https://github.com/s92854/Datenmodellierung/assets/134683810/b643a2bc-144b-467e-8c24-15ee98f0812f">

Abbildung 2

5. Für die einzelnen Kriterien werden nun die einzelnen Spalten zusammengerechnet (Abb. 3)

<img title="Abbildung 3" src="https://github.com/s92854/Datenmodellierung/assets/134683810/a7fa2700-3084-45ac-9658-ceaa8579d947">

Abbildung 3

6. Normierung der Daten (Abb. 4) &rarr; Wir haben nun unsere finale Gewichtung

<img title="Abbildung 4" src="https://github.com/s92854/Datenmodellierung/assets/134683810/30837efa-7f5c-40b8-a84e-fb5ca99e6006">

Abbildung 4

7. Deutschlandkarte von Natural Earth [herunterladen](https://www.naturalearthdata.com/downloads/10m-cultural-vectors/)
8. Vektor zu Raster mithilfe von **gdalwarp_rasterize** (für Autobahnen sowie Schnellladesäulen) (Code 1) &rarr; es wurden anhand der Daten 6 Klassen definiert (Abb. 5).

**Code 1**
```bash
cd/d “d:\QGIS\bin 
gdal_rasterize -l Highways_only -a nummer -tr 2000.0 2000.0 -a_nodata 0.0 -ot Float32 -of GTiff "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/Highways_only.shp" "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/OUTPUT.tif"
```
Gleiches für die Ladesäulen – Output: ladesaeulen.tif

|Klasse|Abstand zu Autobahn in km|Abstand zu Schnelllader in km|Bevölkerungsdichte|Anzahl Elektroautos|
|--|--|--|--|--|
|1|> 20|< 5|0 - 100|0 - 499|
|2|15 - 20|5 - 10|< 100 - 200|500 - 999|
|3|10 - 15|10 - 15|< 200 - 500|1000 - 1999|
|4|6 - 10|15 - 18|< 500 - 1000|2000 - 4999|
|5|3 - 6|18 - 20|> 1000 - 2000|5000 - 9999|
|6|< 3|> 20|< 2000|< 10000|

Abbildung 5. Es galt: min. < Wert <= max.

9. Um die Rasterdaten (Autobahn & Schnelllader) zu bekommen, wurden zunächst die Koordinatensysteme auf 4839 gebracht, um ein einheitliches zu haben. Anschließend wurden Abstände von Autobahnen und Schnellladesäulen erzeugt (Code 2).

**Code 2**
```bash
gdalwarp -s_srs EPSG:3857 -t_srs EPSG:4839 -tr 2000 2000 -r near -of GTiff "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/ladesaeulen.tif" "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/ladesaeulen2.tif"
```

Unter GDAL &rarr; Rasteranalyse &rarr; Nähe mit folgenden Einstellungen:
```
gdal_proximity.bat -srcband 1 -distunits GEO -nodata 0.0 -ot Float32 -of GTiff "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/ladesaeulen.tif" "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/ladesäulen_proximity.tif"
```

10. Nun müssen die Layer noch auf Deutschland zugeschnitten werden, da sie die Abstände über die Landesgrenzen hinaus messen (Code 3).

**Code 3**
```bash
gdalwarp -overwrite -of GTiff -cutline "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/ne_10m_admin_0_countries_deu.shp" -cl ne_10m_admin_0_countries_deu -crop_to_cutline -dst nodata -1.0 "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/autobahnen_proximity.tif" "D:/Onedrive/OneDrive - Berliner Hochschule für Technik/Desktop/Semester 3/Datenmodellierung_GIS/abschlussprojekt/maske.tif"
```

11. Es werden die Daten der erstellten Rasterlayer mit dem Verarbeitungstool „nach Tabelle neuklassifiziert“ nach Abb. 5 sortiert.
12. Nun muss man die Vektordaten (Bevölkerung&Elektroautozahlen) in Rasterdaten umwandeln, um sie mit den restlichen Rasterdaten interagierbar zu machen: Raster &rarr; Konvertierung &rarr; Rastern
13. Die Ergebnisse können nun projiziert werden (Code 4) &rarr; es kam jedoch zu einer Fehlermeldung, welche mit **gdalwarp** behoben wurde (Code 5). Die Dimensionen der verschiedenen Karten wurden auf die der Bevölkerungsdichte angepasst (Abb. 6).

**Code 4**
```bash
gdal_calc.py -A "D:\Onedrive\OneDrive - Berliner Hochschule für Technik\Desktop\Semester 3\Datenmodellierung_GIS\abschlussprojekt\reclass\ev_raster.tif" -B "D:\Onedrive\OneDrive - Berliner Hochschule für Technik\Desktop\Semester 3\Datenmodellierung_GIS\abschlussprojekt\reclass\bev_raster.tif" -C "D:\Onedrive\OneDrive - Berliner Hochschule für Technik\Desktop\Semester 3\Datenmodellierung_GIS\abschlussprojekt\reclass\reclass_autobahn_2.tif" -D "D:\Onedrive\OneDrive - Berliner Hochschule für Technik\Desktop\Semester 3\Datenmodellierung_GIS\abschlussprojekt\reclass\resampled_ladesäulen_2.tif" --outfile "D:\Onedrive\OneDrive - Berliner Hochschule für Technik\Desktop\Semester 3\Datenmodellierung_GIS\abschlussprojekt\reclass\ergebnis.tif" --calc="(0.2323*A + 0.1523*B + 0.4382*C + 0.1763*D)/1" --NoDataValue=0
```

**Code 5**
```bash
gdalwarp -ts 321 434 -r near -of GTiff -te 279371.0591140603646636 5234486.8776375111192465 921371.0591140603646636 6102486.8776375111192465 -s_srs EPSG:4839 -t_srs EPSG:25832 -ot Float32 "D:\Onedrive\OneDrive - Berliner Hochschule für Technik\Desktop\Semester 3\Datenmodellierung_GIS\abschlussprojekt\reclass\reclass_autobahn.tif" "D:\Onedrive\OneDrive - Berliner Hochschule für Technik\Desktop\Semester 
3\Datenmodellierung_GIS\abschlussprojekt\reclass\reclass_autobahn_2.tif"
```

<img title="Abbildung 6" src="https://github.com/s92854/Datenmodellierung/assets/134683810/3029a954-37e2-4398-9b4a-cb4e49ba8a4d">

Abbildung 6
