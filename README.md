# welcome to my bioargo project! 

this repository contains modular code and data processing pipelines to download, clean, and analyze biogeochemical argo float profiles. 

everything here is customized for three specific regions in the Indian Ocean:
* Arabian Sea
* Bay of Bengal
* Equatorial Indian Ocean

---

## what's working right now

The current active pipeline is built to handle the end-to-end data processing:
* **Automation & Filtering:** It automates data fetching for the target regions, isolates chlorophyll data, cleans it using QC filtering, and drops any floats with fewer than 20 cycles.
* **Grid Mapping:** It interpolates everything onto a standard grid to fix depth mismatches between different floats.
* **Climatology & Plotting:** It creates depth-resolved monthly climatologies and plots them right alongside surface SST data from NOAA OISST.
* **5-Variable Update:** The codebase now handles five core variables: Chlorophyll-a, Nitrate, Dissolved Oxygen, Temperature, and Salinity.
* **Latitudinal Binning:** Added spatial processing to sort and analyze data across specific latitudinal bands.

---

## what's next

Post code-scrubbing, the next immediate step is jumping into feature extraction. The upcoming parts of the project will focus on:
* Calculating and analyzing **Mixed Layer Depth (MLD)** and **Deep Chlorophyll Maximum (DCM)** variations.
* Comparing how different QC filters impact the data accuracy.

This repository will keep growing with new research objectives once I'm done exploring!

---

## thanks for drifting by, hope this helps! 