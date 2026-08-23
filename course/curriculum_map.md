# Curriculum Map — Sixteen Units, Fourteen Teaching Weeks

## Summary

The course is written as sixteen units of roughly three hours each — a lecture deck
and a problem set per unit, 32 decks in all. The semester is sixteen weeks, but
**week 8 is the midterm and week 16 is the final**, which leaves fourteen weeks to
teach in. Two weeks therefore carry two units.

The examination papers already fix where the line falls: the midterm covers units
1–8 and the final covers units 9–16. So the split is even, eight units either side,
and the pairings had to sit inside their own half.

---

## 1. The fourteen teaching weeks

| Teaching week | Unit(s) | Topic | Part |
|---|---|---|---|
| 1 | U1 | ML and the finance problem | I |
| 2 | U2 | Financial data structure — bars, the CUSUM filter | I |
| 3 | U3 | Labeling and meta-labeling — the triple barrier | I |
| 4 | U4 | Linear models and regularization | II |
| **5** | **U5 + U6** | **Logistic · KNN · Naive Bayes, and support vector machines** | II |
| 6 | U7 | Trees and ensembles | II |
| 7 | U8 | Neural networks and deep learning | II |
| **8** | **Exam** | **Midterm — units 1–8** | — |
| 9 | U9 | Unsupervised learning | II |
| 10 | U10 | Honest backtesting — purged CV, the Deflated Sharpe Ratio | III |
| 11 | U11 | Portfolio construction — HRP, NCO | III |
| 12 | U12 | NLP, LLMs and RAG | III |
| 13 | U13 | Reinforcement learning and execution | III |
| **14** | **U14 + U15** | **Causality, XAI and fairness, and the frontier** | IV |
| 15 | U16 | Integration and capstone (last class) | IV |
| **16** | **Exam** | **Final — units 9–16** | — |

Bold rows are the two double weeks and the two examination weeks.

---

## 2. Why these two pairings

| Week | Units | The seam |
|---|---|---|
| 5 | U5 + U6 | Both units teach classifiers, and U6 is the next one in the same sequence — logistic regression, KNN and Naive Bayes, then the support vector machine. The anomaly-detection thread runs the same way: LOF in U5, OCSVM in U6, and the syllabus already presents the four detectors in a single table. |
| 14 | U14 + U15 | Both are Part IV. U14 closes the argument about what a model may claim — causation, explanation, fairness — and U15 opens with a pipeline review that takes that argument as given before moving to transformers, graph networks and agents. |

### Pairings considered and rejected

- **U1 + U2.** Light enough to combine, but week 1 is where beginners settle in;
  doubling it front-loads the term at the worst moment.
- **U8 + U9.** Natural in content — deep learning then unsupervised structure — but
  the midterm sits between them.
- **U15 + U16.** Would compress the capstone, which needs its own week before the
  final examination.

---

## 3. Examinations

Both papers are 40 multiple-choice questions, 90 minutes, 2.5 points each for 100.
Every number in them is taken from a worked example in the lectures, so there is no
arithmetic a student has not already seen.

**Midterm — week 8, units 1–8.** Four parts: foundations and data (U1–2), labels and
linear models (U3–4), classification (U5–6), trees and neural networks (U7–8).

**Final — week 16, units 9–16.** Four parts: structure and honest testing (U9–10),
portfolios and language models (U11–12), reinforcement learning, causality and
fairness (U13–14), the frontier and integration (U15–16).

Answer keys are deliberately absent from this repository.

---

## 4. Unit shape

Each unit is a lecture deck of 38 slides and a problem set of 22, and each problem
set works three hands-on problems end to end. The data each problem needs sits in
that unit's `data/` directory — small CSVs, prepared for the exercise, no download
step and no vendor account.

The course keeps three industrial applications running the whole way through —
product recommendation, fraud detection, and an AI chatbot — and revisits each one
at every new level of machinery, from rules to LLMs.
