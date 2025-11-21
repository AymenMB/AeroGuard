# AeroGuard: Intelligent Prognostics for Aerospace Propulsion Systems ✈️⚙️

![R](https://img.shields.io/badge/Language-R-blue.svg)
![Quarto](https://img.shields.io/badge/Presentation-Quarto-blueviolet.svg)
![Machine Learning](https://img.shields.io/badge/Models-XGBoost%20%7C%20Random%20Forest%20%7C%20CoxPH-green.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

> **A Grand Unified Model for Remaining Useful Life (RUL) Prediction of Turbofan Engines under Complex Operational Conditions.**

---

## 🎓 Academic Context & Attribution

This project was developed as a capstone implementation for the course **"Programmation Statistique avec R"** (Statistical Programming with R).

*   **Developer:** Aymen Mabrouk
*   **Institution:** Ecole Polytechnique Sousse
*   **Supervisor:** Pr. Abdallah Khemais
*   **Purpose:** Educational Research & Advanced Applied Statistics

---

## 📋 Executive Summary

In the aviation industry, engine failure is not an option. However, replacing engines too early results in millions of dollars in wasted operational life. **AeroGuard** solves the **"Run-to-Failure"** optimization problem using the **NASA C-MAPSS** dataset, tackling the most complex scenarios including multi-regime operations and multiple failure modes.

This system integrates **Statistical Mechanics (Cox PH)**, **Unsupervised Forensics (Clustering)**, and **Ensemble AI (XGBoost/Random Forest)** to predict engine failure with state-of-the-art accuracy.

### 🏆 The Scoreboard (RMSE Results)

| Dataset | Complexity | Method | AeroGuard RMSE | Industry Benchmark |
|:---|:---|:---|:---:|:---:|
| **FD001** | Baseline (Sea Level) | Random Forest | **17.53** | < 20 |
| **FD002** | Multi-Regime (6 Altitudes) | K-Means + Normalization | **26.54** | < 30 |
| **FD003** | Multi-Fault (Fan/Compressor) | Hierarchical Fault Classifier | **20.05** | < 25 |
| **FD004** | **Ultimate (Combined)** | **Unified Pipeline** | **32.97** | < 35 |

---

## 📂 Project Structure

The repository is organized to separate raw data, analysis code, and presentation assets.

```
AeroGuard/
├── data/                   # Raw NASA C-MAPSS datasets (txt)
│   ├── train_FD001.txt     # Training data
│   ├── test_FD001.txt      # Testing data
│   └── RUL_FD001.txt       # True RUL for validation
├── processed_data/         # Pre-calculated predictions and cleaned data (csv)
│   ├── processed_engine_data.csv
│   └── FD00*_Final_Predictions.csv
├── notebooks/              # Jupyter Notebooks for analysis and modeling
│   ├── Engine_Predictive_Maintenance.ipynb  # FD001 Analysis
│   ├── AeroGuard_FD002_MultiRegime.ipynb    # FD002 Analysis
│   ├── AeroGuard_FD003_Diagnostics.ipynb    # FD003 Analysis
│   └── AeroGuard_FD004_Ultimate.ipynb       # FD004 Analysis
├── presentation/           # Quarto Presentation files
│   ├── AeroGuard_Final_Presentation.qmd     # Master Presentation
│   └── style.css           # Custom styling
└── README.md               # Project Documentation
```

---

## 🛠️ Methodology & Innovation

### Phase 1: The Baseline (FD001)
*   **Goal:** Establish a baseline for single-regime operations.
*   **Technique:** **Cox Proportional Hazards** identified "Static Pressure" (Sensor 11) as the primary death signal. **Random Forest** was used for regression.

### Phase 2: Multi-Regime Dynamics (FD002)
*   **Challenge:** Engines operate at 6 different altitudes/speeds, causing sensor readings to "jump" wildly.
*   **Solution:** **K-Means Clustering** identified the 6 operating regimes. We applied **Z-Score Normalization** *within* each regime to neutralize the altitude noise, recovering the degradation signal.

### Phase 3: The Digital Pathologist (FD003)
*   **Challenge:** Engines fail due to two different causes: **Fan Degradation** or **Compressor Failure**.
*   **Solution:** **Hierarchical Clustering** was used as an unsupervised forensic tool to separate the failure modes. A **Fault-Aware XGBoost** model was trained to handle the specific physics of each failure type.

### Phase 4: The Grand Unified Model (FD004)
*   **Challenge:** The "Ultimate" dataset combining all regimes and all fault modes.
*   **Solution:** A pipeline combining the Regime Normalizer (from FD002) and the Fault Classifier (from FD003) into a single robust architecture.

---

## 💻 Technologies Used

*   **Language:** R (4.x)
*   **Data Manipulation:** `tidyverse`, `dplyr`, `tidyr`
*   **Survival Analysis:** `survival`, `survminer`
*   **Machine Learning:** `randomForest`, `xgboost`, `caret`
*   **Visualization:** `ggplot2`, `plotly`, `gridExtra`
*   **Presentation:** Quarto (`revealjs` engine)

---

## 🚀 Getting Started

### Prerequisites
Ensure you have R and the following libraries installed:

```r
install.packages(c("tidyverse", "survival", "randomForest", "xgboost", "caret", "plotly", "quarto"))
```

### Running the Analysis
Open any notebook in the `notebooks/` folder using VS Code or RStudio to reproduce the training and evaluation steps.

### Rendering the Presentation
To view the final defense presentation:
1.  Open `presentation/AeroGuard_Final_Presentation.qmd` in VS Code.
2.  Click the **Render** button (or run `quarto render` in the terminal).
3.  The presentation will generate an HTML file with interactive slides.

---

## 📜 License

This project is licensed under the MIT License - see the LICENSE file for details.

> *"In God we trust. All others must bring data."* - W. Edwards Deming
