# CityTank ⛽ · Berlin Fuel Prices

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![OpenLayers](https://img.shields.io/badge/OpenLayers-8.2.0-blue)](https://openlayers.org/)
[![Chart.js](https://img.shields.io/badge/Chart.js-4.4.0-orange)](https://www.chartjs.org/)

**CityTank** is a professional, real-time web geovisor that displays fuel prices at gas stations in Berlin, Germany. It combines live data from the [Tankerkönig API](https://www.tankerkoenig.de/) with an intuitive, mobile-responsive interface inspired by modern map applications.

Explore current prices, compare stations, view historical trends, and get directions – all in one tool.

🔗 **Live Demo:** [https://geo-way.github.io/CityTank](https://geo-way.github.io/CityTank) *(Demo)*

---

## ✨ Features

*   **🗺️ Interactive Map**: Built with OpenLayers, centered on Berlin with three base map styles:
    *   `Gray`: A clean, grayscale OSM layer (default).
    *   `Street`: Standard OpenStreetMap.
    *   `Satellite`: High-resolution ESRI satellite imagery.
*   **⛽ Real-time Fuel Prices**: Fetches live data from the Tankerkönig API for a 5km radius. Prices are updated every 5 minutes.
*   **🎨 Smart Color Coding**: Station markers are colored from **green (cheaper)** to **red (more expensive)** based on the selected fuel type (Diesel, E5, E10).
*   **💰 Price Labels**: Each marker displays the current price of the selected fuel.
*   **🏆 Cheapest Station Highlight**: The most affordable station in the area is marked with a **spinning gold ring**.
*   **📍 Zone Statistics**: The bottom sheet shows the **average, minimum, and maximum prices** for the current fuel type in the visible zone.
*   **📈 Historical Trend Chart**: A small, elegant line chart displays the average fuel price trend in Germany over the last 30 days (static demo data).
*   **🌍 Global Context**: Displays the current **Brent Crude Oil price** (USD/BBL) with daily change, sourced from Trading Economics.
*   **📍 User Geolocation**: Click "My location" to center the map on your position. Your location is marked with a **pulsing blue dot** and a subtle red buffer zone.
*   **🔍 City Search**: A dropdown menu of major German cities (sorted alphabetically) for quick navigation.
*   **🗺️ Animated Routes**: Click "Show route on map" in a station's popup to see an animated route (red line with a moving dot) from your location (or map center) to the station, calculated using the OSRM service.
*   **🧭 Google Maps Integration**: The popup also offers a "Navigate" button that opens Google Maps with directions to the station.
*   **📱 Responsive Bottom Sheet**: All controls are housed in a draggable bottom sheet (like Google Maps) that works smoothly on both desktop and mobile.

---

## 🏗️ Architecture & Tech Stack

CityTank is a purely client-side single-page application (SPA). It requires no backend server, making it easy to host on platforms like GitHub Pages.

┌─────────────────────────────────────────────────────────────┐
│ Client Browser │
│ ┌───────────────────────────────────────────────────────┐ │
│ │ HTML/CSS (UI) │ │
│ └───────────────────────────────────────────────────────┘ │
│ │ │
│ ┌───────────────────────────────────────────────────────┐ │
│ │ JavaScript (Core) │ │
│ │ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ │ │
│ │ │ OpenLayers │ │ Chart.js │ │ Fetch API │ │ │
│ │ │ (Map) │ │ (Graph) │ │ (HTTP Calls)│ │ │
│ │ └─────────────┘ └─────────────┘ └─────────────┘ │ │
│ └───────────────────────────────────────────────────────┘ │
│ │ │
└───────────────────────────┼──────────────────────────────────┘
│
┌───────────────────────┼───────────────────────────────────┐
│ ↓ │
│ ╔═════════════════════════════════════════════════════╗ │
│ ║ External APIs & Data ║ │
│ ╠═════════════════════════════════════════════════════╣ │
│ ║ 🔵 Tankerkönig API (live station prices) ║ │
│ ║ 🟢 OSRM (Open Source Routing Machine) ║ │
│ ║ 🟠 Nominatim (OpenStreetMap geocoding) ║ │
│ ║ 📊 Trading Economics (Brent oil price) ║ │
│ ║ 📈 Static historical data (demo) ║ │
│ ╚═════════════════════════════════════════════════════╝ │
└───────────────────────────────────────────────────────────┘


### 🛠️ Core Technologies
*   **OpenLayers (v8.2.0)**: For all map rendering, layers, markers, popups, and interactions.
*   **Chart.js (v4.4.0)**: For the lightweight historical price chart.
*   **Font Awesome (v6)**: For icons and visual enhancements.
*   **Vanilla JavaScript (ES6)**: The entire application logic is written in plain JavaScript, no frameworks, ensuring maximum performance and compatibility.

### 🔌 Data Sources & APIs

1.  **Tankerkönig API** (`creativecommons.tankerkoenig.de`)
    *   **Purpose**: Provides real-time fuel prices for German gas stations.
    *   **License**: [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). **Attribution is required** (provided in the UI footer).
    *   **Usage**: Fetches stations within a 5km radius of the map center.
2.  **OSRM (Project OSRM)** (`router.project-osrm.org`)
    *   **Purpose**: Calculates driving routes between two points for the animated route feature.
    *   **License**: [BSD 2-Clause License](https://github.com/Project-OSRM/osrm-backend/blob/master/LICENSE.md). Free to use with reasonable limits.
3.  **Nominatim (OpenStreetMap)** (`nominatim.openstreetmap.org`)
    *   **Purpose**: Geocodes city names (e.g., "Berlin") to geographic coordinates (latitude, longitude).
    *   **License**: [Open Data Commons Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/). Requires attribution to OpenStreetMap.
    *   **Usage**: Used for the city search dropdown.
4.  **Trading Economics** (via a static embed / callout in this version)
    *   **Purpose**: Displays the current Brent Crude Oil price and daily change.
    *   **Data**: In this demo, the price is fetched from their public API (or a static representative value can be used). Check their website for terms of use for production.
5.  **Historical Price Data**
    *   **Purpose**: To show a 30-day trend for the average fuel price in Germany.
    *   **Source**: Currently uses a static array of demo data for illustration. In a production app, this could be replaced with a call to a historical data API or a custom backend.

---

## 🚀 Getting Started

Follow these instructions to get a copy of the project up and running on your local machine for development and testing purposes.

### 📋 Prerequisites
*   A modern web browser (Chrome, Firefox, Edge, Safari).
*   A code editor (like VS Code).
*   A free API key from **Tankerkönig**. You can register for one [here](https://creativecommons.tankerkoenig.de/).

🎮 How to Use
Explore the Map: Pan and zoom to navigate around Berlin.

Select Fuel Type: Use the "FUEL TYPE" buttons to switch between Diesel, E5, and E10. Marker colors and labels will update instantly.

View Station Details: Click on any station marker to open a popup with its address, all prices, and action buttons.

Get Directions: In the popup, click "Navigate (Google Maps)" to open Google Maps for step-by-step directions. Click "Show route on map" to see an animated route drawn on the CityTank map.

Find Your Location: Click the "My location" button. Grant permission when prompted. The map will center on you, and a pulsing blue dot with a red buffer will appear.

Search for a City: Use the dropdown menu under "SEARCH CITY" to jump to major German cities.

Change Base Map: Use the "BASE MAP" selector to switch between Gray, Street, and Satellite views.

Analyze Prices: The "ZONE STATS" section shows the average, minimum, and maximum prices for the current fuel type. The small chart shows a 30-day historical trend.

📄 License & Attribution
CityTank Project Code: Licensed under the MIT License. You are free to use, modify, and distribute this code.

Tankerkönig Data: The real-time fuel price data is provided by Tankerkönig under the Creative Commons Attribution 4.0 International (CC BY 4.0) license. A clear attribution with a link to their website is provided in the application's footer.

OpenStreetMap Data: Map data used in the "Street" and "Gray" base layers is © OpenStreetMap contributors. Geocoding is provided by Nominatim, which also requires OSM attribution.

ESRI Satellite Imagery: Used under fair-use for demonstration; please refer to ESRI's terms for production use.

Chart Data: The historical price data shown in the chart is for demonstration purposes only.

🙏 Acknowledgements
Tankerkönig for providing the invaluable and free fuel price API.

The OpenLayers and Chart.js teams for their excellent open-source libraries.

OSRM for the powerful routing engine.

OpenStreetMap and its community for the foundational map data.

Trading Economics for commodity price data.
