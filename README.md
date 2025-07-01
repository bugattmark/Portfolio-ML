Full pipeline for Alpha extraction attempt 1, evaluated with information coefficient.
Results:
IC mean: ~0 => no useful alpha extracted
IC std: ~0.12 => noisy
IC sharpe: ~ 0.03/0.04 => unreliable trading signal, should aim for >= 0.5

Next immediate improvements:
***-Huge increase in magnitude of data, uncorrelated and diversified data is ideal, including alternative data
-Build a proper risk model


Method:
Data ingestion & returns
• Downloaded daily close prices for approx. 100 large-cap tickers (2005–2025) with yfinance
• Calculated log returns

Feature engineering
• Momentum: 20‐day rolling sum of log‐returns.
• Volatility: 60‐day rolling std
• Skewness: 60‐day rolling skew
• Beta: 60‐day rolling regression slope vs  equal‐weighted “market”, cross‐sectional mean
• Interactions: momentum x volatility, beta squared.
• Reversal: negative 5-day cumulative return.
(these are textbook features, so understandably, no alpha to be extracted)

Target construction
• Shifted returns by –1 to make next day log‐return the prediction target.

Cross‐sectional normalisation
• z-scored every feature & target across tickers to remove level biases for each date

Modeling & IC analysis
• Split time‐series, 80-20 train-test split
• Standardized features, x5 XGBoost regressors with different seeds
• On test period, calculated Spearman rank‐correlation (IC) between predicted vs actual returns for each day
• IC mean, IC volatility, IC Sharpe calculated and IC time series plotted


