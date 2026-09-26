# Supplementary material

Short, self-contained teaching packages that sit beside the sixteen units — a deck plus
the data and notebook it runs on. They are numbered `SUP01`, `SUP02`, … in the order
they were added, separately from the special sessions `S1`–`S4`.

These are the one place in this repository where material appears in **Korean as well
as English**: each package ships as a pair, `_EN` and `_KR`, with the same numbers, and
the data and notebook come in both languages too.

| # | Package | Slides | Relates to |
|---|---|---|---|
| SUP01 | [Linear Regression on the KOSPI](SUP01_Linear_Regression_KOSPI_EN.pdf) · [한국어](SUP01_Linear_Regression_KOSPI_KR.pdf) | 51 · 53 | U04 Linear Models and Regularization |
| SUP02 | [Logistic Regression on the KOSPI](SUP02_Logistic_Regression_KOSPI_EN.pdf) · [한국어](SUP02_Logistic_Regression_KOSPI_KR.pdf) | 65 · 65 | U05 Classification and Anomaly Detection |

## SUP01 · Linear Regression on the KOSPI

A one-day regression course built around one data set: 29 Korean macro and market
indicators with the KOSPI index as the target, 160 rows (May 2003 – August 2016). Each row
is treated as an independent observation, so the train/test split is a random shuffle.

Six sections — least squares (normal equation and gradient descent), evaluation metrics
and where to measure them, the scikit-learn four-step pattern, Ridge / Lasso / ElasticNet,
polynomial features, and a KOSPI case lab.

The two languages are no longer identical. The **English deck (51 slides)** is the class
edition: its case lab walks the Colab notebook cell by cell — loading, the random split and
the scaler, OLS in four steps, Ridge and Lasso, polynomial features, and one helper that
compares all six models — and reproduces the notebook's R² of 0.95. A narrated video of the
English deck is on YouTube: https://youtu.be/cuqP8qWk63M. The **Korean deck (53 slides)**
keeps the original case lab with its additional evaluation slides, and two appendix slides
list the corrections made to the original Korean deck.

Files in [`SUP01_Linear_Regression_KOSPI/`](SUP01_Linear_Regression_KOSPI/):

| File | What it is |
|---|---|
| `KOSPI_Index_EN.csv` · `KOSPI_Index_KO.csv` | 160 monthly rows, 29 features + KOSPI (column names in English / Korean) |
| `KOSPI_Data_Dictionary.csv` · `KOSPI_Data_Dictionary_KO.csv` | Each column's original Korean name, English name, group, frequency, description |
| `KOSPI_Prediction_EN.ipynb` · `KOSPI_Prediction_KO.ipynb` | The lab in eight sections (§0–§8): load, random 80/20 split and scaling, OLS, Ridge, Lasso, polynomial features, and one table comparing all six models — the English slides follow it cell by cell |

Open the notebook in Colab —
[English](https://colab.research.google.com/github/keerhee/financial-machine-learning/blob/main/supplementary/SUP01_Linear_Regression_KOSPI/KOSPI_Prediction_EN.ipynb) ·
[한국어](https://colab.research.google.com/github/keerhee/financial-machine-learning/blob/main/supplementary/SUP01_Linear_Regression_KOSPI/KOSPI_Prediction_KO.ipynb)
— and upload the matching `KOSPI_Index_*.csv` when the first cell asks for it.

## SUP02 · Logistic Regression on the KOSPI

The classification sequel to SUP01, on the same data. Five sections of theory — the
logistic model (sigmoid, odds and log-odds, maximum likelihood, regularization with `C`),
the basic setup that turns probabilities into calls, the confusion matrix and its metrics
(precision, recall, F1, Fβ, sensitivity, specificity), the ROC curve, and AUC with
precision–recall curves — then two labs: three iris species, and the KOSPI.

The KOSPI lab labels each month 1 if the index rises the next month and 0 otherwise. Only
the label looks ahead; the features are that month's 29 indicators and never another
month's, so each row is an independent observation and the split is a random shuffle.
The original notebook's 0.55 accuracy is set against three checks: an always-up baseline,
unscaled L1 regularization, and a single random split. Repeating the 75/25 split 100 times
gives a mean accuracy of 0.545 against 0.570 for always-up, and the model beats that
baseline in only 40 splits — monthly direction is close to a coin flip.

Both decks have 65 slides with the same numbers; two appendix slides list the corrections
made to the original Korean material. A narrated video of the English deck — the Week 6
make-up class — is on YouTube: https://youtu.be/NG0g3SJlDr0.

Files in [`SUP02_Logistic_Regression_KOSPI/`](SUP02_Logistic_Regression_KOSPI/):

| File | What it is |
|---|---|
| `KOSPI_Index_EN.csv` · `KOSPI_Index_KO.csv` | The SUP01 data, unchanged — 160 monthly rows, 29 features + KOSPI |
| `KOSPI_Data_Dictionary.csv` · `KOSPI_Data_Dictionary_KO.csv` | Each column's original Korean name, English name, group, frequency, description |
| `KOSPI_Logit_EN.ipynb` · `KOSPI_Logit_KO.ipynb` | The lab in three parts: A, the original lab (target, L1 logistic regression, accuracy); B, a fuller evaluation (confusion matrix and metrics, baseline, scaling, 100 random splits, thresholds); C, the lecture examples (the 8-mouse ROC, three iris species) |

Open the notebook in Colab —
[English](https://colab.research.google.com/github/keerhee/financial-machine-learning/blob/main/supplementary/SUP02_Logistic_Regression_KOSPI/KOSPI_Logit_EN.ipynb) ·
[한국어](https://colab.research.google.com/github/keerhee/financial-machine-learning/blob/main/supplementary/SUP02_Logistic_Regression_KOSPI/KOSPI_Logit_KO.ipynb)
— and upload the matching `KOSPI_Index_*.csv` when the first cell asks for it.

## File names

`SUP01_Linear_Regression_KOSPI_EN.pdf` — package number, slug, language. The two
languages of one package share a slug, so they sort next to each other; the data and
notebook live in a directory with the same slug.
