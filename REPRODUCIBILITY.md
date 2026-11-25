# Reproducibility and evaluation notes

**Publication:** Intelligent health state diagnosis of lithium-ion batteries for electric vehicles using wavelet-enhanced hybrid deep learning integrated with an attention mechanism (Clean Energy (2025))  
**DOI:** https://doi.org/10.1093/ce/zkaf019

## Implementation scope

The default `cnn_wavelet_bilstm` implementation combines a fixed Morlet
filterbank, convolutional layers, a bidirectional LSTM and additive attention
for sequence-level SOH regression. Its default configuration sets
`n_clusters: 0`, `optimizer: "none"` and `residual: "none"`; optional clustering,
search and residual modules therefore are not part of an ordinary run.

This repository does not contain the article's full text, original source code
or a complete experiment-parameter table. Consequently, the component-level
similarity suggested by the title is not evidence that the implementation
matches every equation, preprocessing step, feature selection, optimizer,
partition or reported result. Exact paper reproduction remains unverified;
never label the metrics from `train.py` as the published results.

## Data provenance

- NASA PCoE: 12 cell-level CSV files under `data/processed/nasa/`.
- CALCE CS2: four cell-level CSV files under `data/processed/calce/`.
- Source file checksums, record counts and conversion provenance: `data/processed/manifest.json`.
- Source MATLAB and Excel time-series archives are maintained separately; the committed CSVs contain cycle-level aggregates.

## Evaluation protocol

With no `--csv`, `train.py` uses the bundled NASA B0005 cycle-level CSV and six
sensor features. It performs a chronological split within that single cell.
This makes the project immediately runnable, but it is not a substitute for
the held-out-cell experiments described in the publication. For a cross-cell
study, define and document explicit training, validation and test cell IDs;
do not concatenate cell files and allow sequence windows to cross cell
boundaries.

The SOH label is capacity-derived. For leakage-aware results, same-cycle capacity or any direct SOH transformation should not be used as a predictor. Verify the treatment of historical target values, outlier removal, normalization statistics, and battery-specific nominal capacities before comparing experiments.

## Results and remaining checks

Automated tests confirm execution of individual software components. Reproduction of the published numerical results has not yet been established. Further checks include architecture hyperparameters, source features, train/validation/test partitions, random seeds, baseline implementations, and uncertainty across repeated runs.
