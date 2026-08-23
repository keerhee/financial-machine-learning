FML Week 8 - Problem Set Datasets
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

The CSV file below is a HAND-CALC reference only:

1) fml_w8_p2_xor.csv              (4 rows)
   The P2 XOR truth table with the two-layer forward pass:
   h1 = step(x1+x2-0.5) 'OR', h2 = step(x1+x2-1.5) 'AND',
   y = h1 - h2 -> (0,0)->0, (1,0)->1, (0,1)->1, (1,1)->0.

P1 needs no file: w = (-1, +2), b = 0 on (Income, Debt);
z = +0.6 / -1.0 / -0.1 -> sigmoid 0.65 / 0.27 / 0.47 (= Week 5).

P3 needs no file: E(w) = (w-3)^2 from w = 0;
eta 0.25 -> gap halves; eta 0.5 -> one step; eta 1.1 -> gap x1.2 diverges.
