# SWMM teaching exercises: solution files

Step-by-step instructions: https://scott-jeffers.github.io/swmm-newhaven-exercise/exercises.html

| File | Exercise |
|---|---|
| Ex1_one_subcatchment.inp | 1: one subcatchment, 50% impervious |
| Ex1b_one_subcatchment_90pct_imperv.inp | 1b: same at 90% impervious |
| Ex2_pipe_line.inp | 2: J1–J3, C1–C3 (18/24/30 in), outfall, profile "Main line" |
| Ex2b_pipe_line_undersized_C3.inp | 2b: C3 cut to 18 in (surcharge and flooding) |
| Ex3_pipe_line_TSS.inp | 3: Ex2 + TSS buildup/washoff, 7 antecedent dry days |
| Ex4_batch_reactor.inp | 4: closed tank, C = TSS*EXP(-0.5*DT/3600), matches C0*e^(-kt) |
| Ex4b_batch_reactor_HRT_pitfall.inp | 4b: same with EXP(-0.5*HRT), which over-removes (compounds every step) |
| Ex4c_batch_reactor_Kdecay.inp | 4c: same decay using pollutant Kdecay = 12/day |
| Ex5_catch_basins_as_reactors.inp | 5: Ex3 with J1–J3 as storage units (2 ft sumps) + settling |

All files are self-contained (rainfall is an internal time series). Open in EPA SWMM 5.2 and Run.
