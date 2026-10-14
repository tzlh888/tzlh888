# Trustworthy AI Research

[← Portfolio](../README.md) · [Original repository](https://github.com/tzlh888/trustworthy-ai-research-lab)

## Research Question

Can a frozen error-risk model that combines natural-language-inference (NLI) behavior with label-free retrieval and evidence signals rank scientific claim-verification errors better than a matched NLI-only risk model?

The work uses official SciFact data. The historical study divided SciFact Train by connected cited-document and normalized-claim groups into Fit, Calibration, and Internal Test partitions. Research Upgrade V2 evaluates official SciFact Dev separately, while recognizing that it remains part of the same dataset family rather than an external dataset.

## Method and Evidence

The E1 verifier retrieves abstracts with BM25, selects sentences by label-free lexical overlap, and applies a pinned NLI model before aggregating SUPPORT, CONTRADICT, or model-output NO_RELATION. B0 is maximum confidence. B1 is a logistic error-ranker using NLI-derived confidence, margin, and predicted category. B2 uses evidence features only. Full EARS adds the normalized top-two BM25 margin and evidence-conflict rate to B1 under matched training, preprocessing, regularization, and solver settings.

AURC measures average selective risk across all accepted prefixes; lower is better. R80 measures risk at one fixed 80% coverage point. A lower AURC does not imply a lower R80, so the frozen H1 criterion required improvement on both. Risk scores order cases for review; without successful calibration they are not probabilities of error.

## Main Findings

On 88 eligible Internal Test claims in 39 groups, the base verifier accuracy was 0.488636. EARS improved AURC from 0.300833 for B1 to 0.264987, but worsened R80 from 0.428571 to 0.457143—32 rather than 30 errors among 70 accepted claims. The frozen conclusion was therefore **H1 INCONCLUSIVE**.

On 188 eligible SciFact Dev claims in 164 groups, B1 achieved AURC 0.281575 and R80 0.413333; EARS achieved AURC 0.288355 and R80 0.400000. The metric directions reversed, and both paired EARS-minus-B1 intervals crossed zero. Matched ablations did not establish stable incremental value from the added evidence features. This preserves the original hypothesis outcome rather than selecting a favorable metric after the fact.

## Evidence Boundary

SciFact Dev is a held-out split from the same dataset family and shares cited documents with historical data; it is not cross-dataset replication. NO_RELATION is a model aggregation outcome, not verified evidence insufficiency. The weak base verifier and modest grouped sample limit inference. EARS is a combination of established methods, not a demonstrated general-purpose algorithmic breakthrough. The Streamlit interface is a research demo, not a scientific-truth service or deployment-ready fact checker.

## Evidence Trail

- [Research Upgrade V2 report](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/reports/research_upgrade_v2/RESEARCH_UPGRADE_V2_REPORT.md)
- [Frozen protocol](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/RESEARCH_PROTOCOL.md) and [same-dataset independence audit](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/reports/research_upgrade_v2/INDEPENDENT_VALIDATION.md)
- [Phase 3B results](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/docs/PHASE3B_RESULTS.md) and [statistical validity](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/reports/research_upgrade_v2/STATISTICAL_VALIDITY.md)
- [Reproducibility](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/REPRODUCIBILITY.md), [core risk metrics](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/src/trustworthy_ai_lab/phase2_protocol.py), and [V2 tests](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/tests/test_research_upgrade_v2.py)
- [Research decisions](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/reports/research_upgrade_v2/RESEARCH_DECISION_LOG_V2.md), [ownership policy](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/RESEARCH_OWNERSHIP.md), and [personal contribution statement](https://github.com/tzlh888/trustworthy-ai-research-lab/blob/main/docs/PERSONAL_RESEARCH_CONTRIBUTION.md)

This is a solo-human-owner, substantially AI-assisted project. The human owner supplied the overarching objective and integrity constraints and retains accountability for public claims and release. AI systems materially assisted method discussion, implementation, execution, analysis, auditing, and writing. Independent invention, unaided coding, and completed personal verification of every technical detail are not claimed.
