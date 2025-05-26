[model_results_outliers_capped (1).csv](https://github.com/user-attachments/files/20433924/model_results_outliers_capped.1.csv)# Air Quality Prediction in India

Forecasting the Air Quality Index (AQI) using regression models on Indian air‐quality data. This project covers data ingestion, cleaning, EDA, outlier handling (removal vs. capping), feature scaling, model training (6 regressors + stacking), and evaluation.

---

## 📂 Dataset ##

- **Source:** Kaggle – “Air Quality Data in India” by rohanrao  
- **Download:** via `kagglehub` or manually from  
  `new_dataset1.csv`  
- **Key columns:**  
  - `Date` (YYYY-MM-DD)  
  - Pollutants/features:  
    `PM2.5`, `PM10`, `NO`, `NO2`, `NOx`, `NH3`, `CO`, `SO2`, `O3`  
  - Target: `AQI` (and optional `AQI_Bucket`)

---

## 🔍 Data Preprocessing

1. **Missing-Value Handling**  
   - Calculate null counts.  
   - Impute numerical with **median**; categorical (`AQI_Bucket`) with **mode**.

2. **Outlier Treatment**  
   - **Removal:** drop rows where any pollutant z-score > 3.  
   - **Capping:** clip each feature to μ ± 3σ.

3. **Feature Scaling**  
   - Standardize all pollutant columns before modeling.

4. **Train/Test Split**  
   - Time-aware split: first 80% dates → train, last 20% → test.

---

## 📊 Exploratory Data Analysis

- **Histograms & boxplots** for each pollutant  
- **Correlation matrix** for numerical features  
- **Pair plots** for AQI vs. key gases (`CO`, `O3`, etc.)

---

## 🛠️ Models Evaluated

| Model                      | Notes                                               |
|----------------------------|-----------------------------------------------------|
| Linear Regression          | Baseline                                            |
| Decision Tree Regressor    | Non-linear splits                                   |
| Support Vector Regressor   | Kernel-based                                        |
| Random Forest Regressor    | Bagged trees                                        |
| XGBoost Regressor          | Gradient boosting                                   |
| MLP Regressor              | Feedforward neural network                          |
| **Stacked Ensemble**       | Meta-model (Linear) on RF + XGB + MLP predictions   |

All models are trained via `train_evaluate(df, features, target='AQI')`, returning R², MAE, RMSE.

---

## 🚀 Results

- **Best with outliers removed:**  
  `{{Model}}` → R² = {{r2_removed}}, MAE = {{mae_removed}}, RMSE = {{rmse_removed}}
- **Best with outliers capped:**  
  `{{Model}}` → R² = {{r2_capped}}, MAE = {{mae_capped}}, RMSE = {{rmse_capped}}
- **Overall best:** typically **XGBoost** or **Stacked Ensemble**.

*  *


---

## ⚙️ Installation


git clone https://github.com/yourusername/air-quality-prediction.git
cd air-quality-prediction
pip install -r requirements.txt
