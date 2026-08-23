FML Week 7 - Problem Set Datasets
=================================
Policy: public / in-script sources FIRST. The primary dataset this week is
GENERATED inside every script (no download can fail):

    from sklearn.datasets import make_classification
    X, yb = make_classification(n_samples=20000, n_features=20,
                                n_informative=6, weights=[0.99, 0.01],
                                random_state=42)

Real-data extension (free, no signup, no key):
    from sklearn.datasets import fetch_openml
    cc = fetch_openml('creditcard', as_frame=True)

The CSV files below are HAND-CALC references only:

1) fml_w7_p1_loans.csv            (10 loans)
   The P1 Gini table (6 repaid / 4 defaulted).
   Root Gini 0.48; income>50k split -> weighted 0.16 (gain 0.32);
   has_card split -> weighted 0.48 (gain 0).

2) fml_w7_p2_samples.csv          (3 bootstrap samples)
   The P2 bagging demo. A6 appears 0 / 2 / 3 times across T1-T3.
   Query (income<=50k, card=Y): verdicts Default / Default / Repaid
   -> majority vote 2-1 DEFAULT.

P3 needs no file: y = (0, 0, 1, 1), eta = 0.5,
SSE path 1.00 -> 0.25 -> 0.0625 (each round keeps (1-eta)^2 = 25%).
