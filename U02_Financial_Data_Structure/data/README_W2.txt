FML Week 2 — Problem Set Datasets
=================================
Policy: public sources FIRST. Every prompt fetches free, no-signup data
(yfinance daily Close + Volume). The CSV files below are OFFLINE FALLBACKS
and hand-calc references only.

1) fml_w2_prices_offline.csv        (252 rows)
   Simulated 1y of daily Close and Volume with volatility clustering
   (GARCH-like) and fat tails. Columns: date, Close, Volume
   Use for P1 (dollar bars) and P2 (CUSUM) only if yfinance is blocked.

2) fml_w2_p1_10days.csv             (10 rows)
   The exact 10-day price/volume table from the P1 hand calculation.
   Columns: day, close, volume  (close*volume reproduces the $M table:
   8, 6, 20, 22, 5, 4, 6, 25, 5, 6)

3) fml_w2_p3_universe_sim.csv       (500 rows)
   Simulated fund universe: 500 funds x 24 monthly returns; the 150 worst
   first-year funds die in months 10-20 (later cells empty). Column
   dead_month marks the death. Survivor-only 1y mean ~ +11%, point-in-time
   1y mean ~ +5% (bias ~ 6-7 pp).
   Use for P3 only if you cannot run the simulation cell.

4) fml_w2_p3_funds.csv              (6 rows)
   The 6-fund hand-calc table (A-F, funds C and E die end of Year 1).

P2's hand-calc 8 returns are printed on the slide (no file needed).
