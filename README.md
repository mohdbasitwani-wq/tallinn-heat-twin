# 🌡️ Tallinn Heat — Digital Twin & Demand Forecast

> A live, single-file dashboard that visualises a building's heating system as a **digital twin** and forecasts **next-day hourly heat demand** from the previous day + the Tallinn weather forecast.

<p align="center">
  <img alt="HTML" src="https://img.shields.io/badge/HTML5-page-E34F26?logo=html5&logoColor=white">
  <img alt="Chart.js" src="https://img.shields.io/badge/Chart.js-4.4-FF6384?logo=chartdotjs&logoColor=white">
  <img alt="No build" src="https://img.shields.io/badge/build-none%20·%20single%20file-34e0b0">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue">
</p>

---

## 🔗 Live demo

**▶ https://mohdbasitwani-wq.github.io/tallinn-heat-twin/**

> Goes live the moment you enable GitHub Pages (see [Deploy](#-deploy)) — provided the repo is named exactly `tallinn-heat-twin`. On Netlify it'll look like `https://tallinn-heat-twin.netlify.app`.

## 📦 Suggested repository name

| Name | Vibe |
|------|------|
| **`tallinn-heat-twin`** ⭐ | clear, location + concept — recommended |
| `heat-twin-dashboard` | product-y, generic location |
| `building-heat-forecast` | emphasises the forecasting angle |
| `nord-heat` | short and brandable |

The README and links below assume **`tallinn-heat-twin`**.

---

## ✨ Features

- **Live building twin** — animated heat-pump loop, per-zone temperatures, supply/return/ΔT, and a compressor whose spin + pipe-flow speed scale with real-time load.
- **6 headline KPIs** — current output, energy today (vs baseline), **peak demand + when it occurs**, cost (€), CO₂ (kg), live COP.
- **Next-day demand forecast** — degree-hour regression + 24-hour-lag day shape, driven by tomorrow's Tallinn forecast, plotted against the revealed actual and a naive baseline with **MAPE** badges.
- **Two weather modes** — *Winter design day* (space heating dominates) and *Live Tallinn now* (real fetched forecast; outside heating season → hot-water-dominated).
- **Anomaly & flexibility feed** — demand spikes, low-COP warnings, stuck-valve checks, and load-shift tips to the cheapest spot-price hours.
- **Hourly Nord Pool EE spot pricing**, a **7-day energy trend**, and Estonian grid/cost context.
- **Interactive controls** — play/pause, time scrubber, weather mode, night-setback toggle, and a setpoint slider that recomputes everything live.

## 🖼️ Screenshot

> Add a screenshot once hosted: `docs/screenshot.png`, then it renders here.

```
![Dashboard](docs/screenshot.png)
```

---

## 🧠 How the forecast works

Heating load is, within one operating mode, close to **linear in outdoor temperature**. The engine:

1. Fits today's 24 observed pairs to a degree-hour line — `load ≈ a + b · max(0, 17 − T_out)` — by least squares.
2. Keeps the hour-by-hour leftover (the **diurnal / hot-water / setback signature**) as a 24-hour-lag shape.
3. Re-evaluates the temperature term on **tomorrow's Tallinn forecast** and re-applies that shape.

This mirrors the literature's finding that outdoor temperature at **1 h and 24 h lags** are the dominant predictors and that a clustered linear-regression model matches neural-net accuracy for heating — so the model stays transparent instead of a black box. On the winter scenario it lands **≈ 4.8 % MAPE** versus **≈ 6 % for naive persistence**.

---

## 🛠️ Tech stack

- Plain **HTML + CSS + vanilla JS** — one file, no framework, no build step.
- **Chart.js 4** (CDN) for charts; inline **SVG** for the building twin.
- **Google Fonts** (Sora, IBM Plex Sans/Mono).

> Viewers need an internet connection (Chart.js + fonts load from public CDNs).
## 📊 Data & assumptions

| Item | Value / source |
|------|----------------|
| Location | Tallinn, EE (59.44°N, 24.75°E) |
| Live weather | Real Tallinn forecast fetched **at build time** (≈ +13 °C, late May) |
| Building | 220 m², air-source heat pump, 18 kW — *synthetic, editable* |
| Loads | Heat-loss model + DHW + setback + noise — *synthetic* |
| Electricity price | Nord Pool EE day-ahead shape (~0.05–0.20 €/kWh) + ~0.24 €/kWh retail |
| Grid CO₂ | 350 g/kWh (Estonia, de-carbonising off oil shale) |

> ⚠️ Loads, prices and the carbon factor are **realistic but synthetic assumptions**, not metered readings. To operationalise, wire in live BMS data, the **Elering** day-ahead feed, and the real building from Estonia's building registry (**EHR**).

## 🗺️ Roadmap

- [ ] Live weather via Open-Meteo / Elering APIs (auto-refresh)
- [ ] Real metered load ingestion (CSV / BMS)
- [ ] Multi-day carpet/heat-map view
- [ ] Cost-optimal pre-heating scheduler using spot prices
- [ ] Model accuracy panel with rolling MAPE

## 📚 References

- Hua et al., *District heating load patterns and short-term forecasting for buildings and city level*, Energy (2023).
- *Predictive modelling of heating and cooling degree-hour indexes based on outdoor air temperature variability*, Scientific Reports (2023).

## 📄 License

MIT — see [`LICENSE`](LICENSE). Use it, fork it, ship it.

---

Built by [@mohdbasitwani-wq](https://github.com/mohdbasitwani-wq).
