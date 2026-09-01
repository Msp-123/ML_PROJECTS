# Cookie Cats A/B Testing

An end-to-end product experimentation analysis evaluating whether moving the first progression gate in the mobile game **Cookie Cats** from level 30 to level 40 improves player engagement and retention.

[View the analysis on Kaggle](https://www.kaggle.com/code/mertkrpehlivan/cookie-cats-a-b-test) · [View the dataset](https://www.kaggle.com/datasets/mursideyarkin/mobile-games-ab-testing-cookie-cats)

## Project Overview

Cookie Cats is a mobile puzzle game in which players encounter progression gates after reaching certain levels. This experiment compares two versions of the game:

| Group | Version | Gate position |
|---|---|---:|
| Control | `gate_30` | Level 30 |
| Treatment | `gate_40` | Level 40 |

The main question is:

> Does moving the gate from level 30 to level 40 improve player activity and 1-day or 7-day retention?

## Dataset

The dataset contains **90,189 unique players** and five variables:

| Variable | Description |
|---|---|
| `userid` | Unique player identifier |
| `version` | Experiment group: `gate_30` or `gate_40` |
| `sum_gamerounds` | Total game rounds played during the first 14 days |
| `retention_1` | Whether the player returned one day after installation |
| `retention_7` | Whether the player returned seven days after installation |

The data contains no missing values, duplicate rows, duplicate user IDs, or negative game-round values.

## Methodology

The analysis includes:

- Data quality and experiment-group checks
- Exploratory analysis of game-round distributions
- Outlier sensitivity analysis
- Absolute and relative retention uplift
- Two-sided two-proportion z-tests at a 5% significance level
- 95% confidence intervals for retention differences
- Bootstrap validation using 10,000 resamples
- Product interpretation and recommendation

The treatment effect is defined as:

`gate_40 retention rate - gate_30 retention rate`

Therefore, a negative difference means that the treatment performed worse than the control.

## Key Results

| Metric | `gate_30` | `gate_40` | Difference | Relative change | Statistical result |
|---|---:|---:|---:|---:|---|
| 1-day retention | 44.82% | 44.23% | -0.59 pp | -1.32% | Not significant, p = 0.0744 |
| 7-day retention | 19.02% | 18.20% | -0.82 pp | -4.31% | Significant, p = 0.0016 |

### Confidence intervals

| Metric | Analytical 95% CI | Bootstrap 95% CI | Bootstrap samples above zero |
|---|---:|---:|---:|
| 1-day retention | [-1.24, 0.06] pp | [-1.25, 0.06] pp | 3.47% |
| 7-day retention | [-1.33, -0.31] pp | [-1.32, -0.31] pp | 0.10% |

The 1-day interval includes zero, so the evidence is insufficient to conclude that the gate change affected short-term retention. The 7-day interval is entirely below zero, providing consistent evidence that moving the gate to level 40 reduced longer-term retention.

## Gameplay Analysis

The game-round distribution is strongly right-skewed and contains one extreme observation of 49,854 rounds in the control group. After excluding this observation for sensitivity analysis, the mean number of rounds is nearly identical:

| Group | Mean rounds | Median rounds |
|---|---:|---:|
| `gate_30` | 51.34 | 17 |
| `gate_40` | 51.30 | 16 |

This suggests that moving the gate did not produce a meaningful improvement in gameplay activity.

## Product Recommendation

**Keep the gate at level 30.**

Moving the gate to level 40:

- Did not meaningfully improve the number of game rounds played
- Did not significantly improve 1-day retention
- Significantly reduced 7-day retention

The gate at level 30 may provide a useful interruption that encourages players to return, while delaying it appears to weaken longer-term engagement.

## Project Structure

```text
cookie-cats-ab-testing/
├── notebooks/
│   └── Cookie_Cats_AB_Testing.ipynb
├── .gitignore
├── README.md
└── requirements.txt
```

## How to Run

Clone the repository and enter the project directory:

```bash
git clone https://github.com/Msp-123/machine-learning-projects.git
cd machine-learning-projects/cookie-cats-ab-testing
```

Create and activate a virtual environment, then install the dependencies:

```bash
python -m venv .venv

# Windows PowerShell
.venv\Scripts\Activate.ps1

pip install -r requirements.txt
```

Download `cookie_cats.csv` from the [Kaggle dataset page](https://www.kaggle.com/datasets/mursideyarkin/mobile-games-ab-testing-cookie-cats), update `local_path` in the notebook's data-loading cell if necessary, and launch the notebook:

```bash
jupyter notebook notebooks/Cookie_Cats_AB_Testing.ipynb
```

Alternatively, run the complete notebook directly on [Kaggle](https://www.kaggle.com/code/mertkrpehlivan/cookie-cats-a-b-test).

## Tools

- Python
- pandas and NumPy
- Matplotlib and Seaborn
- SciPy and statsmodels
- Jupyter Notebook

## Limitations

The dataset is limited to game rounds and retention outcomes. Revenue, in-app purchases, acquisition channels, player segments, and other behavioral events are not available, so the recommendation is based on engagement and retention rather than overall business value.

## Author

**Mert Kırpehlivan**  
[GitHub](https://github.com/Msp-123) · [Kaggle](https://www.kaggle.com/mertkrpehlivan)
