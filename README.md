# Wavelet-Enhanced Hybrid Deep Learning for Battery SOH

**Publication:** Intelligent health state diagnosis of lithium-ion batteries for electric vehicles using wavelet-enhanced hybrid deep learning integrated with an attention mechanism  
**Journal:** Clean Energy (2025)  
**DOI:** https://doi.org/10.1093/ce/zkaf019

## Research method

The method combines wavelet-oriented feature representation, convolutional and bidirectional recurrent layers, and an attention mechanism for sequence-level SOH regression. The pipeline operates on discharge-cycle measurements and keeps the evaluation chronology separate from the fitting interval.

The project covers data preparation, model fitting, chronological validation, and prediction diagnostics. Configuration parameters are defined in [config.json](config.json), while the main training entry point is [train.py](train.py).

## Battery data

Cycle-level experimental records are included for **12 NASA PCoE cells** and **four CALCE CS2 cells**. The available data, column definitions and provenance hashes are documented in [data/README.md](data/README.md) and [data/processed/manifest.json](data/processed/manifest.json).

## Train

After installing dependencies, run the bundled NASA B0005 experiment with no
extra arguments:

```bash
python -m pip install -r requirements.txt
python train.py
```

The requirements use CPU-only PyTorch wheels, so no GPU or CUDA toolkit is
needed for the documented run.

This uses the six measured discharge-sensor features, the defaults in
`config.json` (8 epochs, seed 42), a chronological within-cell split, and writes
the checkpoint, training log, predictions and metrics to `outputs/latest/`.
To train on another CSV, pass `--csv PATH`; specify its target and sensor
features with `--target` and `--features`. `python train.py --help` lists all
options.

For a quick synthetic software check (not a scientific experiment):

```bash
pytest -q
python train.py --smoke --epochs 2 --out outputs/smoke
```

## Relationship to the paper

The default model implements a fixed Morlet filter bank, CNN, BiLSTM and
additive attention. The default configuration disables clustering, optimizer
search and residual calibration. The one-cell run is a runnable baseline, not
a replication of the paper's cross-cell experiments. Exact agreement with all
paper equations, feature-selection steps, hyperparameters and reported results
has not been verified; see [REPRODUCIBILITY.md](REPRODUCIBILITY.md) before
interpreting any metrics. The data sources and split limitations are described
in [data/README.md](data/README.md) and [docs/REAL_DATA_SETUP.md](docs/REAL_DATA_SETUP.md).
