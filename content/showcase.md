---
title: Showcase
toc: false
layout: wide
---

<link href="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.css" rel="stylesheet" />


<style>
    .content {
      width: 100%;
      height: calc(100vh - 20vh); /* 100% viewport height minus 20px */
    }
</style>

<div id="map" style="width: 100%; height: 100%;"></div>

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