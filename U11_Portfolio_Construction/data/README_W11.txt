FML Week 11 - Problem Set Datasets
==================================
Policy: public / in-script sources FIRST. The primary dataset this week is
the FREE yfinance panel from the setup guide, section 3(b):

    import yfinance as yf
    tickers = ['AAPL','MSFT','GOOGL','AMZN','META','KO','PEP','XOM','JPM','JNJ']
    prices  = yf.download(tickers, start='2020-01-01', end='2024-12-31',
                          auto_adjust=True, progress=False)['Close'].dropna()
    rets    = prices.pct_change().dropna()

Files in this zip (fallbacks / hand-calc references only):

1) fml_w11_p3_clusters.csv        (4 rows)
   The P3 hand-calc setup: KO/PEP (variance 1, within-corr 0) and
   AAPL/AMZN (variance 1, within-corr 0.8). HRP: within IVP 50/50;
   cluster variances 0.5 vs 0.9; across split 64.3%/35.7%;
   final weights (32.1, 32.1, 17.9, 17.9)%.

2) fml_w11_panel_offline.csv      (252 x 11)
   Simulated daily returns panel (MKT + 10 stocks, same file as Weeks 4/9).
   Offline fallback if yfinance is unreachable.

P1 numbers are on the slides: sigma_p^2 = 125 + 100*rho (%^2)
-> rho +1: 15%;  rho 0: ~11.2%;  rho -1: 5%.

P2 numbers are on the slides: equal vols, rho = 0.95,
w1:w2 = (mu1 - rho*mu2):(mu2 - rho*mu1)
-> mu = (10%, 9.0%): (152.6%, -52.6%);  mu = (10%, 9.5%): (100%, 0%).
A 0.5pp forecast change = a 53-point position swing. IVP: (50%, 50%) both times.
