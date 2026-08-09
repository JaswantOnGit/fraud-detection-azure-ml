# ⚠️ RAID Log — Credit Card Fraud Detection

Tracked across the build to catch blockers before they became delays. Status reflects the state at project close.

## Risks

| ID | Risk | Likelihood | Impact | Mitigation | Status |
|---|---|---|---|---|---|
| R1 | Compute cluster fails to provision requested VM size due to regional quota/capacity | Medium | High — blocks training entirely | Confirmed VM SKU availability in West US before submitting AutoML job; fallback SKU identified | Closed — no incident |
| R2 | AutoML job fails with generic retry-exhausted error masking a data access or compute issue | Medium | High | Pre-validated dataset schema and datastore access before job submission | Closed — no incident |
| R3 | Selected best model overfits to the small sample dataset used for this build | Medium | Medium | Flagged in Quality Gate Scorecard as a known limitation; full production dataset required before real deployment | Open — accepted for this build, see Quality Gate notes |
| R4 | Endpoint left running accrues ongoing compute cost after validation is complete | High (default managed endpoint behavior) | Low–Medium (cost) | Documented teardown step; endpoint scoped for short-lived validation only | Monitored |
| R5 | Model drift after deployment goes undetected without a monitoring plan | Medium | High (long-term) | Enabled inferencing data collection at deployment time as the hook for a future drift-monitoring pipeline | Open — fast-follow |

## Assumptions

| ID | Assumption | Validated? |
|---|---|---|
| A1 | The provided transaction dataset is representative enough of real fraud patterns for a proof-of-concept model | Partially — accepted as a lab-scale limitation, not production-representative |
| A2 | AUC (weighted) is an appropriate primary metric given class imbalance | Yes — accuracy would have been misleading on this dataset |
| A3 | Stakeholders reviewing this build understand it is a governed proof-of-concept, not a production-certified model | Yes — stated explicitly in Project Charter scope |

## Issues

| ID | Issue | Resolution | Status |
|---|---|---|---|
| I1 | None encountered during this run — job completed without retries or deployment failures | — | Closed |

## Dependencies

| ID | Dependency | Owner | Status |
|---|---|---|---|
| D1 | Azure subscription with sufficient compute quota in West US | Subscription Owner | Met |
| D2 | Historical labeled transaction data (fraud/not-fraud) | Data source (lab-provided sample) | Met |
| D3 | Azure Machine Learning workspace + linked Storage, Key Vault, App Insights | Provisioned as part of this build | Met |

## Cost Governance Note

Compute cluster and endpoint hosting costs were scoped to a short validation window rather than continuous production hosting. In a real production handoff, this would convert to a tracked monthly run-rate line item owned by the receiving team, with a defined budget ceiling and alerting threshold — not left to accrue indefinitely on a lab subscription.
