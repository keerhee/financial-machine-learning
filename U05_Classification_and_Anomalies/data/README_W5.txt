FML Week 5 - Problem Set Datasets
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

1) fml_w5_p2_applicants.csv       (6 neighbors + the query row)
   The P2 KNN table: Q(1.1, 0.6); sorted d^2 = 0.02, 0.05, 0.10,
   0.13, 0.17, 0.20. Verdicts: k=1 Default, k=3 Safe, k=5 Safe.

2) fml_w5_p3_likelihoods.csv      (3 clues + prior)
   The P3 Naive Bayes table. Posterior path:
   1% -> 10.8% -> 37.7% -> 80.9% (flag at the third clue).

P1 needs no file: z values are printed on the slide
(A +0.6, B -1.0, G -0.1; e-value helpers provided).
