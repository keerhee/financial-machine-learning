FML Week 4 - Problem Set Datasets
=================================
Policy: public sources FIRST. Every prompt fetches free, no-signup data
(yfinance daily prices; SPY as the market / index). The CSV files below
are OFFLINE FALLBACKS and hand-calc references only.

1) fml_w4_panel_offline.csv       (252 rows)
   Simulated daily-return panel: MKT (market) + 10 stocks with true
   betas 0.5 - 1.5 and t-noise. Columns: date, MKT, AAPL_S ... JNJ_S.
   Offline substitute for all three problems (P1: any stock vs MKT;
   P2: one stock vs the other nine; P3: track the equal-weight average).

2) fml_w4_p1_points.csv           (4 rows)
   The four (market, stock) points from the P1 hand calculation.
   OLS answer: beta1 = 26/20 = 1.30, beta0 = -0.30, SSE = 0.20.

3) fml_w4_p3_betas.csv            (5 rows)
   The five standardized OLS betas from the P3 hand calculation.
   Soft threshold: lambda 0.25 keeps 3 of 5; lambda 0.40 keeps 2 of 5.

P2's hand-calc needs no file: beta_ridge = 26 / (20 + lambda).
