# Decoding Match Success Across Tournament Phases

## Explainable Machine Learning Analysis of the 2026 FIFA World Cup

This repository contains reproducibility materials for the study:

**Decoding Match Success Across Tournament Phases: An Explainable Machine Learning Analysis of Performance Indicators in the 2026 FIFA World Cup.**

## Study overview

The study examines match success in the 2026 FIFA World Cup using explainable machine-learning methods.

The analytical dataset contains 208 team-match observations from 104 matches.

The binary outcome is defined as:

- Win = 1
- Non-win = 0

Matches decided by penalty shootouts are classified according to the match result before the shootout. Therefore, when a match is level before the penalty shootout, both teams are coded as non-wins.

## Predictors

The final analysis uses 14 predictors:

1. FIFA ranking difference
2. Attempts on target
3. Corner kicks
4. Crosses
5. Ball possession
6. Completed passes
7. Completed line breaks
8. Defensive pressures
9. Forced turnovers
10. Second balls
11. Saves
12. Save percentage
13. Distance covered
14. Zone 4 low-speed sprinting

FIFA ranking difference is defined as:

**Opponent FIFA ranking position - focal-team FIFA ranking position**

A positive value therefore indicates that the focal team was better ranked than its opponent.

## Primary analysis

The primary analysis normalizes 11 exposure-dependent performance indicators to a 90-minute basis.

The following variables are not exposure-normalized:

- FIFA ranking difference
- Ball possession
- Save percentage

Three machine-learning algorithms are evaluated:

- Elastic Net logistic regression
- Random Forest
- XGBoost

Model evaluation uses nested stratified group cross-validation, with Match_ID as the grouping unit. This prevents the two team observations from the same match from being split between training and test sets.

The outer cross-validation uses five folds. Hyperparameter tuning within each outer training set uses five inner folds.

The random seed is 42.

## Explainability analysis

XGBoost is retained as the focal model for explainability.

Out-of-fold SHAP values are generated only for observations held out in each outer test fold.

Positive SHAP values shift the model output toward the win class, whereas negative SHAP values shift the model output toward the non-win class.

In SHAP beeswarm figures, color represents the predictor value and does not represent match outcome.

Global feature importance is summarized using mean absolute SHAP values.

## Tournament-phase analysis

Model performance and SHAP importance are examined separately for the group stage and knockout stage.

The SHAP phase difference is defined as:

**Knockout-stage mean absolute SHAP - Group-stage mean absolute SHAP**

Uncertainty is estimated using 5,000 match-level bootstrap resamples, preserving the paired team observations belonging to each match.

## Sensitivity analysis

A sensitivity analysis repeats the complete machine-learning pipeline using raw full-match totals rather than per-90 normalized values for the exposure-dependent predictors.

This evaluates the robustness of the main predictive and explainability findings to the treatment of match exposure.

## Repository structure

- `data/` — data availability information and permitted analytical data files.
- `notebooks/` — final reproducible analysis notebooks.
- `results/` — numerical results and reproducibility tables.
- `figures/` — final figures generated from the analyses.
- `requirements.txt` — Python package versions used for the analysis.

## Software environment

The analyses were conducted using Python 3.14.6.

Core packages include:

- NumPy 2.4.6
- pandas 3.0.3
- SciPy 1.18.0
- scikit-learn 1.9.0
- XGBoost 3.4.1
- SHAP 0.52.0
- Matplotlib 3.11.0

Complete package information is provided in `requirements.txt`.

## Reproducibility

The analyses use a fixed random seed of 42.

This repository provides the analysis code and supporting materials required to reproduce the reported analytical workflow, subject to the data-availability conditions described below.

The analytical source datasets are not redistributed because redistribution rights for the underlying FIFA-derived data have not been established; data requirements and expected structure are documented in `data/README.md`.

## Citation

Citation information will be added when publication details become available.

## License

The original analysis code and repository documentation produced for this
study are released under the MIT License. See `LICENSE` for the full license
text.

The MIT License applies only to the original code and documentation produced
for this study. It does **not** grant rights to FIFA-owned or third-party
data, match reports, trademarks, logos, or other proprietary content.

## Data availability

The match-performance data used in this study were manually compiled from
publicly accessible FIFA Training Centre resources and FIFA match reports
during the FIFA World Cup 2026.

Because the underlying information originates from FIFA and redistribution
rights for the compiled analytical datasets have not been established, the
analytical source datasets are not redistributed through this repository.

The repository provides the analysis notebooks, software environment,
derived model outputs, supporting tables, and figures documenting the
analytical workflow. See `data/README.md` for the expected dataset structure
and processing details.

