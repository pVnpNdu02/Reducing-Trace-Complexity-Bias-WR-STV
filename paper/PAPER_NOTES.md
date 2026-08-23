# WR-STV Paper — Overleaf Project

## How to use this project

1. Upload this whole folder to a new Overleaf project (or `git push` it if
   your Overleaf plan supports Git sync).
2. Set the Overleaf compiler to **pdfLaTeX** and main document to `main.tex`.
3. Every `\todo{...}` in the section files is a red inline marker for
   something that still needs your judgment, a citation, a real figure, or
   a number to be filled in from a CSV. Search the project for `\todo{` to
   find them all; there is no code meaning attached to the macro besides
   highlighting, so it's safe to leave them in while drafting and strip
   them right before submission (see below).

## What is already filled in with real numbers

All tables in `tables/` are populated with the actual results already
computed and verified in your notebook (dataset stats, complexity-bias
correlations, main detection results, extra-baseline comparison,
statistical tests, explainability overlap, failure taxonomy, runtime).
Two cells in `table5_cross_dataset_pairs.tex` are marked `\todo{fill}`
because their exact values weren't available when this project was
generated — pull them from `cross_pair_summary_df` in the notebook.

## What is NOT filled in

- **Figures.** All figures are `\fbox{...}` placeholders with a `\todo{}`
  describing exactly what to plot and which notebook variable/cell to plot
  it from. Generate each as a real PDF or PNG from the notebook (the
  cleaned notebook already has `savefig`-ready plotting cells for most of
  these — see `fig_complexity_bias_num_spans`,
  `fig_random_visible_sensitivity_roc_auc`, `fig_failure_categories` if you
  added the final-figure export cell), drop the file into `figures/`, and
  replace the `\fbox{...}` block with
  `\includegraphics[width=\linewidth]{figures/your_file.pdf}`.
- **Prose in Introduction, Related Work, Background.** These are drafted
  with real, established facts and specific `\todo{}` prompts telling you
  exactly what each remaining paragraph needs to say — they are
  intentionally left as guided fill-in rather than fully authored, since
  the framing/motivation choices are yours to make (and because inventing
  citations you haven't verified is worse than leaving a gap).
- **Bibliography.** `references.bib` has three verified, DOI-checked
  entries (TraceAnomaly, Al-Omari 2025, Xing et al. 2025) plus placeholder
  `@misc` entries with search terms for citations you'll want to add
  (Isolation Forest, LOF, One-Class SVM, TrainTicket, TraceVAE). Replace
  each placeholder with a real BibTeX entry before submission — do not
  cite the placeholder entries as-is.

## Before submission checklist

```text
[ ] grep -r "\\todo{" sections/ tables/ appendix/   -- resolve every hit
[ ] Replace all \fbox{...} figure placeholders with real \includegraphics
[ ] Replace all @misc placeholder bib entries with verified citations
[ ] Fill the two blank cells in table5_cross_dataset_pairs.tex
[ ] Re-run the notebook top-to-bottom once; confirm every number in
    tables/*.tex still matches the fresh output (see the comparison
    script Claude offered to write in the prior conversation turn)
[ ] Check IEEEtran page/word limits for your target venue and trim
    the abstract and results prose accordingly
```
