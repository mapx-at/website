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

   .hillshade-overlay {
    position: absolute;
    top: 10px;
    right: 10px;
    background-color: rgba(255, 255, 255, 0.9);
    border-radius: 8px;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    padding: 15px;
    z-index: 1000;
    font-size: 14px;
    max-width: 300px;
  }

  .hillshade-overlay label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
  }

  .hillshade-overlay input[type="range"],
  .hillshade-overlay input[type="color"] {
    width: 100%;
    margin-bottom: 15px;
  }

</style>

<div id="map" style="width: 100%; height: 100%; position: relative;">
  <div class="hillshade-overlay">
    <label for="highlightColor">Highlight-Farbe:</label>
    <input type="color" id="highlightColor" value="#ffffff">
    <label for="shadowColor">Schatten-Farbe:</label>
    <input type="color" id="shadowColor" value="#555555">
    <label for="opacityRange">Transparenz:</label>
    <input type="range" id="opacityRange" min="0" max="1" step="0.1" value="1">
    <label for="azimuthRange">Azimuth (Beleuchtungsrichtung):</label>
    <input type="range" id="azimuthRange" min="0" max="360" step="1" value="315">
    <label for="altitudeRange">Altitude (Beleuchtungshöhe):</label>
    <input type="range" id="altitudeRange" min="0" max="90" step="1" value="45">
  </div>
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

  
    // Hillshade-Funktionen
  document.getElementById('highlightColor').addEventListener('input', (e) => {
    map.setPaintProperty('hillshade', 'hillshade-highlight-color', e.target.value);
  });

  document.getElementById('shadowColor').addEventListener('input', (e) => {
    map.setPaintProperty('hillshade', 'hillshade-shadow-color', e.target.value);
  });

  document.getElementById('opacityRange').addEventListener('input', (e) => {
    map.setPaintProperty('hillshade', 'hillshade-opacity', parseFloat(e.target.value));
  });

  document.getElementById('azimuthRange').addEventListener('input', (e) => {
    map.setPaintProperty('hillshade', 'hillshade-illumination-direction', parseInt(e.target.value));
  });

  document.getElementById('altitudeRange').addEventListener('input', (e) => {
    map.setPaintProperty('hillshade', 'hillshade-illumination-altitude', parseInt(e.target.value));
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
