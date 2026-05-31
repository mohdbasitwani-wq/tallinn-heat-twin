# 🌡️ Tallinn Heat — Digital Twin & Demand Forecast

> A live, single-file dashboard that shows a building's heating system as a **digital twin** and forecasts **next-day hourly heat demand** from the previous day plus the Tallinn weather forecast.

### 👉 [**Open the live dashboard**](https://[mohdbasitwani-wq.github.io/tallinn-heat-twin)

[![Open Live Demo](https://img.shields.io/badge/▶_Open_Live_Demo-34e0b0?style=for-the-badge)](https://mohdbasitwani-wq.github.io/tallinn-heat-twin/)

<p align="center">
  <img alt="HTML" src="https://img.shields.io/badge/HTML5-page-E34F26?logo=html5&logoColor=white">
  <img alt="Chart.js" src="https://img.shields.io/badge/Chart.js-4.4-FF6384?logo=chartdotjs&logoColor=white">
  <img alt="No build" src="https://img.shields.io/badge/single%20file-no%20build-34e0b0">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue">
</p>

## ✨ Features

- **Live building twin** — animated heat-pump loop, per-zone temperatures, supply/return/ΔT, with fan and pipe-flow speed scaling to real-time load.
- **6 KPIs** — current output, energy today, peak demand + time, cost (€), CO₂ (kg), live COP.
- **Next-day forecast** — degree-hour regression + 24 h-lag day shape, driven by tomorrow's Tallinn weather, vs a naive baseline, with MAPE badges (~4.8% vs ~6%).
- **Two weather modes** — winter design day, and live Tallinn forecast.
- **Alerts & flexibility feed**, hourly Nord Pool spot pricing, and a 7-day energy trend.
- **Controls** — play/pause, time scrubber, weather mode, night-setback toggle, setpoint slider — all recompute live.

## 🧠 How the forecast works

Heating load is close to linear in outdoor temperature within one operating mode. The engine fits today's 24 hours to a degree-hour line `load ≈ a + b·max(0, 17 − T_out)`, keeps the hourly leftover (the diurnal / hot-water / setback signature) as a 24-hour-lag shape, then re-evaluates on tomorrow's Tallinn forecast. This matches the literature finding that temperature at 1 h and 24 h lags are the dominant predictors — keeping the model transparent rather than a black box.

## 🚀 Run it

Open `index.html` in any browser — it runs fully, no build step. (Needs internet: Chart.js and fonts load from public CDNs.)

## ⚠️ Note on data

The building, loads, spot prices and grid carbon factor are realistic but **synthetic, editable assumptions** — not metered data. The live weather is the real Tallinn forecast fetched at build time. Swap in BMS data, the Elering spot feed, and a real building to operationalise.

## 📄 License

MIT — see [`LICENSE`](LICENSE).

---

Built by [@mohdbasitwani-wq](https://github.com/mohdbasitwani-wq).
