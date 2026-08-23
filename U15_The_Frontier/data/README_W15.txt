FML Week 15 - Problem Set Datasets
==================================
Policy: public / in-script sources FIRST. This week's demos are tiny
inline numpy examples - no downloads needed. The scaled labs generate
their own data in-script (seeded numpy).

Files in this zip (hand-calc references only):

1) fml_w15_p1_series.csv          (6 rows)
   The P1 attention series: past = (10.0, 10.5, 9.8, 12.0, 11.2, 13.5)
   with recency raw scores 1..6. Forecasts: flat 67.0/6 = 11.17;
   recency 245.4/21 = 11.69; all-on-last 13.50.

2) fml_w15_p2_graph.csv           (4 rows)
   The P2 graph: A-B, A-C, B-C, C-D; degrees (2,2,3,1); shock 5 at A.
   Update h <- 0.5h + 0.5*(Ah)/deg. Node D: 0 -> 0.42 -> 0.73 -
   the shock arrives in round 2, exactly its hop distance.

P3 numbers are on the slides: EV = P*V - (1-P)*L - cost, V = 10.
At L = 20: memory -2.0, RAG +7.5, search+RAG +7.7 (look it up).
At L = 2:  memory +5.2, RAG +8.4 (wins), search+RAG +7.88.
