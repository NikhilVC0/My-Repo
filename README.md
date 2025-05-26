# Air Quality Prediction in India

Forecasting the Air Quality Index (AQI) using regression models on Indian air‐quality data. This project covers data ingestion, cleaning, EDA, outlier handling (removal vs. capping), feature scaling, model training (6 regressors + stacking), and evaluation.

---

## 📂 Dataset ##

- **Source:** Kaggle – “Air Quality Data in India” by rohanrao  
- **Download:** via `kagglehub` or manually from  
  `new_dataset1.csv`  
 
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

-  # Best Model with Outliers Removed:
    Model: MLP Regressor, R2: 0.9130317702390841, MAE: 14.691832402059116, RMSE: 21.26248336557077

- # Best Model with Outliers Capped:
    Model: MLP Regressor, R2: 0.9222354774661881, MAE: 15.293082377227059, RMSE: 22.17956756100499

 *** Overall, the best model is MLP Regressor with outliers capped, achieving R2: 0.9222354774661881, MAE: 15.293082377227059, RMSE: 22.17956756100499

*  *


---

## ⚙️ Installation


git clone https://github.com/yourusername/air-quality-prediction.git
cd air-quality-prediction
pip install -r requirements.txt



### Above Project is Improved Model of a Research Paper titled "PREDICTION OF AIR POLLUTION USING 
SUPPORT  VECTOR MACHINE "    DOI No:     
JETIR November 2024, Volume 11, Issue 11                                                    
www.jetir.org (ISSN-2349-5162) 
