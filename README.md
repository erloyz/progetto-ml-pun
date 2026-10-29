# ⚡ Italian PUN (Prezzo Unico Nazionale) Electricity Price Forecasting

## 📌 Project Overview
This repository contains a reproducible Machine Learning pipeline for Day-Ahead and Multi-Horizon forecasting of the Italian **PUN (Prezzo Unico Nazionale)** electricity clearing price (€/MWh) on the Day-Ahead Market (MGP).

The methodology strictly adheres to the **CRISP-DM (Cross-Industry Standard Process for Data Mining)** lifecycle. By integrating historical price dynamics from the GME with exogenous spatial-meteorological observations (temperature, solar radiation, and wind speed sampled across representative Northern and Southern Italian hubs via Open-Meteo), the project evaluates predictive performance and accuracy degradation across **24h, 48h, and 72h** forecasting horizons.

Developed as the Final Assignment for the **Machine Learning & Data Mining** course (Module 2) at the **University of Bologna (UNIBO)** under the supervision of **Prof. Matteo Francia**.

---

## 👤 Author & Academic Credits
* **Andrea Loi** (Email: `andrea.loi3@studio.unibo.it`)  
  *Individual Project: Business Understanding, Spatial-Meteorological Data Ingestion, Feature Engineering, Multi-Horizon Model Training, Hyperparameter Tuning, IEEE Paper & Documentation.*

---

## 📁 Repository Structure
```text
progetto-ml-pun/
├── README.md                           <- Project overview, CRISP-DM workflow, and setup guide
├── requirements.txt                    <- Python dependencies (pandas, scikit-learn, xgboost, statsmodels, etc.)
├── .gitignore                          <- File patterns ignored by Git (.DS_Store, cache, checkpoints)
├── data/                               <- Data directory for full reproducibility
│   ├── raw/                            <- Raw GME PUN clearing prices and Open-Meteo hourly observations
│   └── processed/                      <- Feature-engineered analytical dataset (processed matrix)
├── notebooks/                          <- Executable Google Colab notebooks
│   ├── 01_data_ingestion_and_eda.ipynb <- Ingestion, time-alignment (UTC/CET), DST management, and EDA
│   └── 02_preprocessing_and_modeling.ipynb <- Feature engineering, multi-horizon split, tuning & benchmarking
└── docs/                               <- Academic deliverables
    ├── paper/                          <- LaTeX sources for the 4-page IEEEtran paper
    ├── presentation/                   <- Exam slides (10-minute presentation)
    └── paper_IEEE_PUN_Forecasting.pdf  <- Compiled final IEEE paper PDF
