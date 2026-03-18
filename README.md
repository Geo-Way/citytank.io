<div align="center">

<img src="img/Logo5.png" alt="GeoWay Logo" width="110"/>

# CityTank ⛽
### Real-Time Fuel Price Geospatial Web Application · Germany

[![Live Demo](https://img.shields.io/badge/🌐_Live_Demo-geo--way.github.io-38bdf8?style=for-the-badge)](https://geo-way.github.io/citytank.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-fbbf24?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![OpenLayers](https://img.shields.io/badge/OpenLayers-8.2.0-10b981?style=for-the-badge)](https://openlayers.org/)
[![Chart.js](https://img.shields.io/badge/Chart.js-4.4.0-ef4444?style=for-the-badge)](https://www.chartjs.org/)
[![Made by GeoWay](https://img.shields.io/badge/Made_by-GeoWay-818cf8?style=for-the-badge)](https://geo-way.github.io/GeoWay.io/)

*A production-grade, client-side geospatial web app combining real-time API data, spatial analytics, and modern cartographic UX — built entirely without backend infrastructure.*

</div>

---

## 📌 Project Context

This project was conceived and developed independently as part of my open geospatial portfolio. It demonstrates applied skills in **web cartography, spatial data integration, real-time API orchestration, and mobile-first UX design** — all relevant to GIS Developer, Geospatial Analyst, and WebGIS Engineer roles.

> 💼 I am actively seeking **remote or Berlin-based opportunities** in geospatial technology, GIS development, or spatial data engineering. If this work resonates with you, I'd welcome a conversation.
>
> 📅 [Book a 30-min intro call](https://calendly.com/alexanderariza/new-meeting) · ☕ [Support open geospatial work on Ko-fi](https://ko-fi.com/alexariza)

---

## 🗺️ What It Does

CityTank is a **fully client-side WebGIS application** that aggregates real-time fuel price data from Germany's official open API and presents it through an interactive, spatially-aware interface.

Key spatial operations it performs:

- **Buffer analysis**: Dynamically queries stations within a user-defined radius (5 km or 10 km) using the Tankerkönig REST API, equivalent to a spatial buffer query
- **Haversine distance computation**: Calculates geodesic distances between the user's GPS position and each station to estimate real-time travel time
- **Choropleth-style symbology**: Normalizes station prices within the active zone and applies a continuous green→amber→red color ramp per marker, scaled to local min/max — a standard thematic cartography technique
- **Real-time GPS integration**: Resolves user coordinates via the Browser Geolocation API, renders a pulsing location marker, and draws a geodesic buffer circle on the map
- **Routing integration**: Calls the OSRM API to compute and animate driving routes as GeoJSON LineString geometries rendered on the OpenLayers vector layer
- **Cartographic context**: Brent Crude Oil price (90-day time series) displayed as an inline chart to contextualize local pump prices within global commodity trends

---

## ✨ Feature Matrix

| Feature | Implementation |
|---|---|
| Base maps | CartoDB Dark Matter · OSM Street · ESRI World Imagery |
| Station markers | Dynamic OL vector layer, price-normalized color ramp |
| Cheapest station | Animated blinking green marker with pulsing ring |
| User location | Browser Geolocation API + Haversine travel time estimate |
| Analysis buffer | Parametric geodesic circle (5 km / 10 km) as polygon overlay |
| Routing | OSRM REST API → GeoJSON → animated OL LineString |
| Price chart | 90-day Brent Crude time series (Chart.js, amber gradient) |
| Zone statistics | Live min/avg/max with proportional mini bar charts |
| Station card | Address, open/closed status, travel time, brand logo |
| Navigation | Google Maps + Apple Maps deep-link integration |
| i18n | Full EN / DE localization across all UI strings |
| Responsive | Mobile-first layout, draggable bottom sheet, touch-optimized |
| Auto-refresh | Station data polling every 5 minutes |

---

## 🏗️ Technical Architecture

CityTank is a **zero-backend SPA** — all processing occurs in the browser. This is a deliberate architectural choice to demonstrate that sophisticated geospatial workflows do not require server infrastructure when designed correctly.

```
┌──────────────────────────────────────────────────────────────────┐
│                        Browser (Client)                          │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │                    UI Layer (HTML/CSS)                   │    │
│  │  Top pill · Right icon column · Draggable bottom sheet  │    │
│  │  Route info bar · Cheapest card · i18n (EN/DE)          │    │
│  └───────────────────────┬─────────────────────────────────┘    │
│                          │                                        │
│  ┌───────────────────────▼─────────────────────────────────┐    │
│  │              Core Application Logic (ES6)                │    │
│  │                                                          │    │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │    │
│  │  │  OpenLayers  │  │   Chart.js   │  │  Fetch API   │  │    │
│  │  │  Map Engine  │  │  Time Series │  │  HTTP Client │  │    │
│  │  └──────────────┘  └──────────────┘  └──────────────┘  │    │
│  │                                                          │    │
│  │  Spatial ops: buffer · Haversine · color normalization  │    │
│  └───────────────────────┬─────────────────────────────────┘    │
└──────────────────────────┼───────────────────────────────────────┘
                           │  REST / GeoJSON
          ┌────────────────┼────────────────────┐
          ▼                ▼                    ▼
   ┌────────────┐  ┌──────────────┐   ┌──────────────┐
   │Tankerkönig │  │ OSRM Routing │   │ CartoDB/ESRI │
   │  Fuel API  │  │   Engine     │   │  Tile Servers│
   │ (CC BY 4.0)│  │(BSD-2-Clause)│   │              │
   └────────────┘  └──────────────┘   └──────────────┘
```

### Stack

| Layer | Technology | Rationale |
|---|---|---|
| Map rendering | OpenLayers 8.2.0 | Industry-standard WebGIS library; supports WMS, WFS, XYZ, vector |
| Charting | Chart.js 4.4.0 | Lightweight canvas renderer; custom gradient fills |
| Routing | OSRM (project-osrm.org) | Open-source, low-latency driving routes via GeoJSON |
| Tile layers | CartoDB Dark Matter · OSM · ESRI | Multi-provider basemap strategy |
| Icons | Font Awesome 6 | Consistent icon system |
| Language | Vanilla ES6+ | No framework overhead; direct DOM control |
| Hosting | GitHub Pages | Static SPA; zero infrastructure cost |

---

## 🔌 Data Sources & Licensing

| Source | Endpoint | Data | License |
|---|---|---|---|
| **Tankerkönig** | `creativecommons.tankerkoenig.de` | Live fuel prices, station metadata, opening hours | CC BY 4.0 |
| **OSRM** | `router.project-osrm.org` | Driving routes as GeoJSON | BSD-2-Clause |
| **CartoDB** | `basemaps.cartocdn.com` | Dark Matter tile layer | CC BY 3.0 |
| **ESRI** | `server.arcgisonline.com` | World Imagery satellite tiles | ESRI Terms |
| **OpenStreetMap** | Nominatim | Geocoding | ODbL |

> All data licenses are respected in the UI with proper attribution.

---

## 🧮 Spatial Algorithms

### Haversine Distance (implemented in-browser)

Used to compute geodesic distance from user GPS position to each station, enabling travel time estimation without a routing API call per station:

```javascript
function haversineKm(lat1, lon1, lat2, lon2) {
    const R = 6371; // Earth radius in km
    const dLat = (lat2 - lat1) * Math.PI / 180;
    const dLon = (lon2 - lon1) * Math.PI / 180;
    const a = Math.sin(dLat/2)**2
            + Math.cos(lat1 * Math.PI/180)
            * Math.cos(lat2 * Math.PI/180)
            * Math.sin(dLon/2)**2;
    return R * 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
}
```

### Price-Normalized Color Ramp

Maps each station's price to a continuous RGB gradient anchored to local min/max, equivalent to a GIS choropleth renderer:

```javascript
// t = 0 (min/green) → 0.5 (avg/amber) → 1 (max/red)
const t = (price - zoneMin) / (zoneMax - zoneMin);
// Bilinear interpolation: green → amber → red
```

### Geodesic Buffer Circle

Approximates a geographic buffer polygon (64-point) around the analysis center using degree offsets derived from the target radius in meters:

```javascript
const dLat = (radiusMeters * Math.cos(angle)) / 111320;
const dLng = (radiusMeters * Math.sin(angle))
           / (111320 * Math.cos(lat * Math.PI / 180));
```

---

## 🚀 Getting Started

### Prerequisites

- Modern browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- Free API key from [Tankerkönig](https://creativecommons.tankerkoenig.de/) (registration required)

### Local Setup

```bash
# Clone the repository
git clone https://github.com/Geo-Way/CityTank.git
cd CityTank

# Open directly — no build step required
open index.html
# or serve with any static server:
python -m http.server 8080
```

### Configuration

Open `index.html` and replace the API key on line ~1355:

```javascript
const API_KEY = 'your-tankerkoenig-api-key-here';
```

### Deployment

Push to any static hosting platform — GitHub Pages, Netlify, Vercel, or an S3 bucket. No server-side processing required.

```bash
# GitHub Pages (assuming repo is already connected)
git add .
git commit -m "deploy: update CityTank"
git push origin main
```

---

## 🖥️ Application Screenshots

> *Add screenshots here showing: splash screen · map with markers · route animation · cheapest card panel*

| Splash / Onboarding | Map + Route | Station Detail |
|---|---|---|
| `img/screenshot-splash.png` | `img/screenshot-map.png` | `img/screenshot-popup.png` |

---

## 🗂️ Repository Structure

```
CityTank/
├── index.html          # Single-file SPA (HTML + CSS + JS)
├── img/
│   ├── Logo5.png       # GeoWay / CityTank brand asset
│   ├── favicon.ico
│   └── ...             # PWA icons (192×192, 512×512, apple-touch)
└── README.md
```

---

## 🔭 Roadmap

- [ ] **WFS/WMS layer integration** — overlay official German infrastructure data
- [ ] **PWA support** — offline caching via Service Worker for last-known prices
- [ ] **Historical API** — replace static Brent data with live FRED/EIA time series
- [ ] **Price alerts** — push notification when a station drops below threshold
- [ ] **Heatmap layer** — density/price surface using OL WebGL renderer
- [ ] **Multi-city comparison** — side-by-side zone statistics across cities
- [ ] **PostGIS backend** (optional) — persistent price history and trend analysis

---

## 👤 About the Author

**Alexander Ariza** — Geospatial Analyst & GIS Developer

I'm an independent geospatial developer with a background in remote sensing, spatial data analysis, and WebGIS. CityTank is part of a broader portfolio of open-source geospatial tools I'm building while seeking new professional opportunities.

**Core competencies:** OpenLayers · QGIS · PostGIS · Python (GeoPandas, Rasterio) · GDAL · REST API integration · Spatial statistics · Cartographic design

📫 **Reach out:**

| Channel | Link |
|---|---|
| 🌐 Portfolio | [geo-way.github.io/GeoWay.io](https://geo-way.github.io/GeoWay.io/) |
| 📅 Schedule a call | [calendly.com/alexanderariza/new-meeting](https://calendly.com/alexanderariza/new-meeting) |
| ☕ Ko-fi (support) | [ko-fi.com/alexariza](https://ko-fi.com/alexariza) |
| 🐙 GitHub | [@Geo-Way](https://github.com/Geo-Way) |

---

## 📄 License

```
MIT License — © 2025 Alexander Ariza / GeoWay

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software, to deal in the Software without restriction, including
the rights to use, copy, modify, merge, publish, distribute, sublicense,
and/or sell copies of the Software.
```

**Data attribution requirements** (non-negotiable per upstream licenses):
- Tankerkönig data → CC BY 4.0 — attribution displayed in UI footer
- OpenStreetMap data → ODbL — attribution displayed on map
- CartoDB basemap → CC BY 3.0 — attribution displayed on map

---

## 🙏 Acknowledgements

- [**Tankerkönig**](https://www.tankerkoenig.de/) — for making German fuel price data freely accessible under CC BY 4.0
- [**OpenLayers**](https://openlayers.org/) — for a robust, framework-agnostic WebGIS library
- [**Project OSRM**](http://project-osrm.org/) — for the open-source routing engine
- [**CARTO**](https://carto.com/) — for the beautiful Dark Matter basemap tiles
- [**OpenStreetMap**](https://www.openstreetmap.org/) contributors — for the foundational geographic data that powers this and countless other projects

---

<div align="center">

**If this project helped you, consider giving it a ⭐ — it helps more people find it.**

*Built with precision and purpose by [GeoWay](https://geo-way.github.io/GeoWay.io/) · Open Geospatial Innovation*

</div>
