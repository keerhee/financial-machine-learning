FML Week 14 - Problem Set Datasets
==================================
Policy: public / in-script sources FIRST. The scaled labs use the
IN-SCRIPT class dataset:

    from sklearn.datasets import make_classification
    X, yb = make_classification(n_samples=20000, n_features=20,
                                n_informative=6, weights=[0.99, 0.01],
                                random_state=42)

Files in this zip (hand-calc references only):

1) fml_w14_p1_days.csv           (10 rows)
   The P1 confounding table: 5 rally days (+2% each, buzz high on 4)
   and 5 calm days (0%, buzz high on 1). Naive buzz gap = 1.2pp;
   within-regime gaps = 0 and 0 -> the signal is 100% confounder.

2) fml_w14_p3_groups.csv         (2 rows)
   The P3 fairness counts: both groups 100 applicants, 80 qualified.
   A: 60 approved (TPR 75%, acc 80%); B: 40 approved (TPR 50%, acc 60%).
   Parity gap 20pp; opportunity gap 25pp - equal talent, unequal odds.

P2 numbers are on the slides: base 0.40, f(I)=0.30, f(D)=0.70,
f(D,I)=0.65 -> phi_D = +0.325, phi_I = -0.075;
0.40 + 0.325 - 0.075 = 0.65 exactly (additivity).
