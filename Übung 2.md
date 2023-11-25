# Übung 2: Raster-Oberflächenanalyse

Die Dateien bis Aufgabe 11 findet ihr [hier](https://cloud.bht-berlin.de/index.php/s/ETzjfgMymbAeXAc)

1. Das **A**dvanced **S**paceborne **T**hermal **E**mission and **R**eflection Radiometer, kurz Aster, ist ein Instrument an Bord der Terra, welches bis zu 14 verschiedene Wellenlängen aufnehmen kann, die vom sichtbaren Licht bis in den Infrarotbereich reichen. Die Bilder haben dabei eine Bodenauflösung von 15 bis 90 m<sup>2</sup> aufnimmt. Das Aster ist das einzige "high spatial resolution" Instrument an Bord der Terra und fungiert so häufig auch als Zoom-Einheit, um so z.B. Veränderungen auf der Erdoberfläche zu untersuchen. Aster kann außerdem stereoskopische Bilder erzeugen, aus denen dann detaillierte, digitale Höhenmodelle erzeugt werden.

&nbsp;

2. 
Projektion: WGS84 - Mercator
Länge Halbachse: 

Projektion auf UTM32 umstellen

<img width="428" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/dbc45f7f-db43-41c3-8db5-599c21beb61d">

Neuen Polygonlayer erstellen > Rechtsklick in Vektorwerkzeugeleiste (siehe Bild 1.) > Erweiterte Digitalisierungsleiste einschalten > in den Bearbeitungsmodus wechseln > Neues Polygon erstellen > Erweiterte Werkzeuge einschalten (5.)

<img width="1400" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/535b4f7a-8a40-46ce-a642-b39c72d2bd4a">

Zuerst sperrt man die Koordinaten, sodass diese nur durch manuelle Eingabe geändert werden können. Anschließend werden die Koordinten

1:```X = 575000``` ```Y = 5760000```,

2:```X = 634000``` ```Y = 5760000```,

3:```X = 634000``` ```Y = 5700000```,

4:```X = 575000``` ```Y = 5700000```

und wieder Koordinate 1, in das erweiterte Digitalisierungswerkzeug eingetragen. Durch Rechtsklick in das Quadrat kann abschließend eine ID vergeben und das Objekt fertig gestellt werden.

<img width="500" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/fc3e87e2-2aae-47c9-8c8e-b8dd65827bfe">

&nbsp;

3. Raster > Reprojektionen > Transformieren (Reprojizieren)

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/58b1de8c-64c0-4dee-b132-c9214963f54d">

&nbsp;

Raster > Extraktion > Raster auf Layermaske zuschneiden > Polygon als Maske wählen

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/86c58aae-6be4-4abc-8328-e00a390d1f85">

&nbsp;

Raster > Extraktion > Kontur

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/82f89c7f-7f81-450e-84ee-c933337f5b80">

Im Vergleich zur Konturvisualisierung der Original .tif Datei werden die Linien normalisiert.

<img width="1200" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/5220e6ca-b9cd-412e-9172-1f1b2d8ef35f">


&nbsp;

4. Die Maximalwerte sind im Rasterhistogramm abgebildet und die maximale Höhe beträgt 1587m in diesem Ausschnitt.

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/c566ae81-1c0d-4d43-b95e-bc7b03b8db97">

Dieser Wert kann jedoch nicht stimmen, da der höchste Wert im Harz der Brocken mit rund 1141m (laut Internetrecherche) ist. Die größte Höhe des Brockens liegt laut QGIS bei 1131m (siehe nächstes Bild).

*Wie kriegen wir für unser Höhenmodell die Einstellungen so angepasst, dass auch unsere Extremwerte richtig in der Statistik angezeigt werden?*

**k.A.**

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/848e8f4d-2a40-4747-88a5-9e1f0cab539f">

&nbsp;

5. 

Infos der Originaldatei:

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/827dc46b-da1b-4e0f-9409-00eb4d04ed02">
<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/be2672da-6baf-42ae-8c6c-a1febe1db71a">

&nbsp;

Infos des Ausschnitts:

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/4c67d479-74bf-403b-a81b-db1fbbdb6059">
<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/1b1fb8d5-c87a-4d97-bf18-b724fb50e693">

Beide Dateien haben eine angegebene Bodenauflösung von rund 20m. Auffällig ist, dass die Pixelanzahl der Originaldatei mit 3601x3601 angegeben, das Bild jedoch nicht quadratisch ist. Zommt man ran, erkennt man, dass die Pixel rechteckig sind. Der konvertierte Ausschnitt des Harzes hat jedoch quadratische Pixel mit einer angegebenen und gemessenen Pixelgröße von rund 20m.

<img width="1200" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/8d676ba0-6201-4228-bdcb-db4471f6825b">

Seltsamer Weise stehen jedoch nirgends die exakten Ausmaße der Pixel der Originaldatei.

&nbsp;

6.

Im bin-Ordner von QGIS - standardmäßig ```C:\Program Files\QGIS %version%\bin``` ist die ```gdalwarp.exe``` zu finden.

Die Hauptfunktion von gdaltindex.exe besteht darin, einen Index für eine Sammlung von Rasterdatensätzen zu erstellen. Dieser Index ist eine Datei, die Informationen über die enthaltenen Rasterdateien enthält, wie ihre Namen, Pfade und räumliche Ausdehnung. Der Tileindex ermöglicht es, schnell auf bestimmte Rasterdatensätze zuzugreifen, ohne alle Dateien einzeln durchsuchen zu müssen.

```batch
"C:\Program Files\QGIS 3.30.1\bin\gdalwarp.exe" -s_srs EPSG:4326 -t_srs EPSG:25832 -tr 25m 25m -te 575000 5700000 634000 5760000 -of GTiff "C:\Users\%username%\Documents\ASTGTMV003_N51E010_dem.tif" "C:\Users\%username%\Documents\Output.tif"
pause
```

&nbsp;

7. Mit dem Tool Schmummerung (Raster > Analyse > Schmummerung)

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/1ab4ecf6-ea95-455d-9c32-ad65a2ea411f">

&nbsp;

8. Der Lichteinstrahl- (Azimutalwinkel) liegt bei 315°. Das entspricht Nordwesten.

&nbsp;

9. Auch in ArcGIS Pro liegt der Sonneneinfallswinkel bei 315°

<img width="500" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/6a46aaff-5e7d-4bad-bdc7-b0ec3cc5ee69">

&nbsp;

10.
```batch
"C:\Program Files\QGIS 3.30.1\bin\gdalwarp.exe" -s_srs EPSG:4326 -t_srs EPSG:25832 -tr 25m 25m -te 575000 5700000 634000 5760000 "C:\Users\%username%\Documents\ASTGTMV003_N51E010_dem.tif" "C:\Users\%username%\Documents\Output.tif"
"C:\Program Files\QGIS 3.30.1\bin\gdaldem.exe" slope "C:\Users\%username%\Documents\ausschnitt_harz_utm32.tif" "C:\Users\%username%\Documents\ausschnitt_harz_slope.tif" -alg ZevenbergenThorne
"C:\Program Files\QGIS 3.30.1\bin\gdaldem.exe" aspect "C:\Users\%username%\Documents\ausschnitt_harz_utm32.tif" "C:\Users\%username%\Documents\ausschnitt_harz_aspect.tif" -alg ZevenbergenThorne
pause
```

&nbsp;

11. Es handelt sich dabei um fokale Rasteranalysen.

&nbsp;

12. 

```batch
cd /d "C:\Program Files\QGIS 3.30.1\bin"
set folder="C:\Users\%username%\Documents"
echo %folder%
set log=log.log
echo %log%
del %folder%\%log%
for %%i in ("%folder%\*.tif") do (
  gdalinfo.exe %%i >> %folder%\%log%
  echo. >> %folder%\%log%
  echo ****************** >> %folder%\%log%
  echp. >> %folder%\%log%
)
pause
```

&nbsp;

13. ```"ausschnitt_harz_aspect@1" >= 250 AND "ausschnitt_harz_aspect@1" <= 290 AND "ausschnitt_harz_slope@1" <= 25 AND "Output@1" >= 700```

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/0df3120e-b872-4e22-94c8-51b924c73700">

&nbsp;

14. Symbolisierung > Darstellungsart: Paletten-/ Eindeutige Werte

<img width="900" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/c8068ab4-2e7d-450b-98f6-9d17c1c8d7e8">

<img width="900" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/85ec99bd-6add-4d9a-9f39-820833ab8ab5">

&nbsp;

15. Raster > Analyse > Sieben > Input: gerade eben erstelltes Binärbild > Schwellenwert: 8

<img width="700" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/ed379e6b-aff9-4093-8957-be021e8d519a">

&nbsp;

16. Raster > Rasterrechner > ```"ausschnitt_harz_aspect_slope_sieve@1" = 1```

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/ce439fb1-1905-4fe3-8407-089f75cfcc34">

&nbsp;

17. Raster > Konvertieren > Vektorisieren

Attributtabelle öffnen > Bearbeitungsmodus aktivieren > Feldrechner > ```$area / 10000``` > Namen wählen (hier: ha) und Ausgabefeldtyp auf Real stellen > Zeile mit der größten Zahl (rund 353515) wählen und löschen > Speichern

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/c1f1d887-717e-4a27-a97f-290580e84281">

18. Attributtabelle öffnen > Objekte über Ausdruck wählen > ```ha < 3``` > Objekte wählen und löschen (28 müssen übrig bleiben)

&nbsp;

19. Vektor > Geometrie-Werkzeuge > Zentroide

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/be94f2a3-a092-463e-8759-29241f3b74a6">

&nbsp;

20. Feldrechner > Neue Spalte > Name: pk > ```@id```

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/69e6c930-d4cd-49a7-b2f5-da26806e5ded">

&nbsp;

21. Vektor > Analyse-Werkzeuge > Distanzmatrix

&nbsp;

22. 
### Kürzeste & längste Distanz
|pk|Distanz||
|--|--|--|
|0|6841,79m|kürzeste Distanz|
|13|20305,23m|längste Distanz|

&nbsp;

23. Erweiterungen > Visibility Analysis

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/b344d1f5-7089-4f96-b630-cf4992c3afbc">

Layer > Neuen Shapedateilayer erstellen > Geometrietyp: Punkt > Layer bearbeiten > Punkt hinzufügen > Punkt in Altenau wählen

Visibility Analysis > Create Viewpoints > Altenaupunkt als Observerlocation und als Digital elevation model das Layer aus Aufgabe 16 verwenden:

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/a86dd54c-b44f-4a32-8756-6889d0ee14f1">

Visibility Analysis > Viewshed > Altenau Viewpoint als Observerlocation und als digital elevation model Output aus Aufgabe 6 verwenden:

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/cfe8c181-31af-4009-96cf-d6da71fd86d1">

Nun Transparenz aller 0-Werte auf 0 und 1-Werte eine andere Farbe geben und Transparenz herunter setzen. Alle Punkte der Distanzen löschen, die innerhalb dieser Fläche sind. Es bleiben 16 Standorte übrig.

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/679308e2-a0f5-495c-a24f-2c97c8311cb1">

&nbsp;

24. Die Koordinaten für pk=4 lauten: ```x = 605548,213```, ```y = 5745815,342```.

&nbsp;

25. Das Eingaberaster ist das slope Raster.

&nbsp;

26. rund 3336


### Quellen
https://terra.nasa.gov/about/terra-instruments/aster


Nico Haupt (956450)
Tara Richter (934172)
