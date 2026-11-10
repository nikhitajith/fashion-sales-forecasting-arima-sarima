Fashion E-Commerce Sales Forecasting with ARIMA and SARIMA
Forecasting daily fashion sales revenue on the Olist Brazilian e-commerce platform with classical time series models. Weekly seasonality is modelled explicitly with SARIMA and compared against an ARIMA baseline on a held-out 30-day window.

Author: Nikhita Ajith, M.Tech (Data Science), Amrita Vishwa Vidyapeetham, Coimbatore Course project

Results
Model	RMSE (R$) ↓	WMAPE accuracy ↑
ARIMA(1,0,1)	161.26	60.6%
SARIMA(1,0,1)(1,0,1,7)	160.21	61.3%
SARIMA beats ARIMA on both metrics, which shows the weekly shopping cycle is real and can be forecast. An accuracy of about 61% is realistic for noisy daily fashion revenue when no exogenous variables (promotions, holidays) are used.

Forecast vs actual

Dataset
Olist Brazilian E-Commerce Public Dataset contains real orders from Oct 2016 to Oct 2018. Four tables are used: orders, order items, products and category translation. The data is filtered to seven fashion sub-categories: bags & accessories, shoes, male clothing, female clothing, underwear & beach, sport, and children's clothes.

The dataset is not included in this repo. Download it from Kaggle and place the CSVs in data/.

Methodology
Preprocessing: merge the four tables with left joins, drop missing values, zero or negative prices and duplicates, then aggregate to a daily revenue series.
EDA: daily and monthly trends, the revenue distribution (right-skewed), outliers and revenue by category.
Stationarity: Augmented Dickey-Fuller test (statistic −6.04, p = 1.3 × 10⁻⁷), so the series is stationary and d = 0.
Order selection: ACF and PACF cut off after lag 1, giving p = 1 and q = 1.
Seasonality: additive decomposition with period 7 shows a stable weekly cycle.
Modelling: ARIMA(1,0,1) as the baseline and SARIMA(1,0,1)(1,0,1,7) as the primary model.
Evaluation: the last 30 days are held out and scored with RMSE and WMAPE-based accuracy. SARIMA residuals are also checked with residual ACF, a histogram and a Q-Q plot.
<p align="center"> <img src="images/decomposition.png" width="48%"> <img src="images/category_revenue.png" width="48%"> </p>
Evaluation metrics

Repository structure
├── Fashion_Sales_Forecasting.ipynb   # full analysis notebook
├── report/Report_final.pdf           # project report
├── images/                           # figures used in this README
├── data/                             # put the Olist CSVs here (not tracked)
└── requirements.txt
How to run
bash
git clone https://github.com/<your-username>/fashion-sales-forecasting.git
cd fashion-sales-forecasting
pip install -r requirements.txt
# download the Olist CSVs into data/
jupyter notebook Fashion_Sales_Forecasting.ipynb
Future work
SARIMAX with exogenous variables (discount flags, holidays, day-of-week dummies)
Separate models for each sub-category
Comparison with Prophet and gradient boosting
Tech stack
Python · pandas · NumPy · statsmodels · scikit-learn · Matplotlib · Seaborn
