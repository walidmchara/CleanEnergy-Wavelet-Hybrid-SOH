# Battery-aging datasets

The experiments use the NASA PCoE and CALCE CS2 battery-aging collections. Cycle-level data prepared from the source archives are versioned in this repository.

## Dataset inventory

| Source | Cells | Location |
| --- | --- | --- |
| NASA PCoE | B0005, B0006, B0007, B0018, B0029, B0030, B0031, B0032, B0053, B0054, B0055, B0056 | [processed/nasa/](processed/nasa/) |
| CALCE CS2 | CS2_35, CS2_36, CS2_37, CS2_38 | [processed/calce/](processed/calce/) |

[processed/manifest.json](processed/manifest.json) records dataset provenance and SHA-256 digests. Each CSV summarizes discharge-cycle electrical measurements and capacity-related indicators; the original sample-level files are maintained separately.

## Experimental use

```bash
python train.py --csv data/processed/nasa/B0005.csv --target target --time-col time --features voltage_mean,voltage_std,current_mean,current_std,temperature_mean,discharge_duration_s --epochs 2 --out outputs/nasa_trial
```

For capacity-based SOH experiments, exclude the capacity-derived label at the same prediction cycle from the input features. A chronological split within one battery does not replace a proper leave-one-cell-out study. The data preparation and column definitions are detailed in [../docs/REAL_DATA_SETUP.md](../docs/REAL_DATA_SETUP.md).

Sources: [NASA PCoE](https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/); [CALCE Battery Research Data](https://calce.umd.edu/data).
