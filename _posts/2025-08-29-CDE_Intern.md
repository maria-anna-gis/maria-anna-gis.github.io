# Turning WorldPop Data into Action: My Internship at the Christian Doppler (CD) Laboratory for geospatial and EO-based humanitarian technologies (GEOHUM)

From 7 July to 29 August 2025, I interned for 8 weeks full-time at the Christian Doppler Lab for geospatial and EO-based humanitarian technologies (GEOHUM), supporting Médecins Sans Frontières in exploring how WorldPop’s high-resolution age–sex data can inform field decisions.

My task was to build a reproducible pipeline that turns 60 TIFs into meaningful outputs which can be utilised in both static and interactive map products for use by MSF.

## What I built

I created a two-notebook workflow:

1. **WorldPop Raster Processing** — Clips all 60 age–sex rasters to an AOI, stacks them into a multi-band composite, aggregates custom age groups, and exports ready-to-use layers. Key tools for this were rasterio, xarray/dask, geopandas and ArcPy.

2. **Zonal Statistics & Population Pyramids (ArcGIS Pro)** — Explodes multipart AOIs, runs per-band zonal stats, writes clean CSV/GPKG outputs, and generates static population pyramids (grouped and single-age). It also names files with human-readable labels using a regex, and shows progress bars for heavy steps.

These outputs could then be utilised in static maps and interactive dashboards, with the intention that analysts can move from data to decisions quickly.

## What I learned

* **Python > Model Builder**: Early ArcGIS Pro models were slow and brittle; the Python/Dask route proved faster and more scalable.
* **NetCDF trade-offs**: While attractive for structure/compression, NC was heavy and crash-prone in ArcGIS for this use case—so I stuck with multi-band GeoTIF.
* **Limits matter**: WorldPop often use the same age-shape proportions across admin units, so pyramids may look similar even when totals differ; this was an important caveat for interpretation.

## Small R detour

I briefly explored **WOPR** (the WorldPop R package) and **woprVision** for catalogue queries and quick country-level figures. This was useful for rapid checks, but Python + ArcGIS handled the heavy lifting better for MSF’s workflow.

## Roadblocks & next steps

Uploading the full composite to ArcGIS Online ran into licensing and file-size limits; right now, I am still exploring vector/tile alternatives. A further future enhancement is including direct API downloads from WorldPop into Notebook 1, especially relevant with the WorldPop update on 4 September. I’m also discussing contributing to a review paper on gridded population products with SpaSe and colleagues.

## Gratitude

Huge thanks to **Sophia Klaußner**, **Lorenz Wendt**, and **Yann Rebois** for guidance.

## Code

All scripts developed during my internship are available to view on my repo here: [maria-anna-gis/worldpop_processing](https://github.com/maria-anna-gis/worldpop_processing)
