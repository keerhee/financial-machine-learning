FML Week 12 - Problem Set Datasets
==================================
Policy: public / in-script sources FIRST. This week's corpus is TEXT,
defined INSIDE every script (no download can fail):

    docs = [
      'The Federal Reserve raised interest rates to fight inflation.',
      'Our refund policy allows returns within 30 days of purchase.',
      'Diversifying a portfolio lowers risk without lowering return.',
      'Quarterly earnings beat analyst expectations this period.' ]

Files in this zip (hand-calc references only):

1) fml_w12_p1_vectors.csv        (4 rows)
   The P1 toy 2-D sentence fingerprints: A(2,1), B(4,2), C(-1,2), D(0,3).
   cos(A,B) = 1.0 (paraphrases), cos(A,D) = 0.447, cos(A,C) = 0.

2) fml_w12_p3_docs.csv           (3 rows)
   The P3 keyword-count vectors over (rates, inflation, refund, return,
   earnings). Question q = (0,0,0,1,0) -> cos = 0 / 0.707 / 0
   -> retrieve d2 (refund policy), then fence the prompt:
   "Answer ONLY from the context; if absent, say NOT FOUND."

P2 numbers are on the slides: softmax over z = (2, 1, -1)
-> T=1: 70.5/25.9/3.5%;  T=0.5: 87.9/11.9/0.2%;  T=2: 54.7/33.1/12.2%.
Temperature is nerve, not knowledge.
