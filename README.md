# Financial Machine Learning

Yonsei University · for 3rd- and 4th-year undergraduates, beginners welcome · 16 units

**Browse and download → https://keerhee.github.io/financial-machine-learning/**

Sixteen units, four optional [special sessions](#special-sessions) beyond them, and a
[supplementary package](#supplementary-material) on regression with KOSPI data. The sessions:
[S1](special_sessions/S1_Recommender_Systems.pdf) and
[S2](special_sessions/S2_Recommender_Systems_Deep_Learning.pdf) on recommenders,
[S3](special_sessions/S3_AI_Native_Asset_Manager.pdf) and
[S4](special_sessions/S4_AI_Native_Asset_Manager_LangGraph.pdf) on the AI-native firm.

From what machine learning is, through the algorithms, to the parts that only matter
in finance: bars and the CUSUM filter instead of the calendar, the triple barrier
instead of "will it go up tomorrow", purged cross-validation instead of a naive
backtest, and a Deflated Sharpe Ratio to tell you when the result was luck.

Built on Hull's *Machine Learning in Business*, López de Prado's *Advances in
Financial Machine Learning*, and *Causal Factor Investing* — and carried through
three industrial applications: product recommendation, fraud detection, and an AI
chatbot.

**57 PDFs · 1,465 slides · 41 practice data files.** For each of the sixteen units a
primer, a lecture deck and a problem set; plus the syllabus, both examination papers,
four special sessions, one supplementary package in English and Korean, and the
companion Colab notebook the labs run from. **Only
PDFs, CSVs, Markdown and the notebook are tracked** — the editable PPTX and DOCX
sources are excluded by `.gitignore`.

---

## Layout

| Path | Contents |
|---|---|
| [`U01_ML_and_the_Finance_Problem/`](U01_ML_and_the_Finance_Problem/) … [`U16_Integration_and_Capstone/`](U16_Integration_and_Capstone/) | Per unit: the primer, the lecture deck, the problem set, and a `data/` directory with the CSVs its three problems use. Each has a `README` naming the special sessions it leads to |
| [`course/`](course/) | Syllabus, the [curriculum map](course/curriculum_map.md), and the [data setup notebook](course/FML_Data_Setup_Guide.ipynb) the labs use |
| [`special_sessions/`](special_sessions/) | Four optional sessions outside the sixteen units, each a deck and a companion note |
| [`supplementary/`](supplementary/) | Supplementary packages beside the units — a deck with its data and notebook, in English and Korean |
| [`exams/`](exams/) | Midterm and final papers — questions only |
| [`site/`](site/) | The GitHub Pages listing page (`index.html`, one file) |

Page counts match the source slide counts one for one. GitHub renders both PDFs and
CSVs in the browser, so nothing needs cloning to read.

### File names

| Form | Example |
|---|---|
| Primer | `U07_Primer_Trees_and_Ensembles.pdf` |
| Lecture deck | `U07_Lecture_Trees_and_Ensembles.pdf` |
| Problem set | `U07_ProblemSet_Trees_and_Ensembles.pdf` |
| Practice data | `U07_Trees_and_Ensembles/data/fml_w7_p1_loans.csv` |
| Special session | `special_sessions/S3_AI_Native_Asset_Manager.pdf` |
| Supplementary package | `supplementary/SUP01_Linear_Regression_KOSPI_EN.pdf` (`_KR` for Korean) |

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

## Primers — watch before the lecture

Every unit opens with a seventeen-slide primer that assumes nothing. It is where the
arithmetic goes, so the lecture does not have to stop for it: what a dot product is
before the support vector machine, what a centroid is before k-means, what
discounting is before reinforcement learning.

| Unit | Primer | Unit | Primer |
|---|---|---|---|
| 1 | What a Model Is | 9 | No Answer Key This Time |
| 2 | How Data Becomes a Bar | 10 | How to Fool Yourself |
| 3 | What Are We Predicting? | 11 | Why Two Is Safer Than One |
| 4 | The Straight Line | 12 | Turning Words Into Numbers |
| 5 | From a Number to a Verdict | 13 | Learning by Doing |
| 6 | What Makes a Line Safe | 14 | Correlation Is Not Enough |
| 7 | Asking the Right Question | 15 | Attention and Neighbours |
| 8 | One Neuron at a Time | 16 | The Whole Pipeline |

Twenty minutes each. If none of it is new, treat it as revision and skip to the
lecture.

---

## Special sessions

Four optional sessions that sit outside the sixteen units. Each is a deck with a
companion note in Markdown, so it reads on GitHub without downloading anything.

| # | Session | Slides | What it covers |
|---|---|---|---|
| S1 | [Recommender Systems](special_sessions/S1_Recommender_Systems.pdf) | 23 | The third running app of the course. Content-based and collaborative filtering, matrix factorization — built from cosine similarity (unit 12) and hidden factors (unit 9). |
| S2 | [Recommender Systems · Part 2](special_sessions/S2_Recommender_Systems_Deep_Learning.pdf) | 30 | Deep-learning recommenders, from factorization machines as the bridge up to graph- and language-based models. |
| S3 | [The AI-Native Asset Manager](special_sessions/S3_AI_Native_Asset_Manager.pdf) | 26 | The capstone view: the investment process as a team of cooperating agents — analysts, traders, risk — with humans overseeing. Pulls units 10–15 together. |
| S4 | [AI-Native Asset Manager · Part 2](special_sessions/S4_AI_Native_Asset_Manager_LangGraph.pdf) | 28 | The implementation half — building that agent firm in LangGraph as an explicit state machine, with checkpointing and human-in-the-loop. |

Each unit's `README` points forward to the sessions that pick it up: unit 9 and unit 12
lead to S1, unit 8 and unit 15 to S2, units 10, 11, 14 and 15 to S3, and units 12, 13
and 15 to S4.

S1→S2 and S3→S4 are pairs; the second of each assumes the first. Notes:
[S1](special_sessions/S1_Recommender_Systems.md) ·
[S2](special_sessions/S2_Recommender_Systems_Deep_Learning.md) ·
[S3](special_sessions/S3_AI_Native_Asset_Manager.md) ·
[S4](special_sessions/S4_AI_Native_Asset_Manager_LangGraph.md)

---

## Supplementary material

Beside the units and the special sessions, self-contained packages that a single lab
can run on: a deck, its data, and a notebook. Unlike the rest of the repository they
ship in **Korean as well as English**.

| # | Package | Slides | What it covers |
|---|---|---|---|
| SUP01 | [Linear Regression on the KOSPI](supplementary/SUP01_Linear_Regression_KOSPI_EN.pdf) · [한국어](supplementary/SUP01_Linear_Regression_KOSPI_KR.pdf) | 51 · 53 | Least squares, gradient descent, metrics, Ridge / Lasso / ElasticNet and polynomial features — then a KOSPI lab (29 indicators, 160 months) that walks the Colab notebook cell by cell and reproduces its 0.95 R². The Korean deck and the notebook go on to show why an honest time split destroys it. Data and notebook in [`supplementary/SUP01_Linear_Regression_KOSPI/`](supplementary/SUP01_Linear_Regression_KOSPI/). Pairs with unit 4 and unit 10. |

Details in [`supplementary/README.md`](supplementary/README.md).

---

## The lab notebook

Twelve of the sixteen lecture decks send you to the same companion notebook, so it
lives once in `course/` rather than inside any one unit:

**[`course/FML_Data_Setup_Guide.ipynb`](course/FML_Data_Setup_Guide.ipynb)** —
[open it in Colab](https://colab.research.google.com/github/keerhee/financial-machine-learning/blob/main/course/FML_Data_Setup_Guide.ipynb)

Run section 0 once, then jump to the section for the unit you are on. Section 10 is a
map from lab to section:

| Unit | Lab topic | Run section |
|---|---|---|
| 1 | Returns and normality; the overfitting demo | 2 |
| 2 | Dollar bars; CUSUM events | 3 (a) |
| 3 | Triple-barrier labeling | 3 (b) |
| 4 | Linear models; index tracking | 3 (b) |
| 5–8 | Fraud and default classification | 4, or 5 offline |
| 9 | PCA, denoising, clustering | 3 (b) |
| 10 | Leakage and multiple testing | 2 |
| 11 | HRP weights; comparing portfolios | 3 (b) |
| 12 | Similar sentences; a tiny RAG | 6 |
| 13 | Q-learning; all-at-once vs sliced execution | 7 |
| 14 | SHAP-style explanation; fairness across groups | 5 |
| 15 | Attention forecast; a graph update | 8 |
| 16 | The capstone pipeline | 9 |
| any | No internet available | 5 — offline fallback |

Prices come from `yfinance` (free, no signup); the fraud and default sets come from
Kaggle; and section 5 simulates every one of them if both are blocked. Units 12, 13,
15 and 16 need no download at all — their data is a few sentences or a few arrays,
built in the notebook. Nothing needs a paid account.

Sections 0 to 5 keep the numbers the lecture decks cite, so a deck that says "run
§3 (b)" still means the multi-stock panel.

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
