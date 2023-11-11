# Übung 2: Raster-Oberflächenanalyse

1. Das **A**dvanced **S**paceborne **T**hermal **E**mission and **R**eflection Radiometer, kurz Aster, ist ein Instrument an Bord der Terra, welches bis zu 14 verschiedene Wellenlängen aufnehmen kann, die vom sichtbaren Licht bis in den Infrarotbereich reichen. Die Bilder haben dabei eine Bodenauflösung von 15 bis 90 m<sup>2</sup> aufnimmt. Das Aster ist das einzige "high spatial resolution" Instrument an Bord der Terra und fungiert so häufig auch als Zoom-Einheit, um so z.B. Veränderungen auf der Erdoberfläche zu untersuchen. Aster kann außerdem stereoskopische Bilder erzeugen, aus denen dann detaillierte, digitale Höhenmodelle erzeugt werden.

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

Raster > Reprojektionen > Transformieren (Reprojizieren)

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

Die Maximalwerte sind im Rasterhistogramm abgebildet und die maximale Höhe beträgt 1587m in diesem Ausschnitt.

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/c566ae81-1c0d-4d43-b95e-bc7b03b8db97">

Dieser Wert kann jedoch nicht stimmen, da der höchste Wert im Harz der Brocken mit rund 1141m (laut Internetrecherche) ist. Die größte Höhe des Brockens liegt laut QGIS bei 1131m (siehe nächstes Bild).

*Wie kriegen wir für unser Höhenmodell die Einstellungen so angepasst, dass auch unsere Extremwerte richtig in der Statistik angezeigt werden?*

**k.A.**

<img width="800" alt="image" src="https://github.com/s92854/Datenmodellierung/assets/134683810/848e8f4d-2a40-4747-88a5-9e1f0cab539f">


### Quellen
https://terra.nasa.gov/about/terra-instruments/aster
