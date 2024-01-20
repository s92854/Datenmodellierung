# Abschlussprojekt: E-Ladesäulen in Deutschland und ihre Anbindung an das Verkehrsnetz
Auswirkungen anthropologischen Bauens - Windräder

### Alexander Radünz (950795), Nico Haupt (956450), Tara Richter (934172) und Tilman Frauenstein (956182)

&nbsp;

## Datengrundlange
* Die Daten der Ladesäulen basieren auf den Daten von [ESRI](https://hub.arcgis.com/maps/bc3c97f73d6b4be4921be8560fbc325a) aus 2023. [DOWNLOAD](https://github.com/s92854/Datenmodellierung/files/13966254/LadesA4ulen_in_Deutschland.zip), entpackt ca. 78MB groß.
* Zusätzlich wurden die Highways von OSM verwendet. [DOWNLOAD](https://github.com/s92854/Datenmodellierung/files/13966279/Strassen.Deutschland.zip), entpackt ca. 112MB groß.

&nbsp;

## Operationen/Vorgehensweise
1. Um die Performance der Highways zu verbessern wurden alle Spalten, bis auf *id* und *ref*, gelöscht. Die gelöschten Spalten beinhalteten hauptsächlich *NULL*-Werte, sowie Daten, die für unsere Untersuchungen nicht notwendig sind. Zusätzlich wurden die Autobahnen A1 - A10 in jeweils einzelne, A20 - A29, A30 - A39 und alle ab A40 in eigene Shapefiles exportiert.
2. Um die Schnellladeeinrichtungen von den normalen zu separieren wurden alle drei Arten ('Normalladeeinrichtung' und 'Schnellladeeinrichtung', welche ab 150kW als 'High-Power-Ladeeinrichtung' gilt) in neue Shapefiles exportiert. Dazu wurde in QGIS die Funktion **Objekte über Ausdruck wählen** verwendet: ```"Art_der_La" = 'Schnellladeeinrichtung'```
3. Für Analysezwecke wurden verschiedene **Puffer** generiert:

|Puffer|Zweck/Grund|Radius|Anzahl|
|--|--|--|--|
|Puffer um jede Schnellladesäule|Da die durchschnittliche Reichweite eines E-Fahrzeugs ca. 200km beträgt, nehmen wir an, dass man normalerweise bei 10% restlicher Akkuladung eine Ladesäule aufsucht. Wenn nun also alle Ladesäulen bei einem Standort belegt sind, hat man die Ausweichmöglichkeiten, die innerhalb dieses Puffers und dem aktuellen Standort liegen.|20km|2|
|Puffer um Autobahnen|Die Ladesäule soll nicht weit von der Autobahn entfernt sein, um weitere Probleme und Entladung zu umgehen.|2km|1|
|||||
|Vereinter Puffer der Ladesäulen|Zwischenschritt der Analysezwecke|20km|1|
|Differenzpuffer von Ladesäulen und Highways|Um die Teile der Autobahn sichtbar zu machen, die noch über keine Schnellladeeinrichtung verfügen. Mögliche Standpunkte.|2km|1|

<img title="Puffer um Autobahnen" height="800" src="https://github.com/s92854/Datenmodellierung/assets/134683810/a7aafe0c-89b8-4dc9-a31f-dfaa2bc50736">

4. Die **Vereinigung** kombinierte die Puffer beider Arten von 'Schnellladeeinrichtungen'. Anschließend wurde die Operation **Auflösen** verwendet, um die Linien innerhalb des Polygons zu entfernen und so ein einziges zusammenhänges Polygon zu erhalten.

<img title="Vereinigung" height="800" src="https://github.com/s92854/Datenmodellierung/assets/134683810/72d27161-6fce-4372-9c3a-c66fd82316be">

5. Durch eine **Differenz** des großen Puffers mit dem der Autobahnen, ergeben sich Abschnitte an Puffern um die Autobahnen, die nicht innerhalb des 20km-Radius von Schnellladesäulen liegen. Diese Bereiche sind somit potentielle Standorte für neue Ladesäulen.

<img title="Ladesäulenfreie Abschnitte" height="800" src="https://github.com/s92854/Datenmodellierung/assets/134683810/b78d3fd1-e069-4c82-919a-b73d79986c79">

6. Mithilfe einer weiteren **Vereinigung** wurden alle 'Schnellladeeinrichtungen' zu einem Punktlayer zusammengefasst und so wird die Heatmap darstellbar.

<img title="Heatmap" height="800" src="https://github.com/s92854/Datenmodellierung/assets/134683810/90e48475-e5e1-487e-bf01-aeb8169e8942">
