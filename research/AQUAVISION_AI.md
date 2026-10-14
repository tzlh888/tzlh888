# AquaVision AI

[← Portfolio](../README.md) · [Original repository](https://github.com/tzlh888/AquaVision-AI)

## Research Question

Can Sentinel-2 multispectral imagery identify processed NASA CyAN Low, Moderate, and High bloom-proxy classes at geographically unseen waterbodies, and what evidence is required before that generalization claim is defensible?

Each historical example pairs a 12 × 64 × 64 Sentinel-2 patch with a 64 × 64 processed CyAN mask. CyAN supplies satellite-derived proxy labels, not laboratory ground truth, toxin measurements, or direct health-warning categories. Resampling a roughly 300 m CyAN cell onto a 20 m grid creates repeated pixel labels; it does not create thousands of independent biological observations.

## Method and Evidence

The historical benchmark has 288 real Sentinel/CyAN patch pairs: 96 training, 48 validation, and 144 test. Models included spectral-index baselines, Logistic Regression, Random Forest, SmallSegCNN, and DeepLabV3/ResNet18. Pixel-level Macro F1 and class-specific F1 were reported, while a registered validation rule—not the best viewed Test score—controlled model selection.

The intended geographic split kept connected source-grid components together, but later auditing found that 0 of 288 historical patches retained confirmed Sentinel product, footprint, waterbody, and event identity. Those components therefore cannot be treated as verified independent lakes. A prospective pilot separately aligned six frozen Sentinel scenes across three named waterbodies with six version-confirmed NASA CyAN V6 products.

## Main Finding

The validation rule selected NDCI, with Validation Macro F1 0.5751 and Validation High F1 0.0000. On Test it achieved Macro F1 0.5185 and High F1 0.0006. Logistic Regression recorded Test High F1 0.5803, but it was not validation-selected; promoting it after seeing Test would be post-hoc model selection. No CNN passed the predefined class guard.

The new-data pilot confirmed that the acquisition, versioning, geolocation, masking, and alignment pipeline worked for 6/6 scenes. Three scenes across two waterbodies contained High support, totaling 48 distinct native High pixels. However, no waterbody met the frozen requirements for a qualified independent High unit. The resulting training/validation/confirmation membership was 0/0/0, so no new model was trained.

## Evidence Boundary

The evidence supports data integration and a scientifically justified stop decision, not cross-waterbody model generalization. Pixel-level performance cannot substitute for scene- or waterbody-level independence. The historical Test was deliberately High-enriched, so its precision and calibration do not estimate natural prevalence. The six-scene pilot verifies a bounded engineering pathway but not representative data availability, field validity, geographic transfer, or classification improvement. The final status is **LIMITED / NOT READY**.

## Evidence Trail

- [Final scientific report](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v3/final_closeout/FINAL_SCIENTIFIC_REPORT.md)
- [V4 scientific report](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v4_candidate/AQUAVISION_V4_SCIENTIFIC_REPORT.md) and [readiness decision](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v4_candidate/DATASET_READINESS_DECISION.md)
- [Label-integration report](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v3/final_label_pilot/LABEL_INTEGRATION_REPORT.md)
- [Geographic identity audit](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v4_candidate/GEOGRAPHIC_IDENTITY_AUDIT.csv) and [reproducibility status](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v4_candidate/AQUAVISION_REPRODUCIBILITY.md)
- [Core label code](https://github.com/tzlh888/AquaVision-AI/blob/main/src/aquavision/data/labels.py) and [selection/reliability code](https://github.com/tzlh888/AquaVision-AI/blob/main/src/aquavision/evaluation/reliability.py)
- [Research decisions](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v3/RESEARCH_DECISION_LOG.md) and [contribution statement](https://github.com/tzlh888/AquaVision-AI/blob/main/research_upgrade_v3/final_closeout/RESEARCH_CONTRIBUTION_STATEMENT.md)

The applicant is the sole human project lead, with substantial AI assistance across data engineering, analysis, testing, and documentation. The repository supports project-level responsibility and the decision to preserve a negative result; it does not establish unaided technical authorship.
