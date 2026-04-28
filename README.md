# Walmart Weekly Sales Forecasting (Time Series | SARIMA)

## Project Overview
This project builds an end-to-end time series forecasting system to predict weekly sales across 45 Walmart stores.

Using classical time series modeling (ARIMA & SARIMA), the project identifies key demand drivers, evaluates multiple models, and generates 12-week forecasts for each store.

The final solution achieves ~6.2% average forecasting error (MAPE) and is complemented by interactive Power BI dashboard to support business decision-making.

## Business Questions
The analysis answers the following questions:

1. Are weekly sales affected by unemployment, and which stores are most affected?
2. Do weekly sales show seasonal trends? If yes, when and why?
3. Does temperature affect weekly sales?
4. How does CPI affect weekly sales across stores?
5. Which stores are the top performers historically?
6. Which stores are the worst performers, and how large is the gap between top and bottom stores?
7. What are the next 12 weeks of forecasted sales for each store? Retail stores often struggle with:
- Overstocking (excess inventory costs)
- Understocking (lost sales opportunities)
- Poor demand visibility across locations

This project answers:
How can we accurately forecast weekly demand per store to improve inventory planning and operational efficiency?

## Dataset
- Source: Walmart weekly sales dataset
- Rows: 6,435
- Columns: 8
- Stores: 45
- Granularity: Weekly

| Column | Description |
|---|---|
| Store | Store number |
| Date | Week of sales |
| Weekly_Sales | Sales for the store in that week |
| Holiday_Flag | Whether the week is a holiday week |
| Temperature | Temperature in the region |
| Fuel_Price | Regional fuel price |
| CPI | Consumer Price Index |
| Unemployment | Regional unemployment rate |


## Exploratory Data Analysis (EDA)

## Key findings:

- Strong seasonality observed, especially during Q4 (Nov–Dec)
- Sales spikes align with holiday periods (Black Friday, Christmas)
- Weak correlation between sales and:
   - Unemployment
   - Temperature
   - CPI
- Significant store-level variation in performance and behavior

## Conclusion:
Sales are primarily driven by seasonality and store-specific dynamics, not macroeconomic variables.

## Modeling Approach

## Models Evaluated:
- ARIMA (baseline)
- SARIMA (seasonal model)

## Methodology:
- Time-based train/test split (last 12 weeks held out)
- ADF test for stationarity
- ACF/PACF for parameter selection
- Grid-style testing of model variants
- Evaluation using:
   - MAE
   - RMSE
   - MAPE

## Model Selection

## Best Model:

- SARIMA(1,0,0)(1,0,0,52)

## Why this model?
- Captures autoregressive behavior
- Captures annual seasonality (52 weeks)
- No differencing required → stable series

## Key Results
- Average MAPE across stores: ~6.20%
- Best Store MAPE: ~1.58%
- Worst Store MAPE: ~17.98%

## Insights:
- High-performing stores are highly predictable
- Some stores show volatile demand patterns
- Seasonal modeling significantly improves accuracy

## Forecasting Output
- Generated 12-week forecasts for all 45 stores
- Outputs stored as:
   data/processed/store_metrics.csv
   data/processed/store_12_week_forecasts.csv

## Power BI Dashboard
Interactive dashboards were built to visualize:

- Historical vs Forecasted Sales
- Store-level forecast performance (RMSE, MAPE)
- Top and worst performing stores
- Seasonal demand patterns

-- dashboard screenshot

## Business Impact
This solution enables:
- Improved inventory planning
- Better demand forecasting at store level
- Identification of:
   - predictable vs volatile stores
   - Proactive preparation for seasonal demand spikes

## Key Learnings
- Seasonality can exist even when not obvious in ACF/PACF plots
- SARIMA significantly outperforms ARIMA when seasonal patterns are present
- Forecast accuracy varies widely across stores
- Store-level modeling is more effective than aggregate modeling


## Project Structure

walmart-time-series-forecasting/

├── data/
│   ├── raw/
│   │   └── walmart.csv
│   ├── processed/
│   │   ├── store_metrics.csv
│   │   └── store_12_week_forecasts.csv
│
├── notebooks/
│   └── walmart_time_series_analysis.ipynb
│
├── dashboard/
│   ├── walmart_forecast_dashboard.pbix
│   ├── walmart_forecast_dashboard.twbx
│   └── images/
│       └── dashboard_overview.png
│
├── reports/
│   └── final_analysis_report.md
│
├── requirements.txt
├── README.md
└── .gitignore


## Installation & Usage

git clone https://github.com/majtom91/walmart-time-series-forecasting.git
cd walmart-time-series-forecasting
pip install -r requirements.txt

Run the notebook:
jupyter notebook notebooks/walmart_time_series_analysis.ipynb

## Tools Used
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Statsmodels
- Scikit-learn
- Power BI

## Future Improvements
- Hyperparameter tuning per store
- Compare with ML models (Random Forest, XGBoost)
- Incorporate external features (promotions, holidays calendar)
- Deploy forecasting API

