# datenhack-sozarchiv
Datenhack-Projekt Schweizerisches Sozialarchiv

~~Auf einem Flyer sucht das Schweizerische Sozialarchiv den "besten Hack seiner freien Daten".
Solche "Hacks" können bis zum 31. Mai 2018 eingereicht
werden, der beste Beitrag wird prämiert.~~

## Der Plan (Stand 1. Februar)

### Die Daten

- [Bildarchiv des Schweizerischen Arbeiterhilfswerks (SAH)](https://data.stadt-zuerich.ch/dataset/sozialarchiv-sah)

Vorhandene Metadaten (Stand 28.2.2018):

Lizenz der Metadaten: CC0

CSV:

- **Signatur**: Eindeutige Signatur des Fotos (Typ: CHAR)
- **Titel**: Titel und Beschreibung des Fotos (Typ: CHAR)
- **Zeit**: Zeitangabe, wann das Foto entstanden ist. Das Attribut beinhaltet verschiedene Zeitgruppierungen. Z.B. «Neuzeit;20.Jh;1901-1950;1941-1950; 1944». (Typ: CHAR)
- **Ort**: Ortsangabe, wo das Foto geschossen wurde. Das Attribut beinhaltet verschiedene räumliche Gruppierungen: «Kontinent;Land;Region;Ort». Z.B. «Europa;Frankreich;Rhône-Alpes;Lyon». (Typ: CHAR)
- Die Zeit-, Ort- und Schlagwortdaten sind jeweils absteigend von sehr allgemein zu sehr konkret aufgelistet.


JSON:


- **Signatur**: Eindeutige Signatur des Fotos (Typ: string)
- **Objekttraeger**: "Papierabzug", "anderes 3-D Objekt", "Druck A4 und kleiner", "Druck grösser als A4, Plakat", "Ansteckobjekt" (Typ: string)
- **Titel**: Titel und Beschreibung des Fotos (Typ: string)
- **Detailinformation**: zusätzliche Infos zu Bildinhalt, Entstehungskontext, ... (Typ: string)
- **Start**, **Ende**: Zeitangabe, wann das Foto entstanden ist. Werte beinhalten das letzte Glied der Kette im Feld **Zeit** (vgl. CSV, bzw. https://www.bild-video-ton.ch/). Z.B. «Neuzeit;20.Jh;1901-1950;1941-1950;1944» -> "Start" : "1944", "Ende" : "1944"; oder «Neuzeit;20.Jh;1901-1950;1950-1960» -> "Start" : "1950", "Ende" : "1960". (Typ: INT)
- **Ort**: Ortsangabe, wo das Foto geschossen wurde. Das Attribut beinhaltet verschiedene räumliche Gruppierungen: «Kontinent;Land;Region;Ort». Z.B. «Europa;Frankreich;Rhône-Alpes;Lyon». (Typ: string)
- **Serientitel**: z.B. «Ordner A: "Lyon 1944"», bildet Archivstruktur ab (Typ: string)
- **Schlagwoerter**: intellektuelle Beschlagwortung, verwendet [Helvetosaurus](https://bartoc.org/en/node/675), eine einsprachige, helvetisierte Version von [EUROVOC](https://bartoc.org/en/node/15); der Thesaurus wird seit kurzem nicht mehr gepflegt; eine el. Kopie beim SozArch erhältlich. (Typ: string)
- **Personen**: dargestellte Personen, tlw. mit Lebensdaten (Typ: string)
- **Urheber**: Personen, Körperschaften, tlw. mit Ortsangabe (Typ: string)

- Die Ort- und Schlagwortdaten sind jeweils absteigend von sehr allgemein zu sehr konkret aufgelistet.

### Use Cases

Wir fangen mit einer minimalen Standard-Applikation an, mit der man sich Bilder und dazugehörige Metadaten anschauen und sie sortieren kann. Je nachdem, was unsere Daten-Gruppe zu den Daten anreichert, implementieren wir dafür zunächst basale Sortier- und Filterfunktionen. Bei der Arbeit an an diesem Standard-Minimal-Ansatz sammeln wir weitere Ideen, was man noch "Cooles" mit den Bildern und Daten sowie mit den uns interessierenden Technologien und Tools machen könnte.

Entsprechend starten wir mit folgenden User Stories:

Als Archivnutzer_in möchte ich...

- ... ein Bild und die zugehörigen Metadaten in einer Ansicht anschauen.
- ... alle Bilder durchsehen, um mir einen Überblick zu verschaffen.
- ... Bilder verschieden sortieren oder filtern, um mich im grossen Bestand orientieren zu können.

### Technologien, Tools

Datenanalyse und -anreicherung, Backend:
- openrefine
- Geodatenanreicherung
- ElasticSearch Index, der auch JSON-LD ausliefern kann
- zunächst kein RDF-Fokus, kein Triplestore, scheint fürs erste zu überdimensioniert

Bilder:
- IIIF Out-of-the-box-Lösungen ausprobieren

Frontend:
- Angular 2
- OpenSeadragon als IIIF-Bild-Viewer
- abzuklären: Wären die Grundmodule des http://ub-afrikaportal.ub.unibas.ch/ für uns weiter nutzbar? Werden sie früh genug veröffentlicht?

API (grosses Experimentier-Interesse):
- aufgepeppte relationale DB als Data Provider, dann kann man zwischen verschiedenen Backends hin- und her-wechseln.
- [Hydra](http://www.hydra-cg.com/): Versuch einer Standardisierung von REST-Kommunikation, REST-Server teilt dem Client mit, wie man mit ihm kommuniziert, dadurch muss man den Client nicht extra serverspezifisch bauen. Ist inzwischen vom W3C anerkannt.

Weitere Ideen und Details zum Plan finden sich im Wiki.
