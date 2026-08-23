FML Week 3 - Problem Set Datasets
=================================
Policy: public sources FIRST. Every prompt fetches free, no-signup data
(yfinance daily prices). The CSV files below are OFFLINE FALLBACKS and
hand-calc references only.

1) fml_w3_prices_offline.csv      (252 rows)
   Same simulated 1y daily Close/Volume series as Week 2 (vol clustering,
   fat tails). Use for P1-P3 only if yfinance is blocked.

2) fml_w3_p1_paths.csv            (3 rows)
   The three 6-day price paths from the P1 hand calculation
   (entry 100, PT 104, SL 96, T = 6 days; labels +1 / -1 / 0).

3) fml_w3_p2_path.csv             (7 rows)
   The single 6-day path from the P2 hand calculation (entry 100).
   Same path yields +1 / -1 / +1 under knobs (+2,-2) / (+3,-1) / (+1,-3).

4) fml_w3_p3_events.csv           (8 rows)
   The eight events from the P3 meta-labeling hand calculation:
   primary side, momentum (%), barrier outcome, primary_correct (1/0).
   All-bets precision 4/8 = 50%; |mom| >= 2% filter -> 4/5 = 80%.


