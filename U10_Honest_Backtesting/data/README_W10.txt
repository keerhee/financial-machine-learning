FML Week 10 - Problem Set Datasets
==================================
Policy: public / in-script sources FIRST. The primary dataset this week is
the FREE yfinance series from the setup guide, section 2:

    import yfinance as yf
    px  = yf.download('AAPL', period='3y', auto_adjust=True,
                      multi_level_index=False, progress=False)['Close']
    ret = px.pct_change().dropna()

Random strategies (Lab 2 / P3) are generated IN-SCRIPT with a fixed seed.

Files in this zip (fallbacks / hand-calc references only):

1) fml_w10_p1_returns.csv        (5 rows)
   The P1 hand-calc returns: +2, -1, +3, 0, +1 (%).
   Mean 1%, sigma sqrt(2) ~ 1.41% -> SR monthly 0.71, annualized ~ 2.45.

2) fml_w10_p2_timeline.csv       (10 rows)
   The P2 purged-CV classification: 3-day label windows, test {5,6,7},
   embargo 1 day -> purge {3,4}, embargo {8}, honest train {1,2,9,10}.

3) fml_w10_prices_offline.csv    (252 rows)
   Simulated daily price series (same file as Week 2's offline fallback).
   Use if yfinance is unreachable.

P3 numbers are on the slides: luck's par = sqrt(2 ln N)/sqrt(756) x sqrt(252)
-> N=10: 1.24;  N=100: 1.75;  N=1000: 2.15. A Sharpe of 2.0 is promising
after 10 tries and fully explained by luck after 1,000.
