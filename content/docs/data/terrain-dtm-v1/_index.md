---
title: Terrain-DTM v1
type: docs
prev: docs/data
sidebar:
  open: true
weight: 1
---


URL für den Zugriff: 
```
https://tiles.mapx.at/terrain-dtm-v1/{z}/{x}/{y}
```

Beispiel:
```
https://tiles.mapx.at/terrain-dtm-v1/14/8881/5681
```

## **Übersicht**


Das **MapX Terrain-DTM v1 Tileset** ist eine digitale Darstellung der Erdoberfläche, die ausschließlich die natürlichen Geländestrukturen ohne Vegetation, Gebäude oder andere Objekte zeigt.  


<br/>
<link href="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.css" rel="stylesheet">

<div id="map" style="width: 100%; height: 400px;"></div>

<script src="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.js"></script>
<script>
  document.addEventListener("DOMContentLoaded", function () {
    const map = new maplibregl.Map({
      container: 'map',
      style: {
        "version": 8,
        "name": "mapx basemap",
        "sources": {
          "hillshadeSource": {
            "type": "raster-dem",
            "tiles": [
              "https://tiles.mapx.at/terrain-dtm-v1/{z}/{x}/{y}"
            ],
            "tileSize": 512,
            "minzoom": 6,
            "maxzoom": 16
          }
        },
        "sprite": "https://maputnik.github.io/osm-liberty/sprites/osm-liberty",
        "glyphs": "https://orangemug.github.io/font-glyphs/glyphs/{fontstack}/{range}.pbf",
        "layers": [
          {
            "id": "hillshade",
            "type": "hillshade",
            "source": "hillshadeSource",
            "minzoom": 6,
            "maxzoom": 16,
            "layout": {},
            "paint": {
              "hillshade-shadow-color": "#aaaaaa",
              "hillshade-highlight-color": "#ffffff"
            }
          }
        ],
        "id": "mapx-hillshade"
      },
      center: [15.16, 48.207],
      zoom: 14,
      attributionControl: false,
      minZoom: 6,
      maxZoom: 16
    });

    map.addControl(
      new maplibregl.AttributionControl({
        customAttribution: '<a href="https://data.bev.gv.at" target="_blank">Datenquelle: ©BEV data.bev.gv.at</a>'
      })
    );

    
    map.addControl(new maplibregl.FullscreenControl());
  });
</script>


<br/>

Die Kodierung der Höhenwerte erfolgt in den Rot-, Grün- und Blau-Kanälen eines 32-bit WebP Bildes mit Transparenz:  
- **Kachelgröße:** 512x512 Pixel  
- **Kachelformat:** WebP  
- **vertikale Auflösung:** 1 Dezimeter  
- **horizontale Auflösung:**

| **Zoomstufe** | **Meter pro Pixel** |
|------------|-------------------------------|
| 6          | ca. 834.08 m                 |
| 7          | ca. 417.04 m                 |
| 8          | ca. 208.52 m                 |
| 9          | ca. 104.26 m                 |
| 10         | ca. 52.13 m                  |
| 11         | ca. 26.06 m                  |
| 12         | ca. 13.03 m                  |
| 13         | ca. 6.52 m                   |
| 14         | ca. 3.26 m                   |
| 15         | ca. 1.63 m                   |
| 16         | ca. 0.82 m                   |




## **Anwendungen**

- **Styling von Geländeneigungen und Hillshades:** Erstelle beeindruckende Kartenvisualisierungen.  
- **Erstellung von 3D-Geländemodellen:** Nutze die präzisen Höhendaten, um realistische 3D-Darstellungen zu erstellen.  
- **Topografische Analysen:** Identifiziere Geländemuster und Höhenveränderungen mit hoher Genauigkeit.  


## **Datenquellen und Updates**

Die Geländedaten im Tileset basieren auf den Daten der [Serie ALS DTM Höhenraster 1m Stichtag 15.09.2023](https://data.bev.gv.at/geonetwork/srv/api/records/5b510b4a-f592-4c02-991f-012cb1a65ea9) des [Bundesamt für Eich- und Vermessungswesen](https://www.bev.gv.at/).  


## **Dekodierung von Höhendaten**

Die Höhe eines Pixels kann mit der folgenden Gleichung berechnet werden:  

```math
height = -10000 + ((R * 256 * 256 + G * 256 + B) * 0.1)
```