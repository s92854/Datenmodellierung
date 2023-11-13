# Übung 2: Raster-Oberflächenanalyse

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

Im Vergleich zur Konturvisualisierung der Original .tiff Datei werden die Linien normalisiert.

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

### Lange Version mit Variablen:

```batch
@echo off

set "QGIS_Version=3.30.1"
set "path=C:\Program Files\QGIS %QGIS_Version%\bin"

set "EingabeLayer=Eingabe.tif"
set "AusgabeLayer=Ausgabe.tif"

set "xmin="
set "ymin="
set "xmax="
set "ymax="

cd /d "%path%"
gdalwarp -overwrite -tr 25 25 -r near -te %xmin% %ymin% %xmax% %ymax% -of GTiff "%EingabeLayer%" "%AusgabeLayer%"
pause
```

&nbsp;

### Kurze Version ohne Variablen:

```batch
cd "C:\Program Files\QGIS 3.30.1\bin\"
gdalwarp -overwrite -tr 25 25 -r near -te %xmin% %ymin% %xmax% %ymax% -of GTiff "C:\Documents\ASTGTMV003_N51E010_dem.tif" "C:\Documents\Output.tif"
pause
```

> Ohne Pfadangabe wird die Datei mit dem übereinstimmenden Namen im selben Ordner, wie die .bat Datei gewählt und der Output auch wieder in diesen Ordner geschrieben

[//]: # (x und y min und max gegen Werte ersetzen)


### Quellen
https://terra.nasa.gov/about/terra-instruments/aster
