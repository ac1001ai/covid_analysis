# COVID-19 Vaccination Forecasting

## Project Overview
This project utilizes a public COVID-19 dataset from [Our World in Data](https://github.com/owid/covid-19-data/tree/master/public/data/vaccinations) to perform time series forecasting for vaccination progress. The goal is to predict future vaccination rates using ARIMA modeling and analyze trends over time. The code for this project is stored in vaccination_forecast.ipynb, and just to note, not all the visualizations display in the notebook preview.

## Thought Process

### 1. Data Loading and Preparation
- Load data from the Our World in Data GitHub repository.
- Perform initial exploration and handle missing values.
- Set up country filtering for focused analysis.

### 2. Exploratory Data Analysis (EDA)
- Visualize global vaccination progress. (

### 3. Time Series Forecasting with ARIMA
- Prepare time series data for the selected country.
- Test for stationarity and apply differencing if needed.
- Justify ARIMA selection:
  - Suitable for time series data with trends.
  - Captures vaccination rate slowdown as saturation approaches.
  - Can account for seasonality if present.

### 4. Model Analysis and Interpretation
- Examine residuals and forecast accuracy.
- Compare forecasts for multiple countries.

## Challenges
- Identifying a suitable dataset that runs efficiently in a Jupyter notebook.
- Configuring a local Conda environment after a long gap in usage.
- Refreshing knowledge on time series forecasting methodologies.

## Results Interpretation

### Time Series Analysis and Stationarity
- **Dickey-Fuller Test**: p-value = **0.0000051** → Series is stationary (no differencing required).
- **Autocorrelation Analysis**:
  - PACF suggests **p=1** (lag 1 influence).
  - ACF suggests **q=1** (slow decay/spikes).
- **Selected Model**: ARIMA(1,0,1) based on ACF/PACF analysis.

### Forecast Insights
- Projected vaccination rate remains stagnant or declines slightly.
- Uncertainty increases over time (wider confidence intervals).
- No projected achievement of 70%, 80%, or 90% full vaccination within forecast period.

### Residual Analysis
- Residuals show deviation from normality (heavy tails, potential skewness).
- Model underestimates extreme values, affecting confidence intervals.
- Possible improvements:
  - Log transformation for variance stabilization.
  - SARIMA for seasonal effects.
  - Inclusion of exogenous factors (e.g., policy changes, new variants).

## Next Steps
### Model Refinement
- Implement a **train/test split** evaluation (last 30 days as test set).
- Optimize ARIMA parameters using a grid search.
- Evaluate performance using **MAE, RMSE**.

### Data Science Enhancements
- Assess data quality (handling outliers, irregular reporting patterns).
- Engineer additional features (demographics, healthcare indicators, policy changes).
- Compare ARIMA with **SARIMA, Prophet, LSTM** for better accuracy.
- Implement **rolling window cross-validation** for robust model evaluation.
- Fine-tune hyperparameters using **Bayesian optimization**.

## Deployment Considerations
### Azure Implementation
#### **Model Hosting**
- Deploy trained ARIMA model as a **REST API** via **Azure Machine Learning Service**.
- Secure API endpoints using authentication keys.

#### **Data Pipeline Automation**
- Use **Azure Functions** to automate daily data retrieval and preprocessing.
- Schedule **weekly/monthly model retraining** based on new data.
- Store raw vaccination data in **Azure Blob Storage**.
- Use **Azure SQL Database** for structured storage.

#### **Web Interface & API Management**
- Deploy a **dashboard via Azure App Service** to visualize forecasts.
- Use **Azure API Management** for unified access control.

### Monitoring & Maintenance
- Implement **Azure Monitor** for resource tracking.
- Use **Application Insights** to log data updates and retraining events.
- Set up **alerting for failures and anomalies**.
- Monitor model performance, forecast accuracy, and adjust retraining frequency.
- Enable **cost tracking and budget alerts** in **Azure Cost Management**.

---
This project provides a scalable and automated approach to forecasting vaccination rates, leveraging cloud-based deployment for continuous updates and real-time insights.

