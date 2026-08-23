FML Week 6 - Problem Set Datasets
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

1) fml_w6_p1_scores.csv           (6 customers)
   The P1/P2 risk-score line. P1 uses R1-R3 + D1-D2:
   b* = (4+8)/2 = 6, margin 2, support vectors R3(4) & D1(8).
   P2 adds R4 (score 7, repaid): hard margin b=7.5 / margin 0.5;
   soft margin keeps b=6 / margin 2 with slack xi = 3.

2) fml_w6_p3_distances.csv        (3 transactions)
   The P3 RBF table: d^2 = 1, 4, 25 to the normal prototype.
   gamma 0.5 -> K = {0.61, 0.14, ~0} (flags T2, T3 at K < 0.2);
   gamma 0.1 -> K = {0.90, 0.67, 0.08} (flags T3 only).
