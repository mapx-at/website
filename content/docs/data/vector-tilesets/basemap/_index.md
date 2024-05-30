---
title: Basemap
type: docs
prev: docs/data/vector-tilesets
sidebar:
  open: true
weight: 2
---


## Overview

Overview text

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



