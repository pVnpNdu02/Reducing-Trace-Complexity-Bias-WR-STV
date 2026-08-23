# Data

## Provenance

Three TrainTicket microservice benchmark trace sets, each a distinct
configuration/version variant of `ts-order-service`:

| Folder | Configuration |
|---|---|
| `dataset_1/` | `ts-order-service_mongodb_4.2.2` |
| `dataset_2/` | `ts-order-service_mongodb_4.4.15` |
| `dataset_3/` | `ts-order-service_3.0.4-mongodb-driver` |

Each dataset folder contains parsed span-level trace data (`logs_clean.parquet`)
and per-container resource metrics (`metrics/`) collected from the running
benchmark deployment.

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
to generate every table in the paper (`paper/tables/*.tex`).

## Regenerating from scratch

The raw TrainTicket deployment logs/traces are not included here (only the
already-parsed, cleaned parquet files are, since they're what the pipeline
consumes directly). To regenerate from a fresh TrainTicket deployment, see
the data-collection cells at the top of the notebook.
