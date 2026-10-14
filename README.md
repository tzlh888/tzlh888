# Admissions Research Portfolio — AI Reliability

I am the sole human project lead for three AI-assisted research projects. This portfolio presents their questions, evidence, negative results, and limitations without claiming unaided implementation or invention of every method.

## Research Overview

My projects examine a common reliability problem: a model can look successful under an aggregate metric while remaining unsafe or scientifically unsupported in the cases that matter. WaterSense supplies the strongest controlled quantitative comparison, on dissolved-oxygen estimation across unseen stations and rare low-oxygen observations. AquaVision AI tests whether satellite-derived bloom-proxy labels support geographic generalization, then stops when independent data requirements are not met. Trustworthy AI Research studies whether evidence-pipeline signals can improve error ranking for scientific claim verification. Together, the work emphasizes grouped validation, data identity, subgroup failures, frozen decision rules, and reproducibility. It does not establish deployment readiness, broad geographic transfer, calibrated error probabilities, or independently verified mastery of every technical component.

## Three Research Projects

### 1. WaterSense AI

**Research Question.** Can routine river-water chemistry estimate dissolved oxygen at unseen monitoring stations, and can a development procedure improve detection of observations below 4 mg/L without hiding the cost elsewhere?

**Method and Evidence.** The study uses 151,031 modelling observations from 840 Northern Ireland monitoring stations (1990–2024). Its main upgrade evaluates a frozen model-selection procedure with nested station-grouped cross-validation on a 119,690-observation development partition.

**Main Finding.** Relative to the fixed baseline, the selected procedure reduced low-DO MAE from 3.3235 to 2.3613 mg/L and increased recall from 0.1293 to 0.3641. Overall MAE worsened from 0.8797 to 0.9516 mg/L, precision fell from 0.7903 to 0.5576, and false positives rose from 26 to 219.

**Key Limitation.** The formal comparison covers the complete selected procedure, not weighting alone. Weight-only evidence is exploratory, and no independent external confirmation or operational warning reliability has been established.

**Explore Research.** [Admissions page](research/WATERSENSE_AI.md) · [Full repository](https://github.com/tzlh888/WaterSense-AI)

### 2. AquaVision AI

**Research Question.** Can Sentinel-2 multispectral imagery identify processed NASA CyAN Low, Moderate, and High bloom-proxy classes at geographically unseen waterbodies?

**Method and Evidence.** The historical benchmark contains 288 Sentinel/CyAN patch pairs split into 96 training, 48 validation, and 144 test pairs. Models include spectral indices, Logistic Regression, Random Forest, and short CNN experiments. Later audits distinguish pixels, patches, scenes, and real waterbodies.

**Main Finding.** The validation rule selected NDCI, whose Test High F1 was 0.0006. Logistic Regression reached a higher Test High F1 of 0.5803 but was not validation-selected, so it remains post-hoc evidence rather than a replacement winner. A later six-scene data-integration pilot succeeded technically but produced zero qualified independent High units.

**Key Limitation.** The historical 288 pairs lack confirmed real-world geographic identity, and the pilot did not create a valid training/validation/confirmation split. Cross-waterbody generalization remains unproven; model development correctly stopped.

**Explore Research.** [Admissions page](research/AQUAVISION_AI.md) · [Full repository](https://github.com/tzlh888/AquaVision-AI)

### 3. Trustworthy AI Research

**Research Question.** Can an evidence-aware risk score rank scientific claim-verification errors better than a matched NLI-only score?

**Method and Evidence.** A BM25-and-NLI verifier is paired with logistic error-rankers. B1 uses NLI-derived features; EARS adds retrieval-margin and evidence-conflict features. Evaluation uses grouped SciFact partitions and paired group bootstrap intervals.

**Main Finding.** On the 88-claim Internal Test, EARS improved AURC (0.264987 vs 0.300833) but worsened R80 (0.457143 vs 0.428571), so H1 remained inconclusive. On 188 eligible SciFact Dev claims, EARS had worse AURC but better R80 than B1, with both paired intervals crossing zero.

**Key Limitation.** SciFact Dev is same-dataset evidence, not cross-dataset replication. EARS scores are uncalibrated ranking scores, and the research demo is not a deployment-grade fact-checking service.

**Explore Research.** [Admissions page](research/TRUSTWORTHY_AI.md) · [Full repository](https://github.com/tzlh888/trustworthy-ai-research-lab)

## Research Themes

- **Statistical evaluation:** grouped splits, paired uncertainty, prespecified rules, and explicit endpoint conflicts.
- **Data quality and generalization:** station, scene, waterbody, and document-group identities are treated as scientific variables rather than administrative details.
- **Model reliability:** aggregate accuracy is checked against rare-subgroup error, false alarms, calibration, and selective risk.
- **Reproducibility:** frozen artifacts, tests, decision logs, and negative findings remain visible.

Using established algorithms does not by itself demonstrate independent derivation of their mathematics.

## Research Ownership and AI Assistance

Across all three projects, I am the confirmed sole human project lead and retain responsibility for research direction, integrity requirements, claims, and release decisions. Records support choices including retaining unfavorable endpoints, requiring grouped validation, and stopping when evidence gates failed.

AI-assisted systems contributed substantially to method discussions, protocol drafting, coding, debugging, experiment execution, statistical analysis, reproducibility checks, and writing. The repositories do not establish that I originated every technical idea, wrote every line unaided, or personally verified every calculation. Specific technical understanding should be treated as verified only where a dated, owner-completed record exists.

## Research Evidence and Repositories

| Project | Full repository | Final scientific report | Protocol / methods | Reproducibility | Ownership / contribution |
|---|---|---|---|---|---|
| WaterSense AI | [Repository](https://github.com/tzlh888/WaterSense-AI) | [Final report](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v3/final_closeout/FINAL_SCIENTIFIC_REPORT.md) | [Frozen protocol](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v4_candidate/EXPERIMENT_PROTOCOL.md) | [V4 status](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v4_candidate/WATERSENSE_REPRODUCIBILITY.md) | [Contribution statement](https://github.com/tzlh888/WaterSense-AI/blob/main/research_upgrade_v3/final_closeout/RESEARCH_CONTRIBUTION_STATEMENT.md) |
| AquaVision AI | [Repository](https://github.com/tzlh888/AquaVision-AI) | [Final report](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v3/final_closeout/FINAL_SCIENTIFIC_REPORT.md) | [Readiness decision](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v4_candidate/DATASET_READINESS_DECISION.md) | [V4 status](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v4_candidate/AQUAVISION_REPRODUCIBILITY.md) | [Contribution statement](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v3/final_closeout/RESEARCH_CONTRIBUTION_STATEMENT.md) |
| Trustworthy AI | [Repository](https://github.com/tzlh888/trustworthy-ai-research-lab) | [V2 report](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/reports/research_upgrade_v2/RESEARCH_UPGRADE_V2_REPORT.md) | [Research protocol](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/RESEARCH_PROTOCOL.md) | [Reproducibility](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/REPRODUCIBILITY.md) | [Ownership policy](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/RESEARCH_OWNERSHIP.md) |
