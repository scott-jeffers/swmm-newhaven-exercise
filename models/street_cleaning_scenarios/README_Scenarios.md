# Catch-basin / street-cleaning scenarios (built from your edited baseline)

All six models use your baseline `WestHaven_JonesHill.inp` (OF-21708 system) unchanged in network and
subcatchments, plus a TSS water-quality setup and an 18-month continuous rainfall record.

| File | Scenario | Sumps | Street sweeping |
|---|---|---|---|
| S0_No_sumps.inp | Reference: catch basins are plain junctions | none | no |
| S1_Full_cleaning.inp | All basins vacuumed | 2.0 ft in all 7 | no |
| S2_Hybrid_cleaning.inp | Only downstream CB-48326 & CB-48324 cleaned | 2.0 ft downstream / 0.5 ft upstream | no |
| S3_No_cleaning.inp | No vacuuming | 0.5 ft in all (75% full) | no |
| S4_No_cleaning_street_sweeping.inp | Neglected sumps + sweeping | 0.5 ft | every 14 days |
| S5_Full_cleaning_street_sweeping.inp | Best case | 2.0 ft | every 14 days |

**Results (Jan 2025 – Jun 2026):** washoff 4,439 lb TSS. Trapped / to outfall:
S1 2,500 / 1,939 (56%) · S2 1,587 / 2,853 (36%) · S3 895 / 3,546 (20%) · S4 849 / 3,345 · S5 2,372 / 1,821.
Quality continuity error < 0.06% in every run. Full table: `Scenario_Results.csv`; per basin: `Basin_Results.csv`.

## How the sump is modeled (method from the Preliminary SWMM Modeling Summary)
- Each catch basin is a **STORAGE** node (4×4 ft, 16 ft²). Its invert is lowered by the sump depth while pipe
  inverts stay put (LINK_OFFSETS = ELEVATION), so pipes sit 2 ft (clean) or 0.5 ft (75% full) above the floor.
  Sumps start full of water.
- **[TREATMENT]** `TSS C = TSS * EXP(-0.5*HRT)` on every sump. Trapped TSS = SWMM "Mass Reacted".
- **Pollutant setup:** TSS, land uses ROAD (ROW subcatchments), RESIDENTIAL (parcels), COMMERCIAL (841 Jones Hill Rd).
  EXP buildup 80 / 40 / 60 lb/ac max at 0.4/day. EXP washoff C1 = 0.95, C2 = 1.5, calibrated to an EMC of about 100 mg/L (NURP median).
- **Sweeping (S4, S5):** ROAD every 14 days, availability 0.70, sweeping removal 50%.
- **Rain:** `HVN_2025-2026_hourly.dat`, Tweed-New Haven ASOS hourly precipitation (Iowa Environmental Mesonet),
  46.9 in over 18 months (2025 was a dry year). Monthly CT evaporation. Routing DYNWAVE at 10 s, 5-min reporting.

## Calibration warning
`k_sensitivity/` re-runs S1–S3 with k = 0.05, 0.1, 0.25 and 1.0 per hour. Full-cleaning capture ranges from 21% to 69%,
so k drives the answer. MassDEP credits deep-sump catch basins with 25% TSS removal, so k = 0.5 is probably optimistic.
The ranking Full > Hybrid > None holds for every k.

Note: the summary table in *Preliminary-SWMM-Modeling-Summary* has the Full and No-cleaning "Escaped" values swapped
relative to its text (text: Full 1,700 / No cleaning 2,032).
