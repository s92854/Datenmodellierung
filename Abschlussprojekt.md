# Abschlussprojekt: E-Ladesäulen in Deutschland und ihre Anbindung an das Verkehrsnetz
Auswirkungen anthropologischen Bauens - Windräder

### Alexander Radünz (), Nico Haupt (956450), Tara Richter (934172) und Tilman Frauenstein ()

&nbsp;

## Datengrundlange
* Die Daten der Ladesäulen basieren auf den Daten von [ESRI](https://hub.arcgis.com/maps/bc3c97f73d6b4be4921be8560fbc325a) aus 2023. [DOWNLOAD](https://github.com/s92854/Datenmodellierung/files/13966254/LadesA4ulen_in_Deutschland.zip), entpackt ca. 78MB groß.
* Zusätzlich wurden die Highways von OSM verwendet. [DOWNLOAD](https://github.com/s92854/Datenmodellierung/files/13966279/Strassen.Deutschland.zip), entpackt ca. 112MB groß.

&nbsp;

## Operationen/Vorgehensweise
1. Um die Performance der Highways zu verbessern wurden alle Spalten, bis auf *id* und *ref*, gelöscht. Die gelöschten Spalten beinhalteten hauptsächlich *NULL*-Werte, sowie Daten, die für unsere Untersuchungen nicht notwendig sind.
2. Um die Schnellladeeinrichtungen von den normalen zu separieren wurden alle drei Arten ('Normalladeeinrichtung' und 'Schnellladeeinrichtung', welche ab 150kW als 'High-Power-Ladeeinrichtung' gilt) in neue Shapefiles exportiert
3. Für Analysezwecke wurden verschiedene Puffer generiert:

|Puffer|Zweck/Grund|Radius|Anzahl|
|--|--|--|--|
|Puffer um jede Schnellladesäule|Da die durchschnittliche Reichweite eines E-Fahrzeugs ca. 200km beträgt, nehmen wir an, dass man normalerweise bei 10% restlicher Akkuladung eine Ladesäule aufsucht. Wenn nun also alle Ladesäulen bei einem Standort belegt sind, hat man die Ausweichmöglichkeiten, die innerhalb dieses Puffers und dem aktuellen Standort liegen.|20km|2|
|Puffer um Autobahnen|Die Ladesäule soll nicht weit von der Autobahn entfernt sein, um weitere Probleme und Entladung zu umgehen.|2km|1|
|||||
|Vereinter Puffer der Ladesäulen|Zwischenschritt der Analysezwecke|20km|1|
|Differenzpuffer von Ladesäulen und Highways|Um die Teile der Autobahn sichtbar zu machen, die noch über keine Schnellladeeinrichtung verfügen. Mögliche Standpunkte.|2km|1|
