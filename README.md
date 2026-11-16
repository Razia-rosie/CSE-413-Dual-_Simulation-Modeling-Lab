# CSE-413 Simulation and Modeling Lab

A collection of lab notebooks for the **CSE-413 Simulation and Modeling** course, including a hypothesis-testing project that compares two dengue rapid tests using three statistical techniques: the chi-square test, Monte Carlo simulation and the two-sample t-test.

## Repository structure

```
.
├── README.md
├── requirements.txt
├── .gitignore
├── experiments/
│   └── dengue_fia_vs_ic/
│       ├── Dengue_ChiSquare_MonteCarlo_Ttest.ipynb   # main project notebook
│       └── dengue_FIA_vs_IC_reconstructed.csv        # dataset (808 rows)
├── notebooks/                                         # earlier lab notebooks
│   ├── SIM_Lab1_Razia_1018.ipynb
│   ├── SIM_Lab2_Razia_1018.ipynb
│   ├── SIM_Lab3_Razia_1018.ipynb
│   ├── SIM_Lab04_Razia_1018.ipynb
│   ├── test_5.ipynb
│   └── SIM_Lab_6_Razia_1018.ipynb
└── docs/
    └── audit_notes.md                                 # reorganization and audit notes
```

The notebook and its CSV are kept in the same folder because the notebook loads the file by relative name (`dengue_FIA_vs_IC_reconstructed.csv`).

---

## Dengue project: FIA vs IC rapid test (NS1)

### Overview and objective
**Question:** does the Fluorescent Immunoassay (FIA) detect dengue better than the Immunochromatography (IC) rapid test?

The notebook is based on the published study Ruchusatsawat et al., *Scientific Reports* 2022;12:17299 (404 plasma samples, 158 dengue-confirmed by RT-qPCR and ELISA). Both tests detect the same marker (NS1) in patient plasma against the same reference standard.

### Data
`dengue_FIA_vs_IC_reconstructed.csv` has the columns `Sample_ID, Test_Type, True_Status, Result, Correct` (808 rows: 404 samples for each of FIA and IC).

> **Important data note (stated in the notebook):** the paper publishes only summary counts (FIA detected 125/158, IC detected 121/158). The per-sample rows are **reconstructed** from those counts, so row order and IDs are arbitrary and the two tests are treated as **unpaired** groups.

The notebook also explains why three other candidate CSV files were not used (different marker, mixed sample types, or summary-only). Those files are not part of this repository.

### Hypotheses (alpha = 0.05)
* **H0:** FIA and IC have the same sensitivity.
* **H1:** FIA sensitivity is higher than IC sensitivity.

### Methodology
Only dengue-positive samples are used (sensitivity = detected / truly diseased). Each row is 1 (detected) or 0 (missed).

| Technique | Role | Summary |
|---|---|---|
| Chi-square test | Main test | Observed vs expected counts under H0, with expected counts from the pooled detection rate; df = 1. |
| Monte Carlo simulation | Cross-check 1 | 20,000 simulated studies under H0 (`random.seed(42)`), counting how often chance gives a gap at least as large as the observed one. |
| Two-sample t-test | Cross-check 2 | Pooled-variance t-test on the 0/1 data, plus a 95% confidence interval for the difference. |

### Results
The notebook is stored **without saved outputs**. Running it in a clean environment (numpy 2.0.2, pandas 2.3.3, scipy 1.13.1, matplotlib 3.9.4) gave:

| Quantity | Value |
|---|---|
| FIA sensitivity | 125/158 = 79.11% |
| IC sensitivity | 121/158 = 76.58% |
| Chi-square statistic (df = 1) / critical value | 0.29 / 3.84 |
| Chi-square p-value (two-sided) | 0.5879 |
| Monte Carlo p-value (two-sided / one-sided) | 0.6220 / 0.3125 |
| t-test p-value (two-sided / one-sided) | 0.5893 / 0.2947 |
| 95% CI for the difference in means | [-0.0669, 0.1175] |

**Conclusion given in the notebook:** all three techniques fail to reject H0. FIA's sensitivity is numerically higher by about 2.5 percentage points, but the difference is not statistically significant. Monte Carlo p-values depend on the random seed and number of trials.

The notebook produces three figures when run: observed vs expected frequencies, the Monte Carlo distribution of gaps, and a bar chart of mean detection rates.

### Limitations (from the notebook)
* The rows are reconstructed from published summary counts, so the tests are treated as unpaired.
* Only NS1 sensitivity is analysed.
* A t-test is less natural for 0/1 data than the chi-square test, so it is used only as a cross-check.

---

## Earlier lab notebooks
`notebooks/` holds the earlier lab notebooks (Labs 1, 2, 3, 4, 6 and `test_5`) exactly as originally uploaded. They use numpy, pandas, scipy, matplotlib, seaborn and sympy; see each notebook for its topic.

## Installation
Requires Python 3 and Jupyter.

```bash
git clone https://github.com/Razia-rosie/CSE-413-Dual-_Simulation-Modeling-Lab.git
cd CSE-413-Dual-_Simulation-Modeling-Lab
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Running
Start Jupyter from inside the experiment folder so the CSV is found:

```bash
cd experiments/dengue_fia_vs_ic
jupyter notebook Dengue_ChiSquare_MonteCarlo_Ttest.ipynb
```

Then choose *Run All*. If the CSV is not found (for example on Google Colab), the notebook prompts you to upload it. Earlier labs: `jupyter notebook notebooks/`.

## Academic information
* Course: CSE-413, Simulation and Modeling Lab
* Author: Razia (the notebooks are named with the ID suffix `Razia_1018`)

University, supervisor and semester details are not recorded in the project files and are therefore not stated here.
