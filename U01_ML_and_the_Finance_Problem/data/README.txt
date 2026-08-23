FML Week 1 — Problem Set Datasets
=================================
Policy: public sources FIRST. Every prompt in the deck fetches free, no-signup
data (yfinance for prices, sklearn fetch_openml('credit-g') for real credit
data). The CSV files below are OFFLINE FALLBACKS and hand-calc references only.

1) fml_w1_p1_returns_offline.csv   (504 rows)
   Simulated 2y daily returns, 2 tickers (fat-tailed, mild negative skew).
   Columns: date, AAPL_SIM, KRX005930_SIM
   Use only if yfinance is blocked. Properties: skew ~ -0.3/-0.4,
   excess kurtosis ~ 3, Jarque-Bera >> 5.99.

2) fml_w1_p3_borrowers.csv         (8 rows)
   The exact 8 applicants from the hand-calculation slides.
   Columns: applicant, income_100k, debt_100k, defaulted
   Use to verify your hand confusion matrix in code.

3) fml_w1_p3_credit_sim.csv        (10,000 rows)
   Simulated borrowers; P(default) rises with 2*debt - income (+noise),
   default rate ~ 8.7%. Columns: income_100k, debt_100k, defaulted
   Use only if you cannot run the simulation cell offline.

Problem 2 (overfitting) needs no file — the script generates its own data
with a fixed seed.
