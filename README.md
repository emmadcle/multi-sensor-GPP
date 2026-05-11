# Data-driven cropland gross primary production retrieval with multi-sensor GPR models

**(Manuscript submitted to ISPRS)**

### GEE Harmonized Retrieval & GPR Prediction Pipeline

This repository provides an **R-based pipeline** for harmonized multi-source data extraction and GPP prediction using Gaussian Process Regression (GPR). The framework integrates **Google Earth Engine (GEE)** for scalable data acquisition with localized GPR inference to estimate daily Gross Primary Production (GPP) and associated epistemic uncertainty.

---

## Key Features
* **Automated Data Fusion:** Seamlessly integrates SAR (Sentinel-1), optical (Sentinel-2), and auxiliary (meteorological, soil and topographical) data.
* **Multi-Configuration Logic:** Dynamically selects the best-available GPR model (S1+Aux, S2+Aux, or S1+S2+Aux) based on cloud cover and sensor overpasses.
* **Uncertainty Quantification:** Provides per-pixel epistemic uncertainty estimates for every GPP prediction based on the GPR probabilistic formulation.
* **Scalable Acquisition:** Fetches site-level data without the need to download entire image collections, minimizing bandwidth and storage overhead.

---

## What it does
For a given coordinate and date range, the pipeline performs the following steps:

### 1. Data Acquisition via GEE
The pipeline fetches and harmonizes the following predictors:
* **Topography (Copernicus GLO-30 DEM):** Elevation, slope, aspect, and hillshade .
* **Soil Properties (SoilGrids 250m):** Texture, carbon content, pH, and other properties .
* **Meteorology (Daily ERA5-Land):** Temperature, Precipitation, Radiation, Wind, and VPD.
* **Radar (Sentinel-1):** SAR backscatter (VV, VH).
* **Optical (Sentinel-2):** Surface reflectance bands + cloud probability masking.

### 2. Preprocessing
Spatially aggregates high-resolution data within a 100m buffer and aligns all multi-source variables into a unified daily time series.

### 3. Inference
Applies pre-trained GPR models to generate daily GPP estimates ($gC \, m^{-2} \, d^{-1}$) and associated confidence intervals (epistemic uncertainty).

---

## Requirements
* A Google Earth Engine account.
* R environment with the `rgee` package installed and authenticated.
* Pre-trained GPR models (provided in ZENODO directory).

---

