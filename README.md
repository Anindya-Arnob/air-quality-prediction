# Air-Quality-Prediction

open code in google colab: 
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Anindya-Arnob/air-quality-prediction/blob/main/Airquality_pred.ipynb)

# 🌬️ Berlin Air Quality Prediction using LSTM

> Predicting PM2.5 concentrations in Berlin using Deep Learning (LSTM) and cloud-based data pipelines.

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat&logo=python)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange?style=flat&logo=tensorflow)
![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-green?style=flat&logo=supabase)
![License](https://img.shields.io/badge/License-Open%20Source-brightgreen?style=flat)

---

## 📌 Overview

Urban air quality monitoring is critical for public health. This project builds an **end-to-end machine learning pipeline** to predict **PM2.5 concentrations** in Berlin by analyzing its relationship with other pollutants — PM10, NO2, and O3.

The system uses a **Long Short-Term Memory (LSTM)** neural network, uniquely suited for capturing long-term dependencies in sequential atmospheric data.

📥 **Dataset Source:** [AQICN Berlin Historical Data](https://aqicn.org/historical/#city:germany/berlin)

---

## ✨ Key Features

- ☁️ **Cloud Data Ingestion** — Connects to Supabase (PostgreSQL) to fetch live/historical sensor data
- 🧹 **Robust Preprocessing** — Linear interpolation, forward/backward fill, temporal sorting
- 🧠 **LSTM Forecasting** — Stacked LSTM layers capturing long-term air quality patterns
- 📈 **Interactive Visualization** — Plotly charts comparing predicted vs. actual PM2.5
- 🛑 **Early Stopping** — Prevents overfitting on time-series data

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| **Data Source** | Supabase (PostgreSQL) |
| **Data Processing** | Python, Pandas, NumPy, Scikit-learn |
| **Deep Learning** | TensorFlow, Keras (LSTM) |
| **Visualization** | Plotly, Matplotlib |

---

## 📊 Dataset & Features

The model uses a **multivariate time-series dataset** with the following features:

| Feature | Description | Role |
|---------|-------------|------|
| `pm25` | Fine particulate matter (µg/m³) | 🎯 Target Variable |
| `pm10` | Coarse particulate matter | Input Feature |
| `no2` | Nitrogen Dioxide levels | Input Feature |
| `o3` | Ozone levels | Input Feature |

> ⚠️ Carbon Monoxide (`co`) was dropped during feature selection to optimize model performance.

---

## 🔄 Workflow
### 1️⃣ Data Retrieval
Fetches up to **4,000 rows** from the `berlin` table in Supabase using `supabase-py` client.

### 2️⃣ Preprocessing Pipeline
- Strip whitespace from column names
- Replace non-numeric markers (`-`) with `NaN`
- **Linear Interpolation** for missing values between known points
- **ffill / bfill** to handle boundary NaN values
- Chronological sorting with `DatetimeIndex`
- **MinMaxScaler** normalization (0 to 1)

### 3️⃣ LSTM Model Architecture
- Stacked LSTM layers for sequential pattern learning
- Sliding window approach — past N days → predict next day's PM2.5
- **Optimizer:** Adam | **Loss:** Mean Squared Error (MSE)
- **Early Stopping** on validation loss

### 4️⃣ Evaluation
Interactive Plotly line chart showing **Actual PM2.5 vs Predicted PM2.5** on the test set.

---

## ⚙️ Installation

```bash
pip install pandas numpy scikit-learn tensorflow supabase plotly
```

### Supabase Configuration
Add your credentials in the notebook:

```python
url = "YOUR_SUPABASE_URL"
key = "YOUR_SUPABASE_KEY"
```

---

## 📉 Model Performance

Performance is validated by comparing predictions against a withheld test set.
The interactive Plotly chart confirms the model successfully **follows Berlin's real air quality trends**.

> Metrics tracked: **MSE loss** (training & validation curves) + **Visual overlap** of actual vs. predicted values

---

## 📁 Project Structure
---

## 🔑 Key ML Concepts Demonstrated

- Time-Series Forecasting with LSTM
- Multivariate Sequential Data Processing
- Cloud Database Integration (Supabase)
- Feature Scaling & Missing Value Imputation
- Supervised Learning from Time-Series (sliding window)
- Early Stopping & Overfitting Prevention

---

## 📜 License

This project is open-source. For inquiries or contributions, please open an issue in the repository.

---

⭐ **If you found this project helpful, please give it a star!**
