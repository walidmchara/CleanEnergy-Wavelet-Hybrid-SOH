# Reproducibility and evaluation notes

**Publication:** Intelligent health state diagnosis of lithium-ion batteries for electric vehicles using wavelet-enhanced hybrid deep learning integrated with an attention mechanism (Clean Energy (2025))  
**DOI:** https://doi.org/10.1093/ce/zkaf019

## Implementation scope

The method combines wavelet-oriented feature representation, convolutional and bidirectional recurrent layers, and an attention mechanism for sequence-level SOH regression. The pipeline operates on discharge-cycle measurements and keeps the evaluation chronology separate from the fitting interval.

The implementation exposes the hybrid neural-network components. Confirmation of all feature-selection steps, any clustering stages, and the article's complete experiment configuration remains part of the reproducibility review.

## Data provenance

- NASA PCoE: 12 cell-level CSV files under `data/processed/nasa/`.
- CALCE CS2: four cell-level CSV files under `data/processed/calce/`.
- Source file checksums, record counts and conversion provenance: `data/processed/manifest.json`.
- Source MATLAB and Excel time-series archives are maintained separately; the committed CSVs contain cycle-level aggregates.

## Evaluation protocol

The default `train.py` command performs a chronological split within a single CSV. This is useful for checking preprocessing, training and evaluation, but it is not a substitute for the held-out-cell experiments described in the publication.

The SOH label is capacity-derived. For leakage-aware results, same-cycle capacity or any direct SOH transformation should not be used as a predictor. Verify the treatment of historical target values, outlier removal, normalization statistics, and battery-specific nominal capacities before comparing experiments.

## Results and remaining checks

Automated tests confirm execution of individual software components. Reproduction of the published numerical results has not yet been established. Further checks include architecture hyperparameters, source features, train/validation/test partitions, random seeds, baseline implementations, and uncertainty across repeated runs.
