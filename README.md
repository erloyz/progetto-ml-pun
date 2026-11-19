# ⚡ Italian PUN (Prezzo Unico Nazionale) Electricity Price Forecasting

## 📌 Project Overview
This repository contains a reproducible Machine Learning pipeline for Day-Ahead and Multi-Horizon forecasting of the Italian **PUN (Prezzo Unico Nazionale)** electricity clearing price (€/MWh) on the Day-Ahead Market (MGP).

The methodology strictly adheres to the **CRISP-DM (Cross-Industry Standard Process for Data Mining)** lifecycle. By integrating historical hourly price dynamics from the GME with exogenous spatial-meteorological observations (temperature, solar radiation, and wind speed sampled across representative Northern and Southern Italian hubs via Open-Meteo) and Italian calendar indicators, the project evaluates predictive accuracy, error degradation, and extreme risk across **24h, 48h, and 72h** forecasting horizons.

Developed as the Final Assignment for the **Machine Learning & Data Mining** course (Module 2) at the **University of Bologna (UNIBO)** under the supervision of **Prof. Matteo Francia**.

> **Note:** Documentation inside the Jupyter Notebooks and the accompanying academic deliverables are written in Italian for evaluation purposes.

---

## 👤 Author & Academic Credits
* **Andrea Loi** (`andrea.loi3@studio.unibo.it`)
  *Individual Project: Business Understanding, Spatial-Meteorological Data Ingestion, Causal Feature Engineering, Direct Multi-Horizon Modeling, CASH Hyperparameter Optimization, Weighted Ensemble Learning, Statistical Validation & Documentation.*

---

## 🧠 Key Methodological Highlights
* **Leakage-Free Direct Multi-Horizon Architecture:** Separate models trained independently for $+24\text{h}$, $+48\text{h}$, and $+72\text{h}$ horizons, strictly filtering autoregressive lags and rolling statistics to $t - h$.
* **CASH (Combined Algorithm Selection & Hyperparameter Optimization):** Automated search across 7 model families (*Ridge*, *Lasso*, *Decision Tree*, *Random Forest*, *XGBoost*, *SVR-RBF*, *MLP Regressor*) using `TimeSeriesSplit`, `Pipeline` scaling (`MinMaxScaler` / `StandardScaler`), and `scipy.stats` continuous/discrete distributions (`randint`, `uniform`, `loguniform`).
* **Heterogeneous Multi-Horizon Ensemble:** Convex combinations tailored per horizon to maximize algorithmic diversity (*XGBoost + Random Forest + MLP Regressor* at 24h; *XGBoost + SVR-RBF + Random Forest* at 48h and 72h).
* **Domain Evaluation & Statistical Validation:** Evaluation via MAE, RMSE, sMAPE (zero-safe), operational **Anomaly Index** ($\vert{}e_t\vert{} > 20\text{ €/MWh}$), Explainable AI (*Feature Importance*), and **Diebold-Mariano** statistical significance testing across all horizons.

---

## 📁 Repository Structure
```text
progetto-ml-pun/
├── README.md                           <- Project overview, methodology, and setup guide
├── requirements.txt                    <- Python dependencies (pandas, scipy, scikit-learn, xgboost, etc.)
├── .gitignore                          <- Ignored files (.venv, .DS_Store, checkpoints, heavy models)
├── data/
│   ├── raw/                            <- Raw GME PUN clearing prices and Open-Meteo hourly observations
│   └── processed/                      <- Chronologically split analytical matrices (X_train, y_train, X_test, y_test)
├── notebooks/
│   ├── 01_data_ingestion.ipynb         <- Data Ingestion, Weather Integration, Feature Engineering & Chronological Split
│   └── 02_modeling.ipynb               <- Baselines, CASH Multi-Horizon Tuning, Ensemble, XAI, DM Test & Deployment
├── artifacts/
│   ├── models/                         <- Serialized best estimators (.joblib) and ensemble weights
│   └── results/                        <- Exported CSV summary tables (metrics, Anomaly Index, Diebold-Mariano)
└── docs/
    ├── paper/                          <- LaTeX sources for the 4-page IEEEtran paper
    ├── presentation/                   <- Exam slides (10-minute presentation)
    └── paper_IEEE_PUN_Forecasting.pdf  <- Compiled final IEEE paper PDF
```

---

## 🚀 Quickstart: Local Execution & Google Colab

### 1. Local Setup (Virtual Environment)
To reproduce the environment locally from scratch, run the following commands in your terminal:

```bash
git clone [https://github.com/erloyz/progetto-ml-pun.git](https://github.com/erloyz/progetto-ml-pun.git)
cd progetto-ml-pun
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

1. Open and execute `notebooks/01_data_ingestion.ipynb` (*Run All*) to generate the clean analytical datasets inside `data/processed/`.
2. Open and execute `notebooks/02_modeling.ipynb` (*Run All*) to train the models, evaluate the ensembles, run the Diebold-Mariano tests, and export the final artifacts into `artifacts/`.

### 2. Google Colab Execution
Both notebooks include an automatic environment check in the first cell that clones the repository into `/content/progetto-ml-pun` and sets the working directory seamlessly. Upload the notebooks to [Google Colab](https://colab.research.google.com/) and run **Runtime → Run all**.

---

## 📄 Academic Deliverables
* **IEEE 4-Page Paper:** Available in `docs/paper_IEEE_PUN_Forecasting.pdf` (LaTeX sources in `docs/paper/`).
* **Exam Presentation:** 10-minute slide deck available in `docs/presentation/`.