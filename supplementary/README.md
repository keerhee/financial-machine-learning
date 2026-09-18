# Supplementary material

Short, self-contained teaching packages that sit beside the sixteen units — a deck plus
the data and notebook it runs on. They are numbered `SUP01`, `SUP02`, … in the order
they were added, separately from the special sessions `S1`–`S4`.

These are the one place in this repository where material appears in **Korean as well
as English**: each package ships as a pair, `_EN` and `_KR` carrying the same slides
and the same numbers, and the data and notebook come in both languages too.

| # | Package | Slides | Relates to |
|---|---|---|---|
| SUP01 | [Linear Regression on the KOSPI](SUP01_Linear_Regression_KOSPI_EN.pdf) · [한국어](SUP01_Linear_Regression_KOSPI_KR.pdf) | 53 | U04 Linear Models and Regularization · U10 Honest Backtesting |

## SUP01 · Linear Regression on the KOSPI

A one-day regression course built around one data set: 29 Korean macro and market
indicators, monthly from May 2003 to August 2016, with the KOSPI index as the target.

Six sections — least squares (normal equation and gradient descent), evaluation metrics
and where to measure them, the scikit-learn four-step pattern, Ridge / Lasso / ElasticNet,
polynomial features, and a KOSPI case lab. The lab reproduces the original notebook's
R² of 0.95 and then shows why it is an illusion: a shuffled time series, a swapped
`r2_score`, and two collinear bond yields with coefficients of −729 and +852. An honest
2014–2016 hold-out sends every model below the naive benchmark. Two appendix slides list
the corrections made to the original Korean deck.

Files in [`SUP01_Linear_Regression_KOSPI/`](SUP01_Linear_Regression_KOSPI/):

| File | What it is |
|---|---|
| `KOSPI_Index_EN.csv` · `KOSPI_Index_KO.csv` | 160 monthly rows, 29 features + KOSPI (column names in English / Korean) |
| `KOSPI_Data_Dictionary.csv` · `KOSPI_Data_Dictionary_KO.csv` | Each column's original Korean name, English name, group, frequency, description |
| `KOSPI_Prediction_EN.ipynb` · `KOSPI_Prediction_KO.ipynb` | Part A reproduces the original lab (random split); Part B works the three pitfalls and the honest split, then tunes α with `TimeSeriesSplit` |

Open the notebook in Colab —
[English](https://colab.research.google.com/github/keerhee/financial-machine-learning/blob/main/supplementary/SUP01_Linear_Regression_KOSPI/KOSPI_Prediction_EN.ipynb) ·
[한국어](https://colab.research.google.com/github/keerhee/financial-machine-learning/blob/main/supplementary/SUP01_Linear_Regression_KOSPI/KOSPI_Prediction_KO.ipynb)
— and upload the matching `KOSPI_Index_*.csv` when the first cell asks for it.

## File names

`SUP01_Linear_Regression_KOSPI_EN.pdf` — package number, slug, language. The two
languages of one package share a slug, so they sort next to each other; the data and
notebook live in a directory with the same slug.
