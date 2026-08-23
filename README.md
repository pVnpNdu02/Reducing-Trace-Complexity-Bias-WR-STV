# Reducing Trace-Complexity Bias in Microservice Anomaly Scoring via Weighted Residual Service Trace Vectors

This repository contains the code, data, and reproduction materials for the paper
**"Reducing Trace-Complexity Bias in Microservice Anomaly Scoring via Weighted
Residual Service Trace Vectors"** (WR-STV).

## Summary

We show that a common pattern in microservice trace anomaly detection — scoring
a Service Trace Vector (STV) representation with a generic unsupervised
detector such as Isolation Forest — produces anomaly scores that are strongly
correlated with trace structural complexity (number of services/spans),
independent of whether a trace is actually anomalous. We propose **WR-STV**
(Weighted Residual Service Trace Vector), a lightweight per-feature
standardization, clipping, and reliability-weighting scheme that substantially
reduces this bias while improving controlled latency-anomaly detection over
the baseline.

## Repository Structure

```
notebooks/    Full experiment pipeline (data loading -> STV construction ->
              WR-STV -> baselines -> evaluation -> statistical tests)
data/         Processed TrainTicket traces/metrics and all experiment result
              CSVs (see data/README.md for provenance)
paper/        LaTeX source for the paper (IEEEtran), tables, and figures
figures/      Standalone diagram sources (pipeline figure, etc.)
```

## Reproducing the Results

1. Create an environment and install dependencies:
   ```bash
   python -m venv venv && source venv/bin/activate
   pip install -r requirements.txt
   ```
2. Open `notebooks/FINAL_REVISED_ANAMOLY_RESEARCH_cleaned_v2.ipynb` in Jupyter.
3. The notebook expects the `data/` folder (already included in this repo) at
   a path configured in the first cell — update that path if you relocate the
   data.
4. Run all cells top to bottom. Each experiment section prints/saves its
   result table to `data/paper_experiment_results/paper_final_tables/`,
   matching the tables in `paper/tables/`.

## Dataset

Three configuration variants of the `ts-order-service` microservice from the
[TrainTicket](https://github.com/FudanSELab/train-ticket) benchmark system
(Zhou et al., IEEE TSE 2021). See `data/README.md` for exact provenance,
collection method, and per-dataset statistics.

## Citation

If you use this code or data, please cite:

```bibtex
@inproceedings{ramina2026wrstv,
  author    = {Ramina, Pavan Kumar},
  title     = {Reducing Trace-Complexity Bias in Microservice Anomaly Scoring via Weighted Residual Service Trace Vectors},
  year      = {2026}
}
```

(Update with final venue/DOI once accepted.)

## License

Code is released under the MIT License (see `LICENSE`). Data derived from the
TrainTicket benchmark is subject to TrainTicket's own license terms.

## Contact

Pavan Kumar Ramina — pavankumar_ramina@srmap.edu.in
