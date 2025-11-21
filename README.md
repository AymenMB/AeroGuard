# AeroGuard: Intelligent Prognostics for Aerospace Propulsion Systems ✈️⚙️

![R](https://img.shields.io/badge/Language-R-blue.svg)
![Machine Learning](https://img.shields.io/badge/Model-Random%20Forest-green.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)
![RMSE](https://img.shields.io/badge/RMSE-17.53-brightgreen.svg)

> **A High-Fidelity Survival Analysis and Machine Learning pipeline to predict the Remaining Useful Life (RUL) of aerospace propulsion systems.**

---

## 🎓 Academic Context & Attribution

This project was developed as a capstone implementation for the course **"Programmation Statistique avec R"** (Statistical Programming with R).

*   **Developer:** Aymen Mabrouk
*   **Institution:** Ecole Polytechnique Sousse
*   **Supervisor:** Pr. Abdallah Khemais
*   **Purpose:** Educational Research & Advanced Applied Statistics

---

## 📋 Executive Summary

In the aviation industry, engine failure is not an option. However, replacing engines too early results in millions of dollars in wasted operational life. This project solves the **"Run-to-Failure"** optimization problem using the **NASA C-MAPSS** dataset.

By leveraging **Cox Proportional Hazards** for risk identification and **Random Forest Regressors** for time-series prediction, this system allows engineers to detect degradation onset up to **50 cycles in advance**.

### 🏆 Key Performance Metrics
*   **RMSE (Root Mean Squared Error):** `17.53` (Industry benchmark < 20).
*   **Concordance (Risk Accuracy):** `0.955` (95.5% accuracy in identifying failing engines).
*   **False Negatives (Critical Failures missed):** Minimally reduced via "Safe Mode" thresholding.

---

## 🛠️ Technical Architecture

The solution is built entirely in **R** using the **Tidyverse** ecosystem, moving through four distinct phases of reliability engineering.

### 1. Data Ingestion & Forensics
*   **Source:** NASA Commercial Modular Aero-Propulsion System Simulation (C-MAPSS).
*   **Challenge:** Processed raw, unlabeled sensor logs into "Run-to-Failure" trajectories.
*   **Technique:** Implemented "Ghost Column" cleaning and reverse-calculated RUL targets based on failure cycles.

### 2. Statistical Survival Analysis
*   **Goal:** Identify *which* sensors drive failure.
*   **Method:** **Cox Proportional Hazards Model**.
*   **Discovery:** **Static Pressure (Sensor 11)** was identified as the primary leading indicator with a Hazard Ratio > 200 (P-value < 2e-16).

### 3. Advanced Feature Engineering
*   **Rolling Window Statistics:** Calculated rolling means and **standard deviations (volatility)** over a 5-cycle window using `zoo` and `dplyr`.
*   **Dimensionality Reduction:** Applied **Principal Component Analysis (PCA)** to compress 14 sensors into a single **"Health Index"** for pilot visualization.

### 4. Machine Learning (The Oracle)
*   **Algorithm:** **Random Forest Regressor** (50 Trees).
*   **Strategy:** Implemented "RUL Clipping" (capping healthy engines at 125 cycles) to remove training noise and improve convergence.
*   **Result:** Accurately predicted the "Knee" of the degradation curve on unseen test data.

---

## 📊 Visualizations & Insights

### The "Death Signature"
Statistical analysis revealed that **Sensor 11 (High-Pressure Compressor Outlet Pressure)** and **Sensor 12 (Fan Speed)** are the dominant signals. As the engine degrades, pressure rises exponentially while fan speed drops to compensate for friction.

### AI Performance (Predicted vs Actual)
The Random Forest model demonstrates tight tracking of the actual degradation slope on unseen test data:

*(Note: See the `output/` folder for full resolution plots)*

---

## 💻 Installation & Usage

### Prerequisites
This project requires **R 4.0+** and the following libraries:

```r
install.packages(c("tidyverse", "survival", "randomForest", "zoo", "plotly", "corrplot"))
```

### Running the Project
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/turbofan-predictive-maintenance.git
   ```
2. Open `coding/Engine_Predictive_Maintenance.ipynb` in Jupyter, RStudio, or Google Colab.
3. Ensure the `data/` folder contains the NASA datasets.
4. Run all cells to generate the analysis and train the model.

---

## 📂 Repository Structure

```
├── coding/
│   ├── Engine_Predictive_Maintenance.ipynb # Main R Source Code
│   └── engine_health.html                  # Interactive Health Dashboard
├── data/                   # Raw NASA C-MAPSS datasets (FD001)
│   ├── train_FD001.txt     # Run-to-failure training data
│   ├── test_FD001.txt      # Censored test data
│   └── RUL_FD001.txt       # Ground truth labels
├── data_unused/            # Other datasets (FD002-FD004)
├── models/
│   └── aircraft_engine_rul_predictor.rds  # Pre-trained Random Forest Model
├── processed_data/
│   └── processed_engine_data.csv
├── presentation.qmd        # Quarto Presentation
└── README.md               # Project Documentation
```

---

## 🚀 Future Roadmap & Challenges

While this project achieves state-of-the-art results on the **FD001** dataset (Single Operating Condition, Single Failure Mode), real-world deployment involves handling complex flight envelopes.

### Why FD001? (The Gold Standard)
*   **Clarity:** Allows for the demonstration of pure algorithmic performance (Cox, Random Forest, PCA) without the noise of flight physics.
*   **Visuals:** Generates smooth, interpretable degradation curves ideal for academic presentation.
*   **Results:** An RMSE of `17.53` proves mastery of Predictive Maintenance concepts.

### The "Jumping Data" Problem (FD002 & FD004)
In FD001, the aircraft flies at a constant altitude and speed. In **FD002**, the aircraft climbs, dives, and accelerates.
*   **The Challenge:** If Sensor 11 (Pressure) spikes, is the engine failing, or did the pilot just throttle up?
*   **The Solution:** Requires **Regime Normalization**.
    1.  Cluster data into "Operating Regimes" (Takeoff, Cruise, Descent).
    2.  Normalize sensor data (Z-score) within each regime.

### The "Ambiguous Failure" Problem (FD003 & FD004)
In FD001, all engines fail due to High-Pressure Compressor degradation.
*   **The Challenge:** In **FD003**, engines may fail due to **Fan degradation** OR **Compressor degradation**. The "Death Signature" for a fan failure looks completely different.
*   **The Solution:** Requires a **Multi-Head Model**.
    1.  **Classification Head:** Predicts *how* the engine will fail (Failure Mode Classification).
    2.  **Regression Head:** Predicts *when* it will fail based on the specific mode.

---

## 📝 Conclusion

This project demonstrates that combining **Classical Statistics** (for interpretability) with **Modern Machine Learning** (for predictive power) yields superior results in reliability engineering tasks. The resulting model is capable of deployment as a real-time decision support system for fleet maintenance.

---

*© 2023 Aymen Mabrouk - Ecole Polytechnique Sousse*
