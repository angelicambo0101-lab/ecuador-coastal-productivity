# Data folder

This folder is a placeholder. The notebooks in `notebooks/` read and write
NetCDF files here; the raw files themselves are not included in this
repository because of their size (~1200 weekly files per variable).

## `weekly_schedule.xlsx`

A two-column spreadsheet (`start_date`, `end_date`) defining the 1200 weekly
periods covering 2002-07-04 to 2025-11-05, used to drive every download and
processing step. Generate it with:

```python
import pandas as pd

start = pd.Timestamp("2002-07-04")
n_weeks = 1200
weeks = pd.DataFrame({
    "start_date": [start + pd.Timedelta(days=7 * i) for i in range(n_weeks)],
    "end_date":   [start + pd.Timedelta(days=7 * i + 6) for i in range(n_weeks)],
})
weeks.to_excel("weekly_schedule.xlsx", index=False)
```

## Expected folder layout after running `01_data_download.ipynb`

```
DATA_ROOT/
├── weekly_schedule.xlsx
├── CMEMS_weekly/
│   ├── SST/    SST_week_0001.nc ... SST_week_1200.nc
│   ├── SSS/    SSS_week_0001.nc ... SSS_week_1200.nc
│   └── MSL/    MSL_week_0001.nc ... MSL_week_1200.nc
├── CHL/        CHL_week_0001.nc ... CHL_week_1200.nc
├── WIND/       WIND_week_0001.nc ... WIND_week_1200.nc
├── WIND_DIRECTION/
├── ERA5_monthly/
└── quality_control.xlsx
```

`DATA_ROOT` is set at the top of each notebook and can point to a local path
or a mounted Google Drive folder.
