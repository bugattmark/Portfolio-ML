# Alpha Extraction Pipeline – Attempt 1

Full pipeline for alpha extraction attempt 1, evaluated with information coefficient.

---

### Results

- **IC mean**: ~0 → no useful alpha extracted  
- **IC std**: ~0.12 → noisy  
- **IC Sharpe**: ~0.03/0.04 → unreliable trading signal, should aim for ≥ 0.5

---

### Next Immediate Improvements

- Huge increase in magnitude of data; uncorrelated and diversified data is ideal, including alternative data  
- Build a proper risk model

---

### Method

#### Data Ingestion & Returns

- Downloaded daily close prices for approx. 100 large-cap tickers (2005–2025) with `yfinance`  
- Calculated log returns

#### Feature Engineering

- **Momentum**: 20‐day rolling sum of log‐returns  
- **Volatility**: 60‐day rolling standard deviation  
- **Skewness**: 60‐day rolling skew  
- **Beta**: 60‐day rolling regression slope vs equal‐weighted “market”; cross‐sectional mean  
- **Interactions**: momentum × volatility, beta squared  
- **Reversal**: negative 5-day cumulative return  

> These are textbook features, so understandably, no alpha was extracted.

#### Target Construction

- Shifted returns by −1 to make next-day log‐return the prediction target

#### Cross‐Sectional Normalisation

- z-scored every feature & target across tickers to remove level biases for each date

#### Modeling & IC Analysis

- Split time‐series: 80-20 train-test split  
- Standardized features  
- Trained 5 XGBoost regressors with different seeds  
- On test period: calculated Spearman rank‐correlation (IC) between predicted vs. actual returns daily  
- Evaluated IC mean, IC volatility, IC Sharpe  
- Plotted IC time series


