# Coastal Ecuador Biophysical Productivity — Code Archive

Code archive for the manuscript *"Geospatial analysis of the biophysical
conditions associated with primary productivity along the Ecuadorian coast"*,
submitted to *Journal of Geophysical Research: Oceans* (AGU). This repository
contains the data-acquisition, geospatial analysis, and figure-generation
code used to produce the results reported in the manuscript, in support of
reproducibility.

## Overview

The study analyzes 23 years (2002–2025) of satellite and reanalysis
observations over the Ecuadorian coastal zone (1°S–2°S), integrating five
biophysical variables — sea surface temperature (SST), sea surface salinity
(SSS), mean sea level (MSL), 10-m wind, and chlorophyll-a — to evaluate
Bakun's Triad hypothesis and the Optimal Environmental Window framework for
this region.

## Repository structure

```
.
├── notebooks/
│   ├── 01_data_download.ipynb      # Acquisition of all five variables (CMEMS, ERA5/CDS, NASA Ocean Color)
│   └── 02_results_figures.ipynb    # Long-term trends, seasonal cycle, spatial climatology, correlation maps
├── data/
│   └── README.md                   # Expected folder layout and weekly schedule format (no raw data included)
├── requirements.txt
└── LICENSE
```

## Data sources

| Variable | Source | Product | Resolution |
|---|---|---|---|
| SST, SSS, MSL | Copernicus Marine Service (CMEMS) | [GLOBAL_MULTIYEAR_PHY_001_030](https://data.marine.copernicus.eu/product/GLOBAL_MULTIYEAR_PHY_001_030/description) | 0.083° |
| Wind (10 m) | ERA5 reanalysis, Copernicus Climate Data Store | [ERA5 hourly data on single levels](https://doi.org/10.24381/cds.adbb2d47) | 0.25° |
| Chlorophyll-a | NASA Ocean Color, MODIS-Aqua | L3m daily, 4 km | 4 km |

Full citations are listed in the manuscript's reference list and Open
Research statement.

## Running the notebooks

Both notebooks were developed for Google Colab and expect a Google Drive
folder as the working data directory (`DATA_ROOT`, set at the top of each
notebook). They also run locally with minor changes — replace the
`drive.mount(...)` cell with a local path and skip it.

1. **`01_data_download.ipynb`** downloads the five variables and writes one
   NetCDF file per variable per week to `DATA_ROOT`. Requires free accounts
   with Copernicus Marine Service, NASA Earthdata, and the Copernicus Climate
   Data Store (CDS) — see the credentials note inside the notebook. No
   credentials are stored in the code; the CDS token is read from the
   `CDS_API_KEY` environment variable or a local `~/.cdsapirc` file.
2. **`02_results_figures.ipynb`** reads the NetCDF files produced above and
   generates the manuscript's result figures (long-term trends, interannual
   anomalies, seasonal cycle, spatial climatology, and Pearson/Spearman
   correlation maps between chlorophyll-a and the physical variables).

## Requirements

See `requirements.txt`. Core dependencies: `xarray`, `numpy`, `pandas`,
`scipy`, `matplotlib`, `cartopy`, `copernicusmarine`, `earthaccess`, `cdsapi`.

## Citation

If you use this code, please cite the manuscript (citation details to be
added upon publication) and, where applicable, this repository's archived
release.

## License

Released under the MIT License — see `LICENSE`.
