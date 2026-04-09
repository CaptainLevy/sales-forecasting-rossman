# 🛒 Rossmann Store Sales Forecasting

A complete end-to-end time series forecasting project using statistical 
and machine learning models on the Rossmann Store Sales dataset.

Built as part of M.Sc Statistics coursework to demonstrate applied 
time series analysis skills for data science placements.

---

## 📊 Results

| Model | RMSE | MAE | MAPE |
|-------|------|-----|------|
| **LightGBM** | **405.48** | **311.52** | **7.06%** 🥇 |
| Prophet | 434.24 | 325.22 | 7.42% |
| SARIMAX | 553.95 | 452.53 | 11.02% |
| Holt-Winters | 785.37 | 646.83 | 13.93% |
| SARIMA | 738.29 | 633.24 | 15.13% |

**Key finding:** LightGBM and Prophet are statistically equivalent 
(Diebold-Mariano p=0.511), both significantly outperforming 
classical models (p<0.05).

---

## 📁 Project Structure

```
sales-forecasting-rossman/
│
├── notebooks/
│   ├── 01_eda.ipynb               # Exploratory Data Analysis
│   ├── 02_preprocessing.ipynb     # Feature Engineering
│   ├── 03_classical_models.ipynb  # SARIMA, SARIMAX, Holt-Winters
│   ├── 04_advanced_models.ipynb   # Prophet, LightGBM
│   └── 05_evaluation.ipynb        # Model Comparison & DM Test
│
├── reports/                       # All generated plots
├── data/
│   ├── raw/                       # Downloaded from Kaggle (not tracked)
│   └── processed/                 # Engineered features (not tracked)
│
├── requirements.txt
└── README.md
```

---

## 🔍 Methodology

### 1. Exploratory Data Analysis
- Sales distribution analysis — confirmed right skew (skewness=1.595)
- STL and classical time series decomposition
- Formal stationarity testing — ADF and KPSS tests (both confirm d=0)
- ACF/PACF analysis — identified SARIMA(1,0,1)(1,1,1)[7] as candidate
- Promo effect — two-sample t-test (p≈0, Cohen's d=0.79, +38.8% sales)

### 2. Feature Engineering
- Calendar features — Year, Month, Day, WeekOfYear, IsDecember
- Competition features — months competitor has been open
- Promo2 active flag — binary indicator for recurring promo months
- Lag features — Sales at lags 1, 2, 3, 7, 14, 21, 28 days
- Rolling statistics — 7-day and 28-day rolling mean and std
- Final dataset — 813,118 rows × 43 columns

### 3. Classical Models
- **SARIMA(3,0,3)(0,1,2)[7]** — selected via auto_arima (AIC=-602.61)
- **SARIMAX(3,0,3)(0,1,2)[7]** — added Promo, SchoolHoliday regressors
- **Holt-Winters** — additive trend and seasonality, damped trend

### 4. Advanced Models
- **Prophet** — dual seasonality (weekly + yearly), Promo regressor
- **LightGBM** — trained on all 1,115 stores, 28 engineered features,
  early stopping at iteration 780

### 5. Statistical Evaluation
- Diebold-Mariano test for formal forecast accuracy comparison
- Residual analysis — mean, std, skewness, kurtosis
- Error analysis by day of week

---

## 🔑 Key Findings

1. **Stationarity** — Sales series is stationary (ADF+KPSS, d=0)
2. **Weekly seasonality** — Strong s=7 pattern, Monday/Sunday peak
3. **Promotions** — Single most important predictor (+38.8% sales)
4. **December effect** — 31% above annual average
5. **Feature importance** — RollingMean_28 and Lag_1 dominate LightGBM
6. **Statistical hierarchy** — LightGBM ≈ Prophet >> SARIMAX >> SARIMA

---

## ⚙️ Setup

### 1. Clone the repository
```bash
git clone https://github.com/CaptainLevy/sales-forecasting-rossman.git
cd sales-forecasting-rossman
```

### 2. Create virtual environment
```bash
python -m venv venv
source venv/bin/activate  # Mac/Linux
# venv\Scripts\activate   # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Download the dataset
Download from [Kaggle](https://www.kaggle.com/c/rossmann-store-sales) 
and place files in `data/raw/`:
```
data/raw/train.csv
data/raw/store.csv
data/raw/test.csv
```

### 5. Run notebooks in order
```
01_eda.ipynb → 02_preprocessing.ipynb → 03_classical_models.ipynb
→ 04_advanced_models.ipynb → 05_evaluation.ipynb
```

---

## 📦 Dependencies

```
pandas
numpy
matplotlib
seaborn
statsmodels
pmdarima
prophet
lightgbm
scikit-learn
scipy
jupyterlab
```

---

## 📉 Limitations

1. Models evaluated on Store 1 only — may not generalize to all 1,115
2. 41-day validation window is short for robust statistical testing
3. LightGBM requires future lag features — recursive prediction needed
   for true multi-step forecasting
4. No hyperparameter tuning on Prophet or SARIMA

---

## 🚀 Future Work

1. Walk-forward cross-validation across multiple stores
2. Hyperparameter tuning with cross-validation
3. Ensemble of LightGBM + Prophet
4. Neural approaches — LSTM, N-BEATS, Temporal Fusion Transformer
5. Store clustering before modelling

---

## 👤 Author

**Ankit** — M.Sc Statistics  
[GitHub](https://github.com/CaptainLevy)# 🛒 Rossmann Store Sales Forecasting

A complete end-to-end time series forecasting project using statistical 
and machine learning models on the Rossmann Store Sales dataset.

Built as part of M.Sc Statistics coursework to demonstrate applied 
time series analysis skills for data science placements.

---

## 📊 Results

| Model | RMSE | MAE | MAPE |
|-------|------|-----|------|
| **LightGBM** | **405.48** | **311.52** | **7.06%** 🥇 |
| Prophet | 434.24 | 325.22 | 7.42% |
| SARIMAX | 553.95 | 452.53 | 11.02% |
| Holt-Winters | 785.37 | 646.83 | 13.93% |
| SARIMA | 738.29 | 633.24 | 15.13% |

**Key finding:** LightGBM and Prophet are statistically equivalent 
(Diebold-Mariano p=0.511), both significantly outperforming 
classical models (p<0.05).

---

## 📁 Project Structure

```
sales-forecasting-rossman/
│
├── notebooks/
│   ├── 01_eda.ipynb               # Exploratory Data Analysis
│   ├── 02_preprocessing.ipynb     # Feature Engineering
│   ├── 03_classical_models.ipynb  # SARIMA, SARIMAX, Holt-Winters
│   ├── 04_advanced_models.ipynb   # Prophet, LightGBM
│   └── 05_evaluation.ipynb        # Model Comparison & DM Test
│
├── reports/                       # All generated plots
├── data/
│   ├── raw/                       # Downloaded from Kaggle (not tracked)
│   └── processed/                 # Engineered features (not tracked)
│
├── requirements.txt
└── README.md
```

---

## 🔍 Methodology

### 1. Exploratory Data Analysis
- Sales distribution analysis — confirmed right skew (skewness=1.595)
- STL and classical time series decomposition
- Formal stationarity testing — ADF and KPSS tests (both confirm d=0)
- ACF/PACF analysis — identified SARIMA(1,0,1)(1,1,1)[7] as candidate
- Promo effect — two-sample t-test (p≈0, Cohen's d=0.79, +38.8% sales)

### 2. Feature Engineering
- Calendar features — Year, Month, Day, WeekOfYear, IsDecember
- Competition features — months competitor has been open
- Promo2 active flag — binary indicator for recurring promo months
- Lag features — Sales at lags 1, 2, 3, 7, 14, 21, 28 days
- Rolling statistics — 7-day and 28-day rolling mean and std
- Final dataset — 813,118 rows × 43 columns

### 3. Classical Models
- **SARIMA(3,0,3)(0,1,2)[7]** — selected via auto_arima (AIC=-602.61)
- **SARIMAX(3,0,3)(0,1,2)[7]** — added Promo, SchoolHoliday regressors
- **Holt-Winters** — additive trend and seasonality, damped trend

### 4. Advanced Models
- **Prophet** — dual seasonality (weekly + yearly), Promo regressor
- **LightGBM** — trained on all 1,115 stores, 28 engineered features,
  early stopping at iteration 780

### 5. Statistical Evaluation
- Diebold-Mariano test for formal forecast accuracy comparison
- Residual analysis — mean, std, skewness, kurtosis
- Error analysis by day of week

---

## 🔑 Key Findings

1. **Stationarity** — Sales series is stationary (ADF+KPSS, d=0)
2. **Weekly seasonality** — Strong s=7 pattern, Monday/Sunday peak
3. **Promotions** — Single most important predictor (+38.8% sales)
4. **December effect** — 31% above annual average
5. **Feature importance** — RollingMean_28 and Lag_1 dominate LightGBM
6. **Statistical hierarchy** — LightGBM ≈ Prophet >> SARIMAX >> SARIMA

---

## ⚙️ Setup

### 1. Clone the repository
```bash
git clone https://github.com/CaptainLevy/sales-forecasting-rossman.git
cd sales-forecasting-rossman
```

### 2. Create virtual environment
```bash
python -m venv venv
source venv/bin/activate  # Mac/Linux
# venv\Scripts\activate   # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Download the dataset
Download from [Kaggle](https://www.kaggle.com/c/rossmann-store-sales) 
and place files in `data/raw/`:
```
data/raw/train.csv
data/raw/store.csv
data/raw/test.csv
```

### 5. Run notebooks in order
```
01_eda.ipynb → 02_preprocessing.ipynb → 03_classical_models.ipynb
→ 04_advanced_models.ipynb → 05_evaluation.ipynb
```

---

## 📦 Dependencies

```
pandas
numpy
matplotlib
seaborn
statsmodels
pmdarima
prophet
lightgbm
scikit-learn
scipy
jupyterlab
```

---

## 📉 Limitations

1. Models evaluated on Store 1 only — may not generalize to all 1,115
2. 41-day validation window is short for robust statistical testing
3. LightGBM requires future lag features — recursive prediction needed
   for true multi-step forecasting
4. No hyperparameter tuning on Prophet or SARIMA

---

## 🚀 Future Work

1. Walk-forward cross-validation across multiple stores
2. Hyperparameter tuning with cross-validation
3. Ensemble of LightGBM + Prophet
4. Neural approaches — LSTM, N-BEATS, Temporal Fusion Transformer
5. Store clustering before modelling

---

## 👤 Author

**Ankit** — M.Sc Statistics  
[GitHub](https://github.com/CaptainLevy)