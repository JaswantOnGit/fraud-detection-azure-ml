# ✅ Quality Gate Scorecard — Credit Card Fraud Detection

Gate checked before promoting the AutoML output from "trained candidate" to "deployed model." A model does not pass to deployment on AUC alone — every row below had to be explicitly checked.

| Gate Criterion | Threshold | Actual | Pass/Fail |
|---|---|---|---|
| Primary metric (weighted AUC) | ≥ 0.95 | 0.98584 | ✅ Pass |
| Metric appropriate for class imbalance | AUC or equivalent, not raw accuracy | Weighted AUC used | ✅ Pass |
| Validation strategy | Automatic train/validation split applied | Confirmed | ✅ Pass |
| Multiple candidate models compared | ≥ 3 algorithm families evaluated | 4 evaluated (SVM, Voting Ensemble, Random Forest, +1 additional trial) | ✅ Pass |
| Best model selection justified | Documented reason for selection, not just top score | StandardScalerWrapper+SVM selected as top-scoring, stable candidate | ✅ Pass |
| Model registered before deployment | Yes | Registered via Azure ML model registry | ✅ Pass |
| Endpoint tested against known-positive and known-negative cases | Both required | Legitimate txn → `0`, fraudulent txn → `1` | ✅ Pass |
| Training data representativeness | Full production-scale dataset | **Sample dataset used, not full production volume** | ⚠️ Conditional — see note |
| Monitoring hook enabled at deployment | Yes | Inferencing data collection enabled | ✅ Pass |
| Cost / teardown plan documented | Yes | See RAID Log cost governance note | ✅ Pass |

## Gate Decision: **Conditional Pass**

Promoted to deployment for validation and portfolio purposes with one explicit condition carried forward: **this model is trained on a lab-scale sample and is not certified against full production transaction volume or a live-data holdout set.** Before any real production use, this model would require:

1. Retraining against the full historical transaction dataset
2. A held-out, time-based test set (not just a random split) to check for temporal drift
3. Formal model risk sign-off per the institution's model governance framework

This condition is stated explicitly rather than glossed over — a governance scorecard that only ever says "pass" isn't doing its job.
