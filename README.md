# Gap Junction Detection Analysis

## Abstract

This repository contains a reproducible analysis pipeline for comparing gap-junction detections under awake and sleep conditions. The workflow integrates detection data from multiple sessions and Z-stacks, applies quality-control filtering, aggregates measurements at the session and stack levels, and generates quantitative summaries suitable for scientific reporting.

## Study objective

The analysis aims to quantify and compare gap-junction detection patterns between two experimental conditions: wakefulness and sleep. The primary focus is on evaluating whether detection counts, object sizes, and agreement metrics differ systematically across conditions and across imaging depths.

## Scientific context

The study is framed around the hypothesis that physiological state may be associated with measurable differences in detected gap-junction structures. By comparing detection outcomes across conditions, the analysis provides a quantitative basis for assessing reproducibility, consistency, and potential biological relevance.

## Data and experimental design

The dataset is organized by condition and session, with separate folders for raw imaging data and detection outputs. Each session contains multiple image stacks, and the analysis is performed at both the image level and the aggregated session/Z-stack level.

Input data are expected in the following structure:

```text
data/
├── awake_1/ ... awake_6/
├── sleep_1/ ... sleep_4/
└── ...
```

Each condition folder contains:

- `Raw/` — original imaging data,
- `Detection/` — per-image JSON detection files,
- `asset_metadata.json` — metadata describing the acquisition context.

## Methods summary

The analysis pipeline proceeds in four stages:

1. Detection loading
   - Per-image JSON files are loaded from the detection folders.

2. Filtering and quality control
   - Detections are screened using predefined criteria, including exclusion of zero-tail detections and removal of area-based outliers using a 3-sigma rule.

3. Aggregation
   - Measurements are summarized at the image, session, and Z-stack levels.

4. Quantitative evaluation
   - Agreement metrics such as precision, recall, F1 score, and mean matched IoU are computed and visualized.

## Quantitative outputs

The pipeline produces both tabular and graphical outputs, including:

- detection counts and object areas,
- session-level and Z-stack-level summaries,
- agreement statistics between conditions,
- boxplots with jittered observations, median and mean summaries, and outlier annotations.

Outputs are written to:

```text
results/
├── detections_summary/
├── zstack_summary/
└── detection_agreement/
```

## Repository contents

- `gj_metrics_pipeline.ipynb` — main analysis workflow for loading detections, filtering data, aggregating results, and exporting summaries.
- `plot_generation_script.ipynb` — plotting workflow for agreement metrics and Z-stack-level visualizations.
- `data/` — input data organized by biological condition and acquisition session.
- `results/` — generated plots and summary tables.

## Reproducibility

To ensure reproducibility, the analysis should be run with a consistent directory structure and documented parameter settings. The notebook workflow is intended to be transparent and easy to adapt for future datasets or revised filtering thresholds.

## Manuscript-ready framing

A scientific article based on this workflow can be organized around the following sections:

- Abstract: state the aim, dataset, method, and main conclusion.
- Introduction: motivate the comparison between awake and sleep conditions.
- Materials and Methods: describe the dataset, detection pipeline, filtering rules, and evaluation metrics.
- Results: report the quantitative findings with figures and summary statistics.
- Discussion: interpret the biological and technical significance of the results.
- Conclusion: highlight the main takeaway and potential implications.

## Usage

1. Set the data root in `MAIN_FOLDER` in `gj_metrics_pipeline.ipynb`.
2. Set the output directory in `OUTPUT_DIR` (default: `./results`).
3. Run the notebook cells in order.
4. Inspect the generated figures and tables in `results/`.
