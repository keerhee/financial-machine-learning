FML Week 16 - Problem Set Datasets (Final Week)
===============================================
Policy: public / in-script sources FIRST. The final set is nearly all
pencil work; the scaled labs use the IN-SCRIPT class dataset:

    from sklearn.datasets import make_classification
    X, yb = make_classification(n_samples=20000, n_features=20,
                                n_informative=6, weights=[0.99, 0.01],
                                random_state=42)

Files in this zip (hand-calc references only):

1) fml_w16_p1_confusion.csv       (6 rows)
   The P1 audit: 1,000 transactions, 20 frauds; TP 8, FP 2, FN 12,
   TN 978. Accuracy 98.6% vs dumb baseline 98.0%; precision 0.80,
   recall 0.40, F1 = 0.533. Luck bar for 20 trials with sd 0.5:
   0.5 * sqrt(2 ln 20) = 1.22 - a reported 1.2 is luck-level.

2) fml_w16_p3_rubric.csv          (3 rows)
   The P3 rubric: weights (.20, .15, .30, .20, .15). Totals:
   A fancy 5.20; B simple-honest 8.05; C middle 6.30.
   Test + explain carry 50% of the grade.

P2 numbers are on the slides: edge 30bp, cost 12bp, 40 trades,
vol 10% -> gross 12%, net (30-12)bp x 40 = 7.2%; Sharpe 1.20 -> 0.72;
breakeven 30bp; halved turnover net 3.6%.
