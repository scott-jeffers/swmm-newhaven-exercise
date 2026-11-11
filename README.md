# SWMM New Haven exercise – West Haven, CT (Jones Hill Rd / Platt Ave)

**Study report:** https://scott-jeffers.github.io/swmm-newhaven-exercise/report.html: the catch-basin and street-cleaning findings, with charts and an interactive basin map.

**Model viewer:** https://scott-jeffers.github.io/swmm-newhaven-exercise/: every model on the aerial map, with graphs and profiles. Deep links work, for example `#S1` or `#S1--ev20251030`.

A browser-based EPA SWMM 5.2 results viewer. You can:

- **Map:** see each model on an aerial background (EPSG:6434), with thematic coloring and a time slider/animation.
- **Graphs:** click any node, conduit or subcatchment for time-series graphs. You can compare scenarios or design storms.
- **Profile:** view hydraulic-grade-line profiles, animated, with the max HGL envelope.
- **Properties, report and .inp:** see element properties, the SWMM status report, and the full `.inp` text.

## Models (`models/`)

| Folder | What it is |
|---|---|
| `baseline/` | `WestHaven_JonesHill.inp`: the OF-21708 storm-drain system. `NOAA14_TypeII_24hr.dat` holds NOAA Atlas 14 24-hr depths (1–100 yr) with the NRCS Type II distribution. Change gage RG1's Station ID to switch storms. |
| `street_cleaning_scenarios/` | Six continuous TSS models (Jan 2025 – Jun 2026, Tweed-New Haven hourly rain): S0 no sumps, S1 full catch-basin cleaning, S2 hybrid, S3 no cleaning, S4 no cleaning + street sweeping, S5 full cleaning + sweeping. Catch-basin sumps are storage nodes with first-order HRT settling. See `README_Scenarios.md`. |
| `street_cleaning_scenarios/k_sensitivity/` | S1–S3 re-run with settling rate k = 0.05–1.0 /hr. |

Open any `.inp` in EPA SWMM 5.2 or PCSWMM. The rain files and background image sit next to the models, so the relative paths work.

## Site files

`report.html` (study report) and `index.html` (viewer), plus `data/*.json` (results extracted from each run's `.out`/`.rpt`). It is a static site with no build step. Leaflet and Plotly load from public CDNs.

## Data sources and caveats

- **Elevations:** from the project DEM, NAVD88 ft. Pipe inverts were estimated because there was no invert data.
- **Rainfall:** NOAA Atlas 14 Vol. 10 (PFDS). Hourly precipitation from ASOS HVN via the Iowa Environmental Mesonet.
- **Soils:** NRCS Soil Data Access.
- **Background imagery:** Esri World Imagery.
- **Water-quality parameters:** illustrative, not calibrated. Buildup, washoff and the settling rate k are teaching values. TSS removal results depend strongly on k.
