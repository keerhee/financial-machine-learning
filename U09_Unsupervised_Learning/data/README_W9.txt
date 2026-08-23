FML Week 9 - Problem Set Datasets
=================================
Policy: public / in-script sources FIRST. The primary dataset this week is
the FREE yfinance panel from the setup guide, section 3(b):

    import yfinance as yf
    tickers = ['AAPL','MSFT','GOOGL','AMZN','META','KO','PEP','XOM','JPM','JNJ']
    prices  = yf.download(tickers, start='2020-01-01', end='2024-12-31',
                          auto_adjust=True, progress=False)['Close'].dropna()
    rets    = prices.pct_change().dropna()

Files in this zip (fallbacks / hand-calc references only):

1) fml_w9_p1_betas.csv            (6 rows)
   The P1 hand-calc data: market betas KO 0.5, PEP 0.6, JNJ 0.7,
   AAPL 1.3, AMZN 1.4, META 1.5. K = 2 from (0.5, 1.5) converges
   in 2 iterations to centers (0.6, 1.4): defensive vs growth.

2) fml_w9_panel_offline.csv       (252 x 11)
   Simulated daily returns panel (MKT + 10 stocks, same file as Week 4).
   Offline fallback if yfinance is unreachable.

P2 needs no file: the 2x2 correlation matrix [[1, rho], [rho, 1]] has
eigenvalues 1 +/- rho -> rho = 0.8: 1.8 / 0.2 (90%/10%);
rho = 0.2: 1.2 / 0.8 (60%/40%). PC1 = market mode, PC2 = spread mode.

P3 numbers are on the slides: lambda_plus = (1 + sqrt(N/T))^2
-> (10, 250): 1.44;  (500, 1260): 2.66. Eigenvalue 2.5 is signal on
the course panel but NOISE at the big-fund scale.
