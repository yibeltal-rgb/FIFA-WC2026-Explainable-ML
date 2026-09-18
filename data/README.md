# Data

## Data availability

The analytical datasets used in this study are not included in this repository at this stage.

Before public redistribution, the licensing and redistribution conditions of the underlying FIFA-derived data should be confirmed.

The analysis notebooks expect the required input files to be placed in this directory.

## Required files

### 1. Primary per-90 dataset

`FIFA_WC2026_Analysis_Ready_Per90_Corrected.xlsx`

Expected characteristics:

- 208 team-match observations
- 104 matches
- 51 columns
- Win_Binary: 80 wins and 128 non-wins
- 8 team-match observations from matches decided by penalty shootouts
- penalty-shootout matches are coded according to the match result before the shootout; both teams are non-wins when level before the shootout

This dataset is used for the primary analysis.

Eleven exposure-dependent performance indicators are represented per 90 minutes.

The per-90 exposure factor is:

`Exposure_Factor = 90 / Match_Duration`

The following predictors remain unchanged rather than being normalized per 90 minutes:

- FIFA ranking difference
- Ball possession
- Save percentage

### 2. Raw-total sensitivity source dataset

`FIFA_WC2026_Analysis_Ready_Corrected.xlsx`

Expected characteristics:

- 208 team-match observations
- 104 matches
- 38 columns
- Win_Binary: 80 wins and 128 non-wins
- 8 team-match observations from matches decided by penalty shootouts

This file is used as the starting dataset for the raw-total sensitivity analysis.

## Documented M14 correction

The raw-total sensitivity notebook transparently corrects one verified data-entry discrepancy for match M14, Cabo Verde vs Spain:

- Completed_Passes: 272 -> 306
- Completed_Line_Breaks: 306 -> 57

The correction is performed within the sensitivity-analysis notebook and is retained in the workflow for auditability.

## Outcome definition

The binary outcome is:

- Win = 1
- Non-win = 0

Penalty-shootout results are not used to redefine the match outcome. If a match is level before the shootout, both team observations are coded as non-wins.

## FIFA ranking difference

Ranking difference is calculated as:

`Opponent FIFA ranking position - focal-team FIFA ranking position`

Therefore:

- Positive values indicate that the focal team is better ranked.
- Negative values indicate that the focal team is worse ranked.

## Public data release

A public-data availability statement should be finalized only after the redistribution conditions of the underlying source data have been verified.