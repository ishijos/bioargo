welcome to my bioargo project!

this repository contains the end-to-end pipeline for detecting and classifying Deep Chlorophyll Maxima (DCM) in BGC-Argo float profiles from the Indian Ocean, producing the dataset used in our paper.

everything here is built for five sub-regions:

- Arabian Sea (AS)
- Bay of Bengal (BoB)
- Equatorial Indian Ocean (EIO)
- Southern Indian Ocean (SIO)
- Seychelles-Chagos Thermocline Ridge (SCTR)

**what the pipeline does**

the single notebook `Deep_Chlorophyll_Maxima_Classifier.ipynb` handles everything end-to-end:

- **QC filtering:** only D (delayed) and A (adjusted) mode data accepted, flags 1/2/5 only
- **Smoothing:** resolution-dependent rolling filter (Cornec et al. 2021) — 5-point median for CHLA, median + mean for BBP700, only triggered when native vertical resolution ≤ 3 m
- **DCM detection:** subsurface CHLA peak classified as a DCM when chla_ratio ≥ 1.5 (rounded half-up), where chla_ratio = peak CHLA ÷ surface median in 0–15 m
- **DAM vs DBM split:** confirmed DCMs are further split by BBP700 — bbp_ratio > 1.3 → DBM (biomass), ≤ 1.3 → DAM (photoacclimation)
- **Mixed Layer Depth:** TEOS-10 sigma0 threshold of 0.03 kg/m³ from 10 dbar, linearly interpolated
- **Nitracline depth:** depth where nitrate first exceeds surface-layer mean + 1 µmol/m³ (Cornec et al. 2021)
- **26 °C isotherm depth:** linearly interpolated
- **Geographic cleaning:** basin assigned purely from lat/lon bounding boxes, profiles outside all boxes dropped
- **Satellite matching:** surface chlorophyll and PAR matched from monthly OCCCI/satellite NetCDF by nearest grid cell and calendar month

**output**

`io_data/basin_csvs/profileswithparandsurfchl.csv` — one row per valid profile with columns: `WMO_ID, cycle, date, lat, lon, monsoon_phase, DCM_TYPE, DCM_Depth, Chla_DCM, bbp_DCM, chla_ratio, bbp_ratio, MLD, nitracline_depth, isotherm_26C_depth, basin_box, surface_chl, PAR`

**input data**

- BGC-Argo Sprof NetCDF files from Argo GDAC (`fixed_*_chl_bioargo/`)
- monthly surface CHL: `io_data/chl_monthly_2012_2024_IO.nc` (OCCCI 2012–2024)
- monthly PAR: `io_data/par_monthly_2012_2024_IO.nc`

**dependencies**

```
pip install numpy pandas xarray gsw
```

thanks for drifting by, hope this helps!
