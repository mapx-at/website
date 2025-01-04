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

  .map-tooltip {
    position: absolute;
    background-color: rgba(255, 255, 255, 0.9);
    color: black;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 8px;
    pointer-events: none;
    display: none;
    font-size: 12px;
    z-index: 1000;
  }

  .hillshade-controls {
    position: absolute;
    top: 10px;
    left: 10px;
    background-color: white;
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 10px;
    font-size: 14px;
    z-index: 1000;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
  }

  .hillshade-controls label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
  }

  .hillshade-controls input[type="range"] {
    width: 100%;
    margin-bottom: 10px;
  }
</style>

<div id="map" style="width: 100%; height: 100%;"></div>
<div class="hillshade-controls">
  <label for="azimuthRange">Beleuchtungsrichtung (Azimuth):</label>
  <input type="range" id="azimuthRange" min="0" max="360" value="315">
  <label for="altitudeRange">Beleuchtungshöhe (Altitude):</label>
  <input type="range" id="altitudeRange" min="0" max="90" value="45">
  <label for="exaggerationRange">Höhenexaggeration:</label>
  <input type="range" id="exaggerationRange" min="1" max="5" step="0.1" value="1">
</div>

<script src="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.js"></script>
<script>
  document.addEventListener("DOMContentLoaded", async function () {
    const response = await fetch('/map_showcase_style.json');
    if (!response.ok) {
      throw new Error('Error loading style: ' + response.statusText);
    }
    const style = await response.json();

    // URL-Parameter auslesen
    const params = new URLSearchParams(window.location.search);
    const centerParam = params.get('center'); // Format: "15.16,48.207"
    const zoomParam = params.get('zoom'); // Format: Zahl

    // Default-Werte
    let center = [15.16, 48.207]; // Standard-Kartenmittelpunkt
    let zoom = 14; // Standard-Zoomlevel

    // Falls Parameter vorhanden sind, Werte setzen
    if (centerParam) {
      const coords = centerParam.split(',').map(Number);
      if (coords.length === 2 && !isNaN(coords[0]) && !isNaN(coords[1])) {
        center = coords;
      }
    }
    if (zoomParam && !isNaN(Number(zoomParam))) {
      zoom = Number(zoomParam);
    }

    // MapLibre-Karte erstellen
    const map = new maplibregl.Map({
      container: 'map',
      style: style,
      center: center, // Kartenmittelpunkt aus URL oder Standard
      zoom: zoom, // Zoom-Level aus URL oder Standard
      attributionControl: false
    });

  
    // Hillshade-Parameter mit Schiebereglern steuern
    const azimuthRange = document.getElementById("azimuthRange");
    const altitudeRange = document.getElementById("altitudeRange");
    const exaggerationRange = document.getElementById("exaggerationRange");

    azimuthRange.addEventListener("input", () => {
      map.setPaintProperty("hillshade", "hillshade-illumination-direction", Number(azimuthRange.value));
    });

    altitudeRange.addEventListener("input", () => {
      map.setPaintProperty("hillshade", "hillshade-illumination-altitude", Number(altitudeRange.value));
    });


    // GeolocateControl hinzufügen
    const geolocateControl = new maplibregl.GeolocateControl({
      positionOptions: {
        enableHighAccuracy: true // Höchste Genauigkeit aktivieren
      },
      trackUserLocation: true, // Nutzereigene Position verfolgen
      showUserHeading: true // Richtung des Nutzers anzeigen (falls verfügbar)
    });
    map.addControl(geolocateControl, 'bottom-right');

    // Funktion zum Aktualisieren der URL-Parameter
    const updateURL = () => {
      const currentCenter = map.getCenter(); // Aktuelle Karte Mitte
      const currentZoom = map.getZoom().toFixed(2); // Aktuelles Zoom-Level
      const newParams = new URLSearchParams({
        center: `${currentCenter.lng.toFixed(5)},${currentCenter.lat.toFixed(5)}`,
        zoom: currentZoom,
      });
      window.history.replaceState({}, '', `?${newParams.toString()}`);
    };

    // URL bei Kartenbewegung aktualisieren
    map.on('moveend', updateURL);

    // Navigation Controls (Zoom + Kompass)
    const navControl = new maplibregl.NavigationControl({
      showCompass: true,
      showZoom: true,
      visualizePitch: true // Zeigt Pitch visuell an
    });
    map.addControl(navControl, 'bottom-right');

    // Maßstabsleiste hinzufügen
    const scaleControl = new maplibregl.ScaleControl({
      maxWidth: 200,
      unit: 'metric' // Einheiten: metrisch
    });
    map.addControl(scaleControl, 'bottom-left');

    // Tooltip-Element hinzufügen
    const tooltip = document.createElement('div');
    tooltip.className = 'map-tooltip';
    document.body.appendChild(tooltip);

    // Mousemove-Ereignis hinzufügen
    map.on('mousemove', (e) => {
      const features = map.queryRenderedFeatures(e.point);
      if (features.length > 0) {
        const feature = features[0];

        // Tooltip anzeigen
        tooltip.style.display = 'block';
        tooltip.style.left = `${e.originalEvent.clientX + 10}px`;
        tooltip.style.top = `${e.originalEvent.clientY + 10}px`;

        // Tooltip-Inhalt setzen
        const properties = feature.properties;
        let content = `<strong>Layer:</strong> ${feature.layer.id}<br>`;
        content += '<br><ul>';

        for (const [key, value] of Object.entries(properties)) {
          content += `<li><strong>${key}:</strong> ${value}</li>`;
        }
        content += '</ul>';

        tooltip.innerHTML = content;
      } else {
        tooltip.style.display = 'none';
      }
    });

    // Mouseleave-Ereignis hinzufügen
    map.on('mouseleave', () => {
      tooltip.style.display = 'none';
    });
  });
</script>
