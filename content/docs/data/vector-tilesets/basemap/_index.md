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
           "hillshadeSource": {
            "type": "raster-dem",
            "tiles": [
              "https://tiles.mapx.at/terrain/{z}/{x}/{y}"
            ],
            "tileSize": 512,
            "maxzoom": 15
          },
           "terrainSource": {
            "type": "raster-dem",
            "tiles": [
              "https://tiles.mapx.at/terrain/{z}/{x}/{y}"
            ],
            "tileSize": 512,
            "maxzoom": 15
          }
        },
        "sprite": "https://maputnik.github.io/osm-liberty/sprites/osm-liberty",
        "glyphs": "https://orangemug.github.io/font-glyphs/glyphs/{fontstack}/{range}.pbf",
        "layers": [
          {
            "id": "hillshade",
            "type": "hillshade",
            "source": "hillshadeSource",
            "minzoom": 7,  // Sichtbar ab Zoom-Level 0
            "maxzoom": 19, // Sichtbar bis Zoom-Level 19
            "layout": {},
            "paint": {
              "hillshade-shadow-color": "#aaaaaa",
              "hillshade-highlight-color": "#ffffff"            }
          },
          {
            "id": "landuse-building",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "building"]],
            "paint": {"fill-color": "rgba(237, 202, 202, 0.8)", "fill-antialias": false}
          },
          {
            "id": "landuse-ancillary",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "ancillary"]],
            "paint": {"fill-color": "rgba(242, 242, 240, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-agriculture",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "agriculture"]],
            "paint": {"fill-color": "rgba(235,255,170,0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-crop",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "crop"]],
            "paint": {"fill-color": "rgba(241, 246, 223, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-bush",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "bush"]],
            "paint": {"fill-color": "rgba(201, 228, 186, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-garden",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "garden"]],
            "paint": {
              "fill-color": "rgba(136,204,102,0.4)",
              "fill-antialias": false,
              "fill-translate-anchor": "map"
            }
          },
          {
            "id": "landuse-vineyard",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "vineyard"]],
            "paint": {"fill-color": "rgba(191,191,86,0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-alp",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "alp"]],
            "paint": {"fill-color": "rgba(206, 211, 188, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-forest",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "forest"]],
            "paint": {"fill-color": "rgba(71,179,18,0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-krummholz",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "krummholz"]],
            "paint": {"fill-color": "rgba(157, 189, 138, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-forestroad",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "forestroad"]],
            "paint": {"fill-color": "rgba(248, 248, 245, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-stream",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "stream"]],
            "paint": {"fill-color": "rgba(179, 217, 255, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-lake",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "lake"]],
            "paint": {"fill-color": "rgba(225, 248, 211, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-riparian",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "riparian"]],
            "paint": {"fill-color": "rgba(225, 248, 211, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-wetland",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "wetland"]],
            "paint": {"fill-color": "rgba(163,255,115,0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-road",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "road"]],
            "paint": {"fill-color": "rgba(246, 246, 244, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-rail",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "rail"]],
            "paint": {"fill-color": "rgba(246, 246, 244, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-roadside",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "roadside"]],
            "paint": {"fill-color": "rgba(246, 246, 244, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-parking",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "parking"]],
            "paint": {"fill-color": "rgba(246, 246, 244, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-business",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "business"]],
            "paint": {"fill-color": "rgba(242, 242, 240, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-landfill",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "landfill"]],
            "paint": {"fill-color": "rgba(248, 248, 245, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-recreation",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "recreation"]],
            "paint": {"fill-color": "rgba(102,153,77,0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-cemetery",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "cemetery"]],
            "paint": {"fill-color": "rgba(153,125,77,0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-rock",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "rock"]],
            "paint": {
              "fill-color": "rgba(242, 242, 239, 0.58)",
              "fill-antialias": false
            }
          },
          {
            "id": "landuse-underbrush",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "underbrush"]],
            "paint": {"fill-color": "rgba(238, 238, 235, 0.25)", "fill-antialias": false}
          },
          {
            "id": "landuse-glacier",
            "type": "fill",
            "source": "mapx_basemap",
            "source-layer": "landuse",
            "filter": ["all", ["==", "usage", "glacier"]],
            "paint": {"fill-color": "rgba(115,240,255,0.25)", "fill-antialias": false}
          },
          {
            "id": "waterroute-lines",
            "type": "line",
            "source": "mapx_basemap",
            "source-layer": "waterroute",
            "paint": {"line-color": "rgba(217, 255, 0.25)", "line-width": 2}
          },
          {
            "id": "road-G-halo",
            "type": "line",
            "source": "mapx_basemap",
            "source-layer": "road",
            "minzoom": 14,
            "maxzoom": 20,
            "filter": ["all", ["==", "edgecat", "G"]],
            "layout": {"line-cap": "round"},
            "paint": {
              "line-width": {
                "stops": [[14, 2], [15, 3], [16, 7], [18, 13], [19, 26], [20, 52]],
                "base": 1.4
              },
              "line-color": "rgba(189, 186, 186, 0.25)"
            }
          },
          {
            "id": "road-G",
            "type": "line",
            "source": "mapx_basemap",
            "source-layer": "road",
            "minzoom": 14,
            "maxzoom": 20,
            "filter": ["all", ["==", "edgecat", "G"]],
            "layout": {"line-cap": "round"},
            "paint": {
              "line-width": {
                "stops": [[14, 1], [15, 2], [16, 6], [18, 12], [19, 25], [20, 50]],
                "base": 1.4
              },
              "line-color": "rgba(255, 255, 255, 1)"
            }
          },
          
        ],
       
        "id": "osm-liberty"
      },
              center: [15.16, 48.207], // Startposition: Longitude, Latitude (z. B. Berlin)
              zoom: 14, // Zoom-Level
              attributionControl: false
            });
        // Tooltip-Element erstellen
          const tooltip = document.createElement("div");
          tooltip.style.position = "absolute";
          tooltip.style.padding = "8px";
          tooltip.style.border = "1px solid";
          tooltip.style.borderRadius = "4px";
          tooltip.style.pointerEvents = "none";
          tooltip.style.display = "none";
          tooltip.style.zIndex = "1000";
          document.body.appendChild(tooltip);

          // Funktion zur Anwendung von Dark/Light Mode auf den Tooltip
          function applyTooltipTheme() {
            const isDarkMode = window.matchMedia("(prefers-color-scheme: dark)").matches;
            if (isDarkMode) {
              tooltip.style.backgroundColor = "rgba(0, 0, 0, 0.8)";
              tooltip.style.color = "white";
              tooltip.style.borderColor = "white";
            } else {
              tooltip.style.backgroundColor = "rgba(255, 255, 255, 0.9)";
              tooltip.style.color = "black";
              tooltip.style.borderColor = "black";
            }
          }

          // Tooltip-Styling basierend auf dem initialen Farbmodus anwenden
          applyTooltipTheme();

          // Farbmodusänderung beobachten und Tooltip aktualisieren
          window.matchMedia("(prefers-color-scheme: dark)").addEventListener("change", applyTooltipTheme);

          // Mousemove-Ereignis hinzufügen
          map.on("mousemove", (e) => {
            const features = map.queryRenderedFeatures(e.point);
            if (features.length > 0) {
              const feature = features[0];
              tooltip.style.display = "block";
              tooltip.style.left = `${e.originalEvent.clientX + 10}px`;
              tooltip.style.top = `${e.originalEvent.clientY + 10}px`;

              tooltip.innerHTML = `
                <strong>Layer:</strong> ${feature.layer.id}<br>
                <strong>Attribute:</strong> ${JSON.stringify(feature.properties, null, 2)}
              `;
            } else {
              tooltip.style.display = "none";
            }
          });

          // Mouseleave-Ereignis hinzufügen
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


