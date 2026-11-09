# Wavelet-Enhanced Hybrid Deep Learning for Battery SOH

**Publication:** Intelligent health state diagnosis of lithium-ion batteries for electric vehicles using wavelet-enhanced hybrid deep learning integrated with an attention mechanism  
**Journal:** Clean Energy (2025)  
**DOI:** https://doi.org/10.1093/ce/zkaf019

## Research method

The method combines wavelet-oriented feature representation, convolutional and bidirectional recurrent layers, and an attention mechanism for sequence-level SOH regression. The pipeline operates on discharge-cycle measurements and keeps the evaluation chronology separate from the fitting interval.

The project covers data preparation, model fitting, chronological validation, and prediction diagnostics. Configuration parameters are defined in [config.json](config.json), while the main training entry point is [train.py](train.py).

## Battery data

Cycle-level experimental records are included for **12 NASA PCoE cells** and **four CALCE CS2 cells**. The available data, column definitions and provenance hashes are documented in [data/README.md](data/README.md) and [data/processed/manifest.json](data/processed/manifest.json).

The training command below runs against an existing NASA dataset:

```bash
pip install -r requirements.txt
python train.py --csv data/processed/nasa/B0005.csv --target target --time-col time --features voltage_mean,voltage_std,current_mean,current_std,temperature_mean,discharge_duration_s --epochs 2 --out outputs/nasa_trial
```

For a quick software check:

```bash
pytest -q
python train.py --smoke --epochs 2 --out outputs/smoke
```

Results are written under `outputs/` as model checkpoints, epoch-level training records, holdout predictions and evaluation metrics.

## Experimental validity

The implementation exposes the hybrid neural-network components. Confirmation of all feature-selection steps, any clustering stages, and the article's complete experiment configuration remains part of the reproducibility review.

The one-cell command demonstrates data compatibility; cross-battery results must use explicitly separated training and test cells. Reported paper metrics are not implied by a successful execution. Full notes on data provenance, split definitions and known limitations are recorded in [REPRODUCIBILITY.md](REPRODUCIBILITY.md) and [docs/REAL_DATA_SETUP.md](docs/REAL_DATA_SETUP.md).
