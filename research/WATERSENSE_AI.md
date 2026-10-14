# WaterSense AI

[← Portfolio](../README.md) · [Original repository](https://github.com/tzlh888/WaterSense-AI)

## Research Question

Can routine river-water chemistry support dissolved-oxygen (DO) estimation at monitoring stations excluded from training, and can a model-selection procedure improve recognition of measured DO below 4 mg/L without concealing the cost to ordinary-condition accuracy?

The source is the OpenDataNI/Northern Ireland Environment Agency river-water-quality export for 1990–2024. The full modelling table contains 151,031 observations from 840 stations. The focused low-DO experiment uses a recovered development partition of 119,690 unique observations from 672 stations, including 758 low-DO observations at 115 stations. The analysis unit is a water-quality observation, while station identity defines grouping and resampling.

## Method and Evidence

Station-grouped validation matters because repeated measurements from the same location are dependent; row-level random splitting can place one station on both sides and overstate transfer to unseen sites. The main experiment used five outer station-grouped folds to evaluate a complete procedure and four inner folds to select among a frozen 128-candidate grid. Fold-local preprocessing, site-clustered bootstrap intervals, saved out-of-fold predictions, and explicit low-DO metrics support the comparison.

The fixed baseline was a Random Forest with unit weights. A weighted model means a candidate fitted with additional weight on low-DO rows; it is not the same as the complete procedure, which also selects model family and hyperparameters. The selected procedure used inner-selected HistGradientBoosting configurations with a low-DO multiplier of 8 in every outer fold. These are not a matched architecture comparison. A later attribution audit reused 640 saved inner-fold pairs with identical architecture and non-weight settings, differing only by weights 1 and 8. All pairs moved low-DO MAE and recall beneficially, but that post-selection analysis remains exploratory.

## Main Finding

| Metric | Baseline | Selected procedure |
|---|---:|---:|
| Overall MAE | 0.8797 mg/L | 0.9516 mg/L |
| Low-DO MAE | 3.3235 mg/L | 2.3613 mg/L |
| Low-DO recall | 0.1293 | 0.3641 |
| Low-DO precision | 0.7903 | 0.5576 |
| False positives | 26 | 219 |

Under the evaluated development protocol, rare-condition sensitivity improved while overall error and false-alarm burden worsened. Low-DO MAE improved at 102 of 115 low-DO stations, but 482 false negatives remained. The result is therefore a documented trade-off, not a comprehensive model victory.

## Evidence Boundary

The formal conclusion supports the complete model-selection procedure. It does not isolate weighting as the sole cause, because model family and hyperparameters also changed. The matched inner-fold analysis supports weighting as a contributor, not as an independently confirmed causal effect. The outer folds are development cross-validation; they are not an untouched external test or evidence of deployed warning performance. The current official export was byte-identical to the historical file, so independent external confirmation was unavailable.

## Evidence Trail

- [Final scientific report](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v3/final_closeout/FINAL_SCIENTIFIC_REPORT.md)
- [Experiment 1 report](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v3/experiment1_weighted_regression/EXPERIMENT1_RESEARCH_REPORT.md)
- [Matched attribution audit](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v3/experiment1a_attribution/EXPERIMENT1A_ATTRIBUTION_REPORT.md)
- [Frozen protocol](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v4_candidate/EXPERIMENT_PROTOCOL.md) and [reproducibility status](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v4_candidate/WATERSENSE_REPRODUCIBILITY.md)
- [Core experiment code](https://github.com/tzlh888/WaterSense-AI/blob/main/src/weighted_regression_experiment.py) and [tests](https://github.com/tzlh888/WaterSense-AI/blob/main/tests/test_weighted_regression_experiment.py)
- [Research decisions](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v3/RESEARCH_DECISION_LOG.md) and [contribution statement](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v3/final_closeout/RESEARCH_CONTRIBUTION_STATEMENT.md)

The applicant is the sole human project lead, with substantial AI assistance in protocol, implementation, analysis, testing, and writing. Project leadership and reporting responsibility are supported; unaided authorship of every technical component and independent external validation are not.
