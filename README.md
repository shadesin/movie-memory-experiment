# Movie Memory Experiment

**Team: The Outliers**  
Behavioral Research: Statistical Methods (BRSM) · IIIT Hyderabad · March 2026

| Member | Roll No. |
|---|---|
| Souradeep Das | 2025201004 |
| Srinjoy Sengupta | 2025202010 |
| Surjit Mandal | 2025201057 |

---

## Overview

This repository contains the full analysis pipeline for a recognition memory experiment investigating whether abrupt film cuts impair memory for nearby frames compared to natural event boundaries.

**Research Questions:**
- **RQ1** — Does viewing condition (abrupt cut vs. natural boundary) affect overall recognition accuracy and response time?
- **RQ2** — Is recognition of Before-Boundary (BB) frames lower in the Abrupt-cut group?
- **RQ3** — Is recognition of Event-Middle (EM) frames similar across conditions (EM is far from the cut point)?

---

## Experiment Design

- **Participants:** 166 (AB *n* = 79; NB *n* = 87) from IIIT Hyderabad
- **Stimuli:** 40 YouTube Shorts clips, each prepared in two versions:
  - **AB (Abrupt-cut):** clip ends 1–5 s before a consensus event boundary
  - **NB (Natural-boundary):** clip ends at the unedited natural endpoint
- **Recognition task:** 2-AFC (two-alternative forced choice) — one target frame vs. one unseen lure, at three difficulty levels (easy, moderate, difficult)
- **Target types:** BB (Before-Boundary frame) and EM (Event-Middle frame)
- **Confidence rating:** 1–5 scale after each recognition decision
- **Software:** PsychoPy

**Design:** Between-subjects on Condition (AB/NB); within-subjects on Target Type (BB/EM)

---

## Analysis Pipeline (`phase1.Rmd`)

The R Markdown file runs end-to-end from raw CSVs to all reported statistics and figures:

1. **Data ingestion** — reads all per-subject PsychoPy CSVs, parses subject IDs and condition labels
2. **Exclusions** — removes corrupt file (`sub42_NB`) and 4 vigilance failures (encoding > 27.05 min)
3. **RT sanity check** — flags encoding-phase rows (no RT recorded by design)
4. **Demographic balance checks** — Mann–Whitney *U* (age), chi-square (gender)
5. **Accuracy analysis** — per-subject means, 2×2 breakdown (Condition × Target Type)
6. **REC and LDI** — bias-corrected discrimination indices
7. **RT and confidence** — subject-level means and distributions
8. **Confidence–accuracy calibration** — monotonic calibration curves
9. **Correlation matrix** — Pearson *r* across subject-level variables
10. **Normality testing** — Shapiro–Wilk tests + Q-Q plots → justification for non-parametric tests
11. **Planned inferential tests** — Mann–Whitney *U*, Mixed ANOVA, Spearman *ρ*

---

## Key Results

| Measure | AB | NB | Δ (NB − AB) |
|---|---|---|---|
| Mean accuracy | 83.8% (SD 8.2%) | 87.0% (SD 7.3%) | +3.2 pp |
| REC | 0.676 | 0.740 | +0.064 |
| BB accuracy | 82.2% | 85.8% | +3.6 pp |
| EM accuracy | 85.4% | 88.3% | +2.9 pp |
| Mean RT (s) | 5.56 (SD 1.41) | 5.76 (SD 1.64) | — |
| Mean confidence | 4.07 (SD 0.46) | 4.20 (SD 0.42) | — |

Shapiro–Wilk tests rejected normality for both conditions (AB: *W* = 0.957, *p* = .009; NB: *W* = 0.942, *p* < .001), requiring non-parametric inferential tests.

---

## Requirements

The following R packages are required:

```r
install.packages(c("tidyverse", "knitr", "kableExtra", "ggplot2", "ggridges", "ggcorrplot", "rmarkdown"))
```

### Usage

To run the full analysis, place `phase1.Rmd` in the same directory as the data folder (`BRSM data csv/`) and knit:

```r
rmarkdown::render("phase1.Rmd")
```

This produces an HTML report with all tables, figures, and statistics.

---

## Exclusion Criteria

| Stage | Change | N |
|---|---|---|
| Recruited | | 184 |
| Data error (first 13) | −13 | 171 |
| Corrupt file (sub42_NB) | −1 | 170 |
| Vigilance failures (encoding > 27.05 min) | −4 | **166** |

Vigilance threshold = 5.6 min (repeated clips) + 25 s assumed skip latency × 5 repetitions = 27.05 min.  
Failed participants: sub32-AB (27.3 min), sub36-AB (27.8 min), sub151-NB (27.2 min), sub161-NB (28.0 min).

---

## Contact

Experiment lead: gargi.shukla@research.iiit.ac.in
