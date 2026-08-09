# 📋 Project Charter — Credit Card Fraud Detection

| Field | Detail |
|---|---|
| **Project Name** | Real-Time Credit Card Fraud Detection |
| **Sponsor (simulated)** | Head of Fraud & Risk Operations |
| **Project Manager** | Jaswant Singh, AI Project Manager |
| **Workspace** | `Credit-Fraud-Detection` (Azure Machine Learning, West US) |
| **Start Date** | Aug 9, 2026 |
| **Status** | Deployed — real-time endpoint live |

## 1. Business Problem

The institution's existing fraud controls rely on manual transaction review and static, rule-based flags. This produces two costly failure modes:

- **Missed fraud** — sophisticated patterns that don't trip a static rule go undetected until after the loss occurs.
- **False positives** — legitimate customers get declined or flagged, damaging trust and increasing support volume.

## 2. Objective

Deliver a machine learning classification model that scores each transaction as fraudulent or legitimate **in real time**, exposed as an API endpoint that downstream transaction-processing systems can call synchronously at the point of authorization.

## 3. Scope

**In scope**
- Data ingestion and validation of historical labeled transaction data
- AutoML-driven model selection across multiple candidate algorithms
- Model promotion through a defined quality gate
- Deployment as a managed, real-time scoring endpoint
- Post-deployment monitoring hook (inferencing data collection) for future drift review

**Out of scope (this phase)**
- Integration into the live payment-authorization system (handoff to Engineering)
- Champion/challenger testing against the existing rules engine
- Multi-region failover / high-availability endpoint architecture
- Formal model risk management (SR 11-7 style) documentation — noted as a fast-follow

## 4. Success Criteria

| Criterion | Target | Result |
|---|---|---|
| Weighted AUC on validation set | ≥ 0.95 | **0.98584** ✅ |
| Model deployed as callable real-time endpoint | Yes | ✅ `credit-fraud-detection-mbydj` |
| Endpoint validated against known legitimate + known fraudulent transactions | Yes | ✅ (see `notebooks/endpoint_test.ipynb`) |
| Governance artifacts complete before promotion | Yes | ✅ this folder |

## 5. Key Stakeholders

See [`03_RACI_Matrix.md`](03_RACI_Matrix.md) for the full accountability breakdown.

## 6. High-Level Timeline

| Milestone | Date |
|---|---|
| Workspace + compute provisioned | Aug 9, 2026, 2:45 PM |
| Dataset registered | Aug 9, 2026, 3:02 PM |
| AutoML training job submitted | Aug 9, 2026, 3:11 PM |
| Best model selected, quality gate passed | Aug 9, 2026, 3:20 PM |
| Model deployed to real-time endpoint | Aug 9, 2026, 4:44 PM |
| Endpoint validated (UAT) | Aug 9, 2026, 5:05–5:06 PM |

## 7. Budget Note

Compute, storage, and endpoint hosting for this build stayed within a defined lab-scale budget ceiling (compute cluster + short-lived managed endpoint). See cost governance note in [`02_RAID_Log.md`](02_RAID_Log.md).
