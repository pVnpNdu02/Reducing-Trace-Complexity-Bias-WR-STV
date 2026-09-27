# Data

## What the released pipeline actually uses

The notebook (`notebooks/FINAL_REVISED_ANOMALY_RESEARCH_cleaned_v2.ipynb`) reads
exactly **one** file per dataset as its input:

```
data/dataset_1/spans_long.parquet
data/dataset_2/spans_long.parquet
data/dataset_3/spans_long.parquet
```

Every table and figure in the paper is derived from these three files via the
pipeline described in the notebook (STV construction → per-feature training
statistics → residual normalization → reliability weighting → top-k
aggregation → baselines → statistical tests).

Each `spans_long.parquet` contains one row per span, with columns for trace ID,
span ID, service, operation, root-to-node service path, start time, and
duration, reconstructed from the three TrainTicket configuration variants of
`ts-order-service`:

| Folder | Configuration |
|---|---|
| `dataset_1/` | `ts-order-service_mongodb_4.2.2` |
| `dataset_2/` | `ts-order-service_mongodb_4.4.15` |
| `dataset_3/` | `ts-order-service_3.0.4-mongodb-driver` |

## Other files present in `data/dataset_*/`

`logs_clean.parquet`, `spans_enriched.parquet`, `traces_flat.parquet`,
`baseline_stv.npy`, `baseline_stv_trace_ids.csv`, and `metrics/*.parquet`
(per-container CPU/memory/network time series) are produced by
`notebooks/data_preprocessing.ipynb` (see below) from the raw TrainTicket
deployment capture. **They are included for transparency but are not read by
the main analysis notebook** — the entire reported pipeline runs on
`spans_long.parquet` alone.

## Other files present in `data/paper_experiment_results/`

Most CSVs here are written directly by
`notebooks/FINAL_REVISED_ANOMALY_RESEARCH_cleaned_v2.ipynb`. A handful
(`multi_seed_all_results.csv`, `multi_seed_summary_by_method.csv`,
`multi_seed_summary_by_dataset_method.csv`, `all_dataset_synthetic_v2_results.csv`,
`summary_synthetic_v2_results.csv`) are carried over from an earlier full run
of the same underlying experiment code, prior to the notebook being trimmed
down to the version in this repo. We verified their reported values (e.g.,
per-method ROC-AUC means) are numerically identical to the equivalent, currently
regenerated files (`paper_key_methods_summary_clean.csv`,
`*_clean_pipeline.csv`) — they are kept for traceability, not because the
released notebook regenerates them under those exact filenames.

## Trace-graph quality (verified before modeling)

- Exactly one root span per trace, all three datasets
- Zero non-root spans with a missing parent
- Zero duplicate (traceID, spanID) pairs

See Table II in the paper for full trace/span/service counts per dataset.

## `paper_experiment_results/`

All CSV outputs from the experiment pipeline: complexity-bias correlations,
main detection results, extra-baseline comparisons, statistical tests,
cross-dataset transfer, distribution-shift analysis, explainability overlap,
failure categorization, runtime benchmarks, and hyperparameter validation.

`paper_experiment_results/paper_final_tables/` contains the exact CSVs used
for the results reported in the paper.

### Latest Reviewer Evidence Run

The active `03_complexity_analysis_final` notebook section records a D1-D3
run with seeds 0-4: 30 complexity runs across the `sentinel` and `zero`
missing-value policies, plus 48 perturbation configurations across 5 seeds
and 3 datasets (720 evaluations total). Its saved output confirms all three
datasets and the five-seed checkpoints.

The notebook writes the full reviewer exports to the Colab Drive folder
`_processed_phase1/paper_experiment_results/reviewer_revision_final/`. Those
full CSVs are not currently included in this repository; only the notebook's
displayed previews are available here. See
`paper_experiment_results/reviewer_revision_final/README.md` for the expected
files and export status. Do not treat the obsolete appendix's 3-seed preview
as the final reviewer run.

The files in `paper_experiment_results/runtime_lightweight_analysis/` are
retained: they are produced by the active `09_runtime_final` section, which
uses 3 seeds across 3 datasets (9 runs), not by a deleted notebook section.

## Regenerating from scratch

`notebooks/data_preprocessing.ipynb` parses the raw TrainTicket deployment
capture (structured logs, Prometheus metric JSON, Jaeger trace JSON) into
every file under `data/dataset_*/`, including `spans_long.parquet`. The raw
deployment capture itself is **not included in this repository** — only its
processed output (`data/`) is. To re-run preprocessing from scratch, you need
your own raw TrainTicket capture in the layout documented at the top of that
notebook; point it at `WRSTV_RAW_DATA_ROOT` (or run in Colab with the data in
your own Drive). The main analysis notebook
(`FINAL_REVISED_ANOMALY_RESEARCH_cleaned_v2.ipynb`) picks up from
`spans_long.parquet` onward and runs directly on the `data/` folder already
included in this repo — no raw capture needed to reproduce the paper's
reported results.
