# Reviewer Revision Final Outputs

## Status

The active notebook section `03_complexity_analysis_final` records the completed D1-D3 reviewer run. Its full output CSVs were written to the Colab Drive path:

`_processed_phase1/paper_experiment_results/reviewer_revision_final/`

The full exports are not present in this repository yet. The notebook's saved cell output contains summary previews and run-completion checks, not the complete CSV contents. This folder is intentionally a status note, not a substitute for the missing result data.

## Recorded Run

- Datasets: `dataset_1`, `dataset_2`, `dataset_3`
- Seeds: `0` through `4`
- Complexity analysis: both `sentinel` and `zero` missing-value policies, for 30 dataset/seed/policy runs
- Perturbation sweep: 48 configurations across 5 seeds and 3 datasets, for 720 evaluations
- Checkpoints: one CSV per seed/dataset pair, 15 total
- Additive perturbation duration assumption: microseconds; verify before citing additive results

## Expected Exports

- `complexity_all.csv`
- `complexity_summary.csv`
- `complexity_by_dataset.csv`
- `perturbation_all.csv`
- `perturbation_grid_summary.csv`
- `perturbation_checkpoints/seed{seed}_dataset_{dataset}.csv`

Do not use the obsolete appendix's 3-seed output preview as the final paper result. The separate `../runtime_lightweight_analysis/` artifacts remain valid outputs from the active `09_runtime_final` stage (3 seeds x 3 datasets, 9 runs).
