# Air Pollution Forecasting Using Machine Learning

> **Course:** Machine Learning | Nova School of Business & Economics
> **Date:** March 2025 | **Team:** Group T

---

## Team Members

- Sofia Pignataro
- Felix Otter
- Davide Dal Cero
- Francisco Manuel Nunes Mendes da Costa
- Moritz Müller
- Léon Philipp Klingele

---

## Research Question

> *"Can meteorological variables be used to accurately forecast hourly air pollution levels (PM2.5) in Beijing, enabling a public early-warning system for hazardous air quality conditions?"*

---

## Business Context

As an American consulting firm contracted by the **Municipality of Beijing**, the team was tasked with designing a machine learning pipeline to forecast air pollution levels on an hourly basis. The model was intended to power a mobile application or SMS notification service to alert Beijing residents when poor air quality is expected — enabling preventive actions such as wearing masks or reducing outdoor activities, particularly for individuals with respiratory conditions.

Air pollution accounts for approximately 9 million deaths per year globally, making accurate and timely forecasting a critical public health concern.

---

## Dataset

- **Source:** [Air Pollution Forecasting – LSTM Multivariate](https://www.kaggle.com/datasets/rupakroy/lstm-datasets-multivariate-univariate) (Kaggle)
- **Coverage:** Hourly records from 2010 to 2014, collected at the U.S. Embassy in Beijing
- **Target variable:** PM2.5 concentration (classified into Low / Medium / High pollution levels)
- **Features:** Temperature, dew point, atmospheric pressure, wind speed, wind direction, snow, rain

---

## Key Results

- **Random Forest achieved 81.7% accuracy** with a recall of **87.9% for the High Pollution class** after threshold adjustment — the best performing model
- **XGBoost** achieved 78.8% accuracy with 85.8% recall for high pollution
- **Logistic Regression** baseline: 74.3% accuracy, 71.4% recall for high pollution
- **ROC AUC** values of 0.95 (Low vs High), 0.91 (Low vs Medium), 0.89 (Medium vs High)
- **5-fold cross-validation** confirmed model stability: mean accuracy 81.1% ± 0.38%
- The **24-hour rolling mean of pollution** was the most important feature (36.4%), confirming strong temporal dependency

---

## Methodology

### 1. Exploratory Data Analysis
- Distribution analysis of all meteorological variables
- Correlation matrix — wind speed had the strongest negative correlation with pollution (-0.23)
- Time-series analysis revealed clear **seasonal pollution spikes**, particularly in winter months
- Outlier detection via z-score method — extreme winter pollution spikes retained as real events

### 2. Feature Engineering
- **Pollution lag variables** — 24-hour lag to capture temporal dependencies
- **Rolling statistics** — 24-hour rolling mean to smooth short-term fluctuations
- **Wind vector components** — wind direction converted to numerical wind_x and wind_y features
- **Temperature flags** — binary indicators for extreme heat (>30°C) and cold (<0°C)
- **Cyclical time encoding** — day of week encoded using sine/cosine to preserve cyclical nature
- **Seasonal features** — month mapped to Spring/Summer/Fall/Winter categories

### 3. Feature Transformation
- Log transformation for right-skewed pollution variables
- Standardisation for continuous meteorological variables
- Rain and snow converted to binary features (occurred / did not occur)
- Target variable (PM2.5) categorised into 3 classes based on percentiles: Low (≤25th), Medium (25th–75th), High (≥75th)

### 4. Model Selection & Comparison
| Model | Accuracy | Recall (High Pollution) |
|-------|----------|------------------------|
| Logistic Regression (baseline) | 74.3% | 71.4% |
| XGBoost | 78.8% | 85.8% |
| **Random Forest (selected)** | **81.7%** | **87.9%** |

### 5. Hyperparameter Tuning
- RandomizedSearchCV used for efficient hyperparameter search
- Decision threshold adjusted from default 0.5 to 0.3 to prioritise recall for the High Pollution class — a 10% improvement in detecting critical events at the cost of 0.8% overall accuracy

### 6. Model Explainability
Top features by importance:
1. Pollution rolling mean (24h) — 36.4%
2. Wind Y component — 11.7%
3. Pollution lag (24h) — 11.0%
4. Wind X component — 10.0%
5. Dew point — 9.7%

---

## Technologies Used

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-FF6600?style=flat)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=flat)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

---

## Skills Demonstrated

- **Time-Series Analysis** — Identifying seasonal patterns and temporal dependencies in environmental data
- **Feature Engineering** — Creating lag variables, rolling statistics, cyclical encodings, and domain-informed binary features
- **Multi-Class Classification** — Handling 3-class pollution prediction with threshold adjustment to optimise for critical class recall
- **Model Comparison & Selection** — Systematic evaluation of Logistic Regression, XGBoost, and Random Forest
- **Hyperparameter Tuning** — RandomizedSearchCV with cross-validation
- **Model Explainability** — Feature importance analysis to support business decision-making
- **Business Communication** — Framing technical findings in terms of public health impact and operational deployment

---

## Files

| File | Description |
|------|-------------|
| `GroupT_notebook.ipynb` | Full analysis and modelling notebook |
| `GroupT_report.pdf` | Final written report submitted to the course |

---

## How to Run

1. Clone this repository
   ```bash
   git clone https://github.com/franciscosta/air-pollution-forecasting.git
   ```
2. Open `GroupT_notebook.ipynb` in Jupyter or Google Colab
3. The notebook loads the dataset directly from a public GitHub URL — no manual download needed
4. Run all cells in order

---

## Course

Machine Learning — Nova School of Business & Economics, 2024/25
