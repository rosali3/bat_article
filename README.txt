# Gap Junction Detection Analysis

Analysis pipeline comparing gap junction detections between Wakefulness and Sleep conditions.

## Files

- **`gj_metrics_pipeline.ipynb`** — main pipeline: loads per-image JSON detection files,
  applies filtering (zero-tail exclusion, 3-sigma area-outlier exclusion), aggregates
  results per session and per Z-stack, and generates a text report, a CSV export, and
  summary plots.
- **`plot_generation_script.ipynb`** — generates per-Z-stack plots of detection agreement
  metrics (precision, recall, F1, mean matched IoU) between conditions.

## Output

All plots are saved under `results/`, organized into subfolders:

```
results/
├── detections_summary/    # boxplots of detection counts and areas (per image / per detection)
├── zstack_summary/        # per-Z-stack boxplots: median/sum count, median/sum area
└── detection_agreement/   # per-Z-stack boxplots: precision, recall, F1, mean matched IoU
```

Each plot shows individual data points (jittered) alongside the group median and mean,
and flags statistical outliers using the IQR rule.

## Usage

1. Set the path to the data folder in `MAIN_FOLDER` (in `gj_metrics_pipeline.ipynb`).
2. Set the output folder in `OUTPUT_DIR` (default: `./results`).
3. Run the notebook cells in order.