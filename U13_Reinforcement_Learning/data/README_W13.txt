FML Week 13 - Problem Set Datasets
==================================
Policy: public / in-script sources FIRST. This week's environments are
BUILT INSIDE every script (RL needs a world, not a table):

    # 1-D walk: reach the goal at the right end for a reward
    N_STATES = 6; ACTIONS = ['left', 'right']
    # execution: impact k*t^2 (k = 0.00002) + drift 0.01/period

File in this zip (hand-calc reference only):

1) fml_w13_p3_schedules.csv       (3 rows)
   The P3 execution bills: all-at-once 2,000 / TWAP 650 (impact 200 +
   drift 450) / front-half 600 (impact 400 + drift 200). The winner
   depends on conditions - that is the RL agent's job.

P1 numbers are on the slides: G = r1 + g*r2 + g^2*r3.
Grab (10,0,0) vs Invest (-2,0,20): gamma 0.5 -> 10 vs 3 (grab);
gamma 0.9 -> 10 vs 14.2 (invest); threshold gamma* = sqrt(0.6) ~ 0.775.

P2 numbers are on the slides: 3-state walk, alpha 0.5, gamma 0.9.
Q(1,R): 0.5 -> 0.75 -> 0.875;  Q(0,R): 0 -> 0.225 -> 0.45.
The goal's glow spreads backward one state per episode (TD learning).
