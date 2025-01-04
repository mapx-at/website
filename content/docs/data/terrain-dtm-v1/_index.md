---
title: Terrain-DTM v1
type: docs
prev: docs/data
sidebar:
  open: true
weight: 1
---

Das **MapX Terrain-DTM v1 Tileset** ist eine digitale Darstellung der Erdoberfläche, die ausschließlich die natürlichen Geländestrukturen ohne Vegetation, Gebäude oder andere Objekte zeigt.  

Die Höhenwerte werden in den Rot-, Grün- und Blau-Kanälen kodiert:  
- **Kachelgröße** - 512x512 Pixel  
- **Kachelformat** - WebP  
- **vertikale Auflösung** - 1 Dezimeter  
- **horizontale Auflösung** - max. Zoomstufe 15 (~2,39 Meter pro Pixel)  


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
           "hillshadeSource": {
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
            "minzoom": 7,  
            "maxzoom": 19,
            "layout": {},
            "paint": {
              "hillshade-shadow-color": "#aaaaaa",
              "hillshade-highlight-color": "#ffffff"            }
          }         
        ],
        "id": "mapx-hillshade"
      },
      center: [15.16, 48.207], 
      zoom: 14, // Zoom-Level
      attributionControl: false
    })};
</script>


## **Anwendungen**

- **Styling von Geländeneigungen und Hillshades:** Erstelle beeindruckende Kartenvisualisierungen.  
- **Erstellung von 3D-Geländemodellen:** Nutze die präzisen Höhendaten, um realistische 3D-Darstellungen zu erstellen.  
- **Topografische Analysen:** Identifiziere Geländemuster und Höhenveränderungen mit hoher Genauigkeit.  


## **Datenquellen und Updates**

Die Geländedaten im Tileset basieren auf hochwertigen österreichischen Höhendatenquellen und werden regelmäßig aktualisiert, sobald neue oder verbesserte Daten verfügbar sind.  


## **Dekodierung von Höhendaten**

Die Höhe eines Pixels kann mit der folgenden Gleichung berechnet werden:  

```math
height = -10000 + ((R * 256 * 256 + G * 256 + B) * 0.1)
```