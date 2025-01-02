---
title: Basemap
type: docs
prev: docs/data/vector-tilesets
sidebar:
  open: true
weight: 2
---


## Overview

<div id="map" style="width: 100%; height: 400px;"></div>

<script src="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.js"></script>
<script>
  document.addEventListener("DOMContentLoaded", function () {
    const map = new maplibregl.Map({
      container: 'map',
      style: {
        "version": 8,
        "name": "mapx basemap",
        "metadata": { "maputnik:renderer": "mlgljs" },
        "sources": {
          "mapx_basemap": {
            "type": "vector",
            "url": "https://tiles.mapx.at/landuse,waterbody,waterroute,road"
          },
           "terrain": {
            "type": "raster-dem",
            "tiles": [
              "https://tiles.mapx.at/terrain/{z}/{x}/{y}"
            ],
            "tileSize": 512
          }
        },
        "sprite": "https://maputnik.github.io/osm-liberty/sprites/osm-liberty",
        "glyphs": "https://orangemug.github.io/font-glyphs/glyphs/{fontstack}/{range}.pbf",
        "layers": [
          {
            "id": "hillshade",
            "type": "hillshade",
            "source": "terrain",
            "layout": {},
            "paint": {
              "hillshade-shadow-color": "#aaaaaa",
              "hillshade-highlight-color": "#ffffff",
              "hillshade-exaggeration": 0.5
            }
          },
          {
            "id": "landuse-building",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "building"]],
            "paint": { "fill-color": "rgb(237, 202, 202)", "fill-antialias": false }
          }
          // Restliche Layer hier unverändert ...
        ]
      },
      center: [15.16, 48.207],
      zoom: 14,
      attributionControl: false
    });

    const tooltip = document.createElement("div");
    tooltip.style.position = "absolute";
    tooltip.style.padding = "8px";
    tooltip.style.border = "1px solid";
    tooltip.style.borderRadius = "4px";
    tooltip.style.pointerEvents = "none";
    tooltip.style.display = "none";
    tooltip.style.zIndex = "1000";
    document.body.appendChild(tooltip);

    function applyTooltipTheme() {
      const isDarkMode = window.matchMedia("(prefers-color-scheme: dark)").matches;
      tooltip.style.backgroundColor = isDarkMode ? "rgba(0, 0, 0, 0.8)" : "rgba(255, 255, 255, 0.9)";
      tooltip.style.color = isDarkMode ? "white" : "black";
      tooltip.style.borderColor = isDarkMode ? "white" : "black";
    }

    applyTooltipTheme();

    window.matchMedia("(prefers-color-scheme: dark)").addEventListener("change", applyTooltipTheme);

    map.on("mousemove", (e) => {
      const features = map.queryRenderedFeatures(e.point);
      if (features.length > 0) {
        const feature = features[0];
        tooltip.style.display = "block";
        tooltip.style.left = `${e.originalEvent.clientX + 10}px`;
        tooltip.style.top = `${e.originalEvent.clientY + 10}px`;
        tooltip.innerHTML = `<strong>Layer:</strong> ${feature.layer.id}<br><strong>Attribute:</strong> ${JSON.stringify(feature.properties, null, 2)}`;
      } else {
        tooltip.style.display = "none";
      }
    });

    map.on("mouseleave", () => {
      tooltip.style.display = "none";
    });
  });
</script>


### Data sources and updates

MapX Basemap vector tiles are based on a combination of datasets from [data.gv.at](https://data.gv.at),  [data.bev.gv.at](https://data.bev.gv.at) and proprietary data crafted by MapX.

| Layer   | Source | Version | License |
| --------  | -------- | -------- | -------- |
| [boundaries](#boundaries) | [BEV - Kataster DXF Stichtagsdaten](https://www.bev.gv.at/Services/Produkte/Kataster-und-Verzeichnisse/Kataster-Stichtagsdaten.html) | 2023-10-01 | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| [buildings](#buildings)   | [BEV - Kataster DXF Stichtagsdaten](https://www.bev.gv.at/Services/Produkte/Kataster-und-Verzeichnisse/Kataster-Stichtagsdaten.html) | 2023-10-01 | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| [housenums](#housenums)   | [BEV - Kataster DXF Stichtagsdaten](https://www.bev.gv.at/Services/Produkte/Kataster-und-Verzeichnisse/Kataster-Stichtagsdaten.html) | 2023-10-01 | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| [landuse](#landuse)       | [BEV - Kataster DXF Stichtagsdaten](https://www.bev.gv.at/Services/Produkte/Kataster-und-Verzeichnisse/Kataster-Stichtagsdaten.html) | 2023-10-01 | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| [streets](#streets)       | [Intermodales Verkehrsreferenzsystem Österreich (GIP.at) Österreich](https://www.data.gv.at/katalog/dataset/3fefc838-791d-4dde-975b-a4131a54e7c5) | 24.2 | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| [water](#water)           | [Gesamtgewässernetz - Fliessgewässer](https://www.data.gv.at/katalog/dataset/c2287ccb-f44c-48cd-bf7c-ac107b771246) <br>[Gesamtgewässernetz - Stehende Gewässer](https://www.data.gv.at/katalog/dataset/ce50ffa6-5032-4771-90a2-1c48d6a0ac85) | v18 | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |

### Data quality
The layers [boundaries](#boundaries), [buildings](#buildings), [landuse](#landuse) and [parcels](#parcels) are derived from the product [BEV - Kataster DXF Stichtagsdaten](https://www.bev.gv.at/Services/Produkte/Kataster-und-Verzeichnisse/Kataster-Stichtagsdaten.html) from [BEV - Bundesamt für Eich- und Vermessungswesen](https://data.bev.gv.at) to ensure maximum accuracy and avoid data preparation errors on data format conversions, especially floating point errors. The data has been reprojected from the local coordinate systems EPSG:31254, EPSG:31255, and EPSG:31256 to the more web-friendly Web Mercator EPSG:3857. Therefore, the view is distorted, and the coordinate accuracy cannot be compared to the original data.


### Attribution
When you publicly use maps that use Mapx vector tiles, you must display proper [attribution](/docs/other/attribution).





## Layer Reference

| Layer   | Min. zoom level | Max. zoom level |
| --------  | -------- | -------- |
| [boundaries](#boundaries) | 0   | 18 | 
| [buildings](#buildings)   | 13  | 18 |
| [housenums](#housenums)   | 16  | 18 |
| [landuse](#landuse)       | 5   | 18 |
| [parcels](#parcels)       | 12  | 18 |
| [streets](#streets)       | 3   | 18 |
| [water](#water)           | 0   | 18 |



### boundaries

All boundaries are dissolved from the parcel polygonsand therfore match on vertex level.git 

| Level | Description | Min. zoom level |
| --------  | -------- | -------- |
| national  |  national border | 0 |
| state  | state border | 10 |
| district  | district border | 10 |
| municipal  | municipal border | 14 |
| cadastral  | cadastral border | 15 |
| parcel  | parcel border | 16 |




### buildings

### housenums

### landuse

| value | description |
| ----- | ----------- |
| building | Gebäude |
| ancillary | Gebäudenebenflächen |
| agriculture | Äcker, Wiesen oder Weiden |
| crop | Dauerkulturanlagen oder Erwerbsgärten |
| bush | Verbuschte Flächen |
| garden | Gärten |
| vineyard | Weingarten |
| alp | Alpen |
| forest | Wälder |
| krummholz | Krummholzflächen |
| forestroad | Forststraßen |
| stream | Fließende Gewässer (Wasserlauf) |
| lake | Stehende Gewässer (Wasserfläche) |
| riparian | Gewässerrandflächen |
| wetland | Feuchtgebiete |
| road | Straßenverkehrsanlagen |
| rail | Schienenverkehrsanlagen |
| roadside | Verkehrsrandflächen |
| parking | Parkplätze |
| business | Betriebsflächen |
| landfill | Abbauflächen, Halden und Deponien |
| recreation | Freizeitflächen |
| cemetery | Friedhöfe |
| rock | Fels- und Geröllflächen |
| underbrush | Vegetationsarme Flächen |
| glacier | Gletscher |

### streets

#### type
| type | description                               |
|------|-------------------------------------------|
| A    | Autobahn                                  |
| AW   | Almweg                                    |
| B    | Landesstraße B                            |
| BA   | Bringungsanlage                           |
| BS   | Bundesstraße Deutschland                  |
| EA   | Eisenbahn Anschlussbahn                   |
| EH   | Eisenbahn hochrangig                      |
| EN   | Eisenbahn Nebenbahn                       |
| ES   | Sonstige Eisenbahn                        |
| EU   | Eisenbahn U-Bahn                          |
| FS   | Forststraße/-weg                          |
| FW   | Fußweg                                    |
| G    | Gemeindestraße                            |
| GS   | Genossenschaftsstraße                     |
| GW   | Güterweg                                  |
| H    | Hauptstraße                               |
| HA   | Hauptstraße A                             |
| HB   | Hauptstraße B                             |
| I    | Interessentenweg                          |
| IO   | Interessentenstraße öffentlich            |
| KR   | Kreisstraße Deutschland                   |
| L    | Landesstraße L                            |
| LS   | Landesstraße Italien                      |
| LD   | Landesstraße Deutschland                  |
| M    | Mountainbikeweg                           |
| MW   | Mountainbike-                             |
| N    | nicht bekannt                             |
| OW   | ÖWG Instandhaltungsweg                    |
| P    | hochrangige Privatstraße                  |
| PO   | Privatstraße mit Öffentlichkeitscharakter |
| PS   | Privatstraße/-weg                         |
| PW   | Privatweg                                 |
| R    | andere Straße                             |
| RW   | Radweg                                    |
| S    | Schnellstraße                             |
| SB   | Seilbahn                                  |
| ST   | Straßenbahntrasse                         |
| SD   | Staatsstraße Deutschland                  |
| SS   | Staatsstraße Italien                      |
| T    | Tourismus                                 |
| TW   | Treppelweg                                |
| U    | Rad bzw. Fußweg                           |
| UR   | überregionaler Radweg                     |
| SW   | stillschweigend gewidmete Straße          |
| VS   | Verbindungsstraße                         |
| VW   | Verbindungsweg                            |
| W    | Weg                                       |
| WA   | Wanderweg                                 |
| WW   | Wirtschaftsweg                            |

#### functional road class

| Nummer | Beschreibung                                           |
|--------|-------------------------------------------------------|
| -1     | Unbekannt                                              |
| 000    | Straßen des transnationalen Netzes                    |
| 001    | Straßen des transregionalen Netzes                    |
| 002    | Straßen des zentralörtlichen Netzes                   |
| 003    | Straßen des regionalen Netzes                         |
| 004    | Gemeindeverbindungen                                  |
| 005    | Straßen des innerörtlichen Netzes                     |
| 006    | Sammelstraßen                                         |
| 007    | Straßen der internen Erschließung                     |
| 008    | Sonstige Straße                                       |
| 010    | Rad-/Fußweg                                           |
| 011    | Wirtschaftsweg                                        |
| 012    | Sonstiger Weg                                         |
| 020    | Bahntrasse Hauptnetz                                  |
| 021    | Bahntrasse Ergänzungsnetz                             |
| 022    | Bahntrasse Anschlussbahn, Verbindungsgleis, sonstiges Gleis |
| 024    | Straßenbahntrasse                                     |
| 025    | U-Bahn-Trasse                                         |
| 031    | Fähre                                                 |
| 045    | Treppe                                                |
| 046    | Rolltreppe                                            |
| 047    | Aufzug                                                |
| 048    | Rampe für den nichtmotorisierten Verkehr              |
| 098    | Betriebsumkehr                                        |
| 099    | Betriebsweg                                           |
| 101    | Fußweg ohne Anzeige                                   |
| 102    | Fußwegpassage                                         |
| 103    | Seilbahn und Sonstige                                 |
| 105    | Almaufschließungsweg                                  |
| 106    | Forstaufschließungsweg                                |
| 107    | Gebäudezufahrt                                        |
| 115    | Friedhofsweg                                          |
| 200    | Singletrail (MTB)                                     |
| 201    | Shared Trail                                          |
| 300    | Wanderweg                                             |

#### form of way

| Nummer | Beschreibung                                      |
|--------|--------------------------------------------------|
| -1     | Unbekannt                                        |
| 001    | Autobahn                                         |
| 002    | Fahrbahnteilung (keine Autobahn)                 |
| 003    | Ungeteilte Fahrbahn                              |
| 004    | Kreisverkehr                                     |
| 006    | Parkplatz                                        |
| 007    | Parkgarage                                       |
| 008    | Unstrukturierte Kreuzung                        |
| 010    | Ab-/Einbiegefahrbahn                             |
| 011    | Servicestraße-Fahrbahn/Pannenstreifen            |
| 012    | Ausfahrt/Einfahrt von/zu einem Parkplatz         |
| 013    | Straße (teilweise) im Objekt                    |
| 014    | Fußgängerzone                                   |
| 015    | Fußweg                                          |
| 016    | Fußweg (teilweise) im Objekt                    |
| 017    | Spezielle Fahrbahnführung                       |
| 018    | Stiege                                          |
| 019    | Furt                                            |
| 020    | Straße für Berechtigte/Behörden                 |
| 021    | Stiege (teilweise) im Objekt                    |
| 022    | Rolltreppe                                      |
| 023    | Rolltreppe (teilweise) im Objekt                |
| 024    | Aufzug                                          |
| 025    | Aufzug (teilweise) im Objekt                    |
| 026    | Rampe NMIV (teilweise) im Objekt                |
| 101    | Straßenbahn                                     |
| 102    | U-Bahn                                          |
| 103    | Bahn                                            |
| 200    | Singletrail-Strecke (MTB)                       |
| 220    | MTB Strecke                                     |
| 301    | Betriebsumkehr                                  |
| 400    | Traktorweg                                      |
| 401    | Steig                                           |
| 402    | Steigspuren                                     |
| 403    | Klettersteig                                    |
| 404    | Alpine Route                                    |
| 405    | Gletscherroute                                  |
| 406    | Schluchtweg                                     |
| 504    | Geh- und Radweg                                 |
| 505    | Radweg                                          |
| 506    | Normalspurbahn mehrgleisig                      |
| 507    | Normalspurbahn eingleisig                       |
| 508    | Schmalspurbahn                                  |
| 509    | Zahnradbahn                                     |
| 510    | Breitspurbahn                                   |
| 511    | Seilschwebebahn                                 |
| 512    | Standseilbahn                                   |
| 513    | Magnetschwebebahn                               |
| 514    | Monorail                                        |
| 515    | Schwebebahn                                     |
| 516    | Schlepplift                                     |
| 517    | Materialseilbahn                                |
| 518    | Kombilift                                       |
| 519    | Sessellift                                      |
| 520    | Babylift                                        |
| 521    | Umlaufbahn                                      |
| 522    | Zweiseilpendelbahn                              |
| 523    | Schrägaufzug                                    |
| 524    | Pendelbahn                                      |
| 525    | Sesselbahn                                      |
| 526    | Kabinenbahn                                     |
| 527    | Kombibahn                                       |
| 528    | Korblift                                        |
| 599    | Sonstige                                        |
| 601    | Wasserweg / Fähre                               |
| 701    | Rampe für nichtmotorisierten Verkehr            |
| 702    | Einschließlichstrecke                           |

### water



