# AeroGuard: Intelligent Prognostics for Aerospace Propulsion Systems ✈️⚙️

![R](https://img.shields.io/badge/Language-R-blue.svg)
![Quarto](https://img.shields.io/badge/Presentation-Quarto-blueviolet.svg)
![Machine Learning](https://img.shields.io/badge/Model-XGBoost%20%7C%20Random%20Forest%20%7C%20CoxPH-green.svg)
![RMSE](https://img.shields.io/badge/Best%20RMSE-17.53-brightgreen.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

> **A Grand Unified Model for Remaining Useful Life (RUL) Prediction of Turbofan Engines under Complex Operational Conditions.**

---

## 🎓 Academic Context & Attribution

This project was developed as a capstone implementation for the course **"Programmation Statistique avec R"** (Statistical Programming with R).

*   **Developer:** Aymen Mabrouk
*   **Institution:** Ecole Polytechnique Sousse
*   **Supervisor:** Pr. Abdallah Khemais
*   **Purpose:** Educational Research & Advanced Applied Statistics
*   **Data Source:** [NASA PCoE Prognostic Data Repository (C-MAPSS)](https://data.nasa.gov/dataset/C-MAPSS-Aircraft-Engine-Simulator-Data/x339-9te4)

---

## 📋 Executive Summary

In the aviation industry, engine failure is not an option. However, replacing engines too early results in millions of dollars in wasted operational life. **AeroGuard** solves the **"Run-to-Failure"** optimization problem, tackling the most complex scenarios including multi-regime operations and competing failure modes.

This system integrates **Statistical Mechanics (Cox PH)**, **Unsupervised Forensics (Clustering)**, and **Ensemble AI (XGBoost/Random Forest)** to predict engine failure with state-of-the-art accuracy.

### 🏆 The Scoreboard (Results)

| Dataset | Complexity | AeroGuard Strategy | RMSE Achieved |
|:---|:---|:---|:---:|
| **FD001** | Baseline (Sea Level) | Random Forest (Clipped RUL) | **17.53** 🏆 |
| **FD002** | Multi-Regime (6 Altitudes) | K-Means + Z-Score Normalization | **26.54** |
| **FD003** | Multi-Fault (Fan/Compressor) | Hierarchical Fault Classifier | **20.05** |
| **FD004** | **Ultimate (Combined)** | **Unified Pipeline (Regime + Fault)** | **32.97** |

---

## 📊 Key Visualizations

### 1. The "Death Signature" (FD001)
*Statistical proof that Static Pressure (Sensor 11) is the leading indicator of failure.*
![Hazard Ratio Plot](path/to/your/hazard_ratio_plot.png)
*(Note: Replace this link with your actual image path if available)*

### 2. Multi-Regime Normalization (FD002)
*Recovering the degradation signal from raw noisy flight data using Regime Clustering.*
![Normalization Plot](path/to/your/normalization_plot.png)

### 3. The Oracle (Prediction vs Truth)
*The AI (Blue line) accurately predicting the "Knee" of the failure curve.*
![Prediction Plot](path/to/your/prediction_plot.png)

---

## 🛠️ Methodology & Innovation

### Phase 1: The Baseline (FD001)
*   **Technique:** **Cox Proportional Hazards** identified "Static Pressure" (Sensor 11) as the primary death signal.
*   **Innovation:** Implemented "RUL Clipping" (capping targets at 125 cycles) to remove noise from healthy engine phases.

### Phase 2: Multi-Regime Dynamics (FD002)
*   **Challenge:** Engines operate at 6 different altitudes/speeds, causing sensor readings to "jump" wildly.
*   **Solution:** **K-Means Clustering** identified the 6 operating regimes. We applied **Z-Score Normalization** *within* each regime to neutralize the altitude noise.

### Phase 3: The Digital Pathologist (FD003)
*   **Challenge:** Engines fail due to two different causes: **Fan Degradation** or **Compressor Failure**.
*   **Solution:** **Hierarchical Clustering** was used as an unsupervised forensic tool to separate the failure modes. A **Fault-Aware XGBoost** model was trained to handle the specific physics of each failure type.

### Phase 4: The Grand Unified Model (FD004)
*   **Challenge:** The "Ultimate" dataset combining all regimes and all fault modes.
*   **Solution:** A pipeline combining the Regime Normalizer (from FD002) and the Fault Classifier (from FD003) into a single robust architecture.

---

## 📂 Project Structure

```bash
AeroGuard/
├── data/                   # Raw NASA C-MAPSS datasets
├── processed_data/         # Pre-calculated predictions (FD001-FD004)
├── models/                 # Saved AI Models (.rds)
│   ├── aircraft_engine_rul_predictor.rds
│   ├── FD004_XGBoost_Model.rds
│   └── FD004_Fault_Classifier.rds
├── notebooks/              # R Code
│   ├── 01_Baseline_FD001.ipynb
│   ├── 02_MultiRegime_FD002.ipynb
│   ├── 03_Diagnostics_FD003.ipynb
│   └── 04_Ultimate_FD004.ipynb
└── presentation/           # Final Defense
    └── AeroGuard_Presentation.qmd
```

---

## 🚀 Usage

### Prerequisites
```r
install.packages(c("tidyverse", "survival", "randomForest", "xgboost", "caret", "plotly", "quarto"))
```

### Inference (Using Pre-trained Models)
You can load the trained models directly without re-training:

```r
# Load the 'Grand Unified' XGBoost model
model <- readRDS("models/FD004_XGBoost_Model.rds")

# Make predictions on new sensor data
predictions <- predict(model, as.matrix(new_data))
```

---

## 📜 License

This project is licensed under the MIT License.

> *"In God we trust. All others must bring data."* - W. Edwards Deming
