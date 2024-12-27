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
        container: 'map', // ID des HTML-Containers
        style: {
          "version": 8,
          "name": "mapx basemap",
          "metadata": {"maputnik:renderer": "mlgljs"},
          "sources": {
            "mapx_basemap": {
              "type": "vector",
              "url": "https://tiles.mapx.at/landuse,waterbody,waterroute"
            }
          },
          "sprite": "https://maputnik.github.io/osm-liberty/sprites/osm-liberty",
          "glyphs": "https://orangemug.github.io/font-glyphs/glyphs/{fontstack}/{range}.pbf",
          "layers": [
            {
              "id": "landuse-building",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "building"]],
              "paint": {"fill-color": "rgb(237, 202, 202)", "fill-antialias": false}
            },
            {
              "id": "landuse-ancillary",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "ancillary"]],
              "paint": {"fill-color": "rgb(242, 242, 240)", "fill-antialias": false}
            },
            {
              "id": "landuse-agriculture",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "agriculture"]],
              "paint": {"fill-color": "rgb(250, 255, 233)", "fill-antialias": false}
            },
            {
              "id": "landuse-crop",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "crop"]],
              "paint": {"fill-color": "rgb(241, 246, 223)", "fill-antialias": false}
            },
            {
              "id": "landuse-bush",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "bush"]],
              "paint": {"fill-color": "rgb(201, 228, 186)", "fill-antialias": false}
            },
            {
              "id": "landuse-garden",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "garden"]],
              "paint": {
                "fill-color": "rgb(208, 234, 194)",
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
              "paint": {"fill-color": "rgb(206, 211, 188)", "fill-antialias": false}
            },
            {
              "id": "landuse-forest",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "forest"]],
              "paint": {"fill-color": "rgb(210, 236, 197)", "fill-antialias": false}
            },
            {
              "id": "landuse-krummholz",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "krummholz"]],
              "paint": {"fill-color": "rgb(157, 189, 138)", "fill-antialias": false}
            },
            {
              "id": "landuse-forestroad",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "forestroad"]],
              "paint": {"fill-color": "rgb(248, 248, 245)", "fill-antialias": false}
            },
            {
              "id": "landuse-stream",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "stream"]],
              "paint": {"fill-color": "rgb(179, 217, 255)", "fill-antialias": false}
            },
            {
              "id": "landuse-lake",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "lake"]],
              "paint": {"fill-color": "rgb(225, 248, 211)", "fill-antialias": false}
            },
            {
              "id": "landuse-riparian",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "riparian"]],
              "paint": {"fill-color": "rgb(225, 248, 211)", "fill-antialias": false}
            },
            {
              "id": "landuse-wetland",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "wetland"]],
              "paint": {"fill-color": "rgb(226, 247, 211)", "fill-antialias": false}
            },
            {
              "id": "landuse-road",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "road"]],
              "paint": {"fill-color": "rgb(246, 246, 244)", "fill-antialias": false}
            },
            {
              "id": "landuse-rail",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "rail"]],
              "paint": {"fill-color": "rgb(246, 246, 244)", "fill-antialias": false}
            },
            {
              "id": "landuse-roadside",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "roadside"]],
              "paint": {"fill-color": "rgb(246, 246, 244)", "fill-antialias": false}
            },
            {
              "id": "landuse-parking",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "parking"]],
              "paint": {"fill-color": "rgb(246, 246, 244)", "fill-antialias": false}
            },
            {
              "id": "landuse-business",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "business"]],
              "paint": {"fill-color": "rgb(242, 242, 240)", "fill-antialias": false}
            },
            {
              "id": "landuse-landfill",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "landfill"]],
              "paint": {"fill-color": "rgb(248, 248, 245)", "fill-antialias": false}
            },
            {
              "id": "landuse-recreation",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "recreation"]],
              "paint": {"fill-color": "rgb(216, 229, 210)", "fill-antialias": false}
            },
            {
              "id": "landuse-cemetery",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "cemetery"]],
              "paint": {"fill-color": "rgb(229, 222, 210)", "fill-antialias": false}
            },
            {
              "id": "landuse-rock",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "rock"]],
              "paint": {"fill-color": "rgb(242, 242, 239)", "fill-antialias": false}
            },
            {
              "id": "landuse-underbrush",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "underbrush"]],
              "paint": {"fill-color": "rgb(238, 238, 235)", "fill-antialias": false}
            },
            {
              "id": "landuse-glacier",
              "type": "fill",
              "source": "mapx_basemap",
              "source-layer": "landuse",
              "filter": ["all", ["==", "usage", "glacier"]],
              "paint": {"fill-color": "rgb(115,240,255)", "fill-antialias": false}
            },
            {
              "id": "waterroute-lines",
              "type": "line",
              "source": "mapx_basemap",
              "source-layer": "waterroute",
              "paint": {"line-color": "rgb(179, 217, 255)", "line-width": 2}
            }
          ],
          "id": "osm-liberty"
        },
        center: [15.16, 48.207], // Startposition: Longitude, Latitude (z. B. Berlin)
        zoom: 14, // Zoom-Level
        attributionControl: false
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

### water



