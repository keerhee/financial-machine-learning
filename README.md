# Financial Machine Learning

Yonsei University · for 3rd- and 4th-year undergraduates, beginners welcome · 16 units

**Browse and download → https://keerhee.github.io/financial-machine-learning/**

From what machine learning is, through the algorithms, to the parts that only matter
in finance: bars and the CUSUM filter instead of the calendar, the triple barrier
instead of "will it go up tomorrow", purged cross-validation instead of a naive
backtest, and a Deflated Sharpe Ratio to tell you when the result was luck.

Built on Hull's *Machine Learning in Business*, López de Prado's *Advances in
Financial Machine Learning*, and *Causal Factor Investing* — and carried through
three industrial applications: product recommendation, fraud detection, and an AI
chatbot.

**35 PDFs · 981 slides · 37 practice data files.** A lecture deck and a problem set
for each of the sixteen units, the syllabus, and both examination papers. **Only
PDFs, CSVs and Markdown are tracked** — the editable PPTX and DOCX sources are
excluded by `.gitignore`.

---

## Layout

| Path | Contents |
|---|---|
| `U01_ML_and_the_Finance_Problem/` … `U16_Integration_and_Capstone/` | Per unit: the lecture deck, the problem set, and a `data/` directory with the CSVs its three problems use |
| `course/` | Syllabus and the [curriculum map](course/curriculum_map.md) |
| `exams/` | Midterm and final papers — questions only |
| `site/` | The GitHub Pages listing page (`index.html`, one file) |

Page counts match the source slide counts one for one. GitHub renders both PDFs and
CSVs in the browser, so nothing needs cloning to read.

### File names

| Form | Example |
|---|---|
| Lecture deck | `U07_Lecture_Trees_and_Ensembles.pdf` |
| Problem set | `U07_ProblemSet_Trees_and_Ensembles.pdf` |
| Practice data | `U07_Trees_and_Ensembles/data/fml_w7_p1_loans.csv` |

`U07` is unit 7 — the seventh block of material, not the seventh week of term. The
data files keep their original `w7` naming from when the course was written; unit 7
and its data are the same thing.

---

## The four parts

| Part | Units | Topic |
|---|---|---|
| I · Foundations | 1–3 | ML paradigms · bars and CUSUM · triple barrier and meta-labeling |
| II · Core Algorithms | 4–9 | Linear · logistic, KNN, NB · SVM · trees and ensembles · deep learning · unsupervised |
| III · Financial ML in Depth | 10–13 | Purged CV, DSR and PBO · HRP and NCO · NLP, LLMs and RAG · reinforcement learning |
| IV · Frontier and Causality | 14–16 | Causal inference · SHAP and fairness · TFT, GNN and agents · integration |

Anomaly detection runs as its own thread across the algorithms — LOF in unit 5,
OCSVM in unit 6, Isolation Forest in unit 7, the autoencoder in unit 8 — because in
production no single detector is enough.

---

## Sixteen units, fourteen teaching weeks

Week 8 is the midterm and week 16 is the final, so the sixteen units are taught in
fourteen weeks. Two weeks carry two units: **week 5** takes the three simple
classifiers together with the support vector machine, and **week 14** takes
causality and fairness together with the frontier.

The examination papers fix where the line falls — the midterm covers units 1–8 and
the final covers units 9–16 — so the split is even, eight units either side. The
full table and the rejected pairings are in
[`course/curriculum_map.md`](course/curriculum_map.md).

---

## Examinations

Both papers are 40 multiple-choice questions over 90 minutes, 2.5 points each. Every
number in them comes from a worked example in the lectures.

| Paper | Covers | File |
|---|---|---|
| Midterm | Units 1–8 | [`exams/Midterm_Units01-08_40Q.pdf`](exams/Midterm_Units01-08_40Q.pdf) |
| Final | Units 9–16 | [`exams/Final_Units09-16_40Q.pdf`](exams/Final_Units09-16_40Q.pdf) |

**Questions only — the answer keys are not in this repository**, and `.gitignore`
refuses them by name so they cannot be added by accident. The papers still carry the
instruction line telling candidates not to turn to the key; that is how the paper
reads in the examination room.

---

## Practice data

Every problem ships the data it needs. The files are small, synthetic or derived, and
sit beside the deck that uses them:

```
U05_Classification_and_Anomalies/data/
    README_W5.txt
    fml_w5_p2_applicants.csv
    fml_w5_p3_likelihoods.csv
```

No download step, no API key, no vendor account — the numbers are chosen so the
hand-calculation in the problem set and the code you write afterwards agree exactly.

---

## Tooling

Python — pandas, numpy, matplotlib, scikit-learn; XGBoost for the ensembles; PyTorch
for the neural network and autoencoder units.

Prerequisites are deliberately light: pandas and numpy basics, conditional
probability and Bayes, matrix multiplication and eigendecomposition, and returns and
risk. None of it is graded, and the syllabus lists a self-study resource for each.

---

## Licence

Course materials and practice data under [CC BY-NC-SA 4.0](LICENSE). Textbook content
referenced in the slides belongs to its authors and is cited, not reproduced.
