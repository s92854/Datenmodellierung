# Abschlussprojekt: E-Ladesäulen in Deutschland und ihre Anbindung an das Verkehrsnetz
Auswirkungen anthropologischen Bauens - Windräder

### Nico Haupt (956450), Tara Richter (934172) und Alexander Radünz ()

How-To-Buffer
https://www.geographyrealm.com/buffers-in-gis/

Idee: Buffer um Windräder mit dem gesetzlichen Mindestabstand wo nicht gebaut werden darf und dann "verlorenen Space" analysieren. &rarr;	
https://www.govdata.de/web/guest/daten/-/details/rhein-kreis-neuss-windenergieanlagen

&nbsp;

&nbsp;

## Datengrundlange
* Die Daten der Ladesäulen basieren auf den Daten von [ESRI](https://hub.arcgis.com/maps/bc3c97f73d6b4be4921be8560fbc325a) aus 2020. [DOWNLOAD](https://github.com/s92854/Datenmodellierung/files/13966254/LadesA4ulen_in_Deutschland.zip), entpackt ca. 78MB groß.
* Zusätzlich wurden die Highways von OSM verwendet. [DOWNLOAD](https://github.com/s92854/Datenmodellierung/files/13966279/Strassen.Deutschland.zip), entpackt ca. 112MB groß.

## Operationen
1. Um die Performance der Straßen zu verbessern wurden mittels einer **Vereinigung** alle exportierten Highways zu einer Linie zusammengefasst
2. Um die Schnellladeeinrichtungen von den normalen zu separieren wurden beide in neue Shapefiles exportiert
