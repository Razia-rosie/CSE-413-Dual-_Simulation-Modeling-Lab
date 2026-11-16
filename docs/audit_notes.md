# Audit and reorganization notes

## What was audited
* Supplied folder: `Dengue_ChiSquare_MonteCarlo_Ttest.ipynb` and `dengue_FIA_vs_IC_reconstructed.csv` (no hidden files, no nested folders, no Git history).
* Both files were byte-identical to the copies already on `main` of the GitHub repository. Nothing new needed uploading, so the work was organizing and documenting.
* The repository also held five earlier lab notebooks and `test_5.ipynb`; these were preserved.

## Changes made (all `git mv` renames, so history is kept; no file contents were edited)
* Dengue notebook + CSV moved to `experiments/dengue_fia_vs_ic/` (kept together because the notebook reads the CSV by relative path).
* Other notebooks moved to `notebooks/`.
* Added `README.md`, `requirements.txt`, `.gitignore`, and this file.

## Observations (original files not changed)
1. The dengue notebook has no saved outputs, so there are no stored graphs or result tables. None were fabricated.
2. Cell 4 imports `google.colab` as a fallback when the CSV is missing; this fails outside Colab if the CSV is not present.
3. The notebook text mentions class notebooks ("Day 3/4/6/7") that are not in this repository.
4. The three other CSV files the notebook discusses are not in the repository.
5. The bar-chart error bars use `fmt='k_'`; it ran without error with matplotlib 3.9.4.
6. Executed output matches the figures quoted in the notebook's own conclusion (chi-square p about 0.59, Monte Carlo one-sided p about 0.31, t-test one-sided p about 0.29).
7. The earlier lab notebooks were not executed or reviewed in detail.
8. A search for keys, passwords and tokens in the notebooks found none.
