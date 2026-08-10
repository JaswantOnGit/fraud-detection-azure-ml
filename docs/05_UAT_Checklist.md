# 🧪 UAT Checklist - Credit Card Fraud Detection

Validation of the deployed real-time endpoint before sign-off. Conducted from a JupyterLab notebook against the live scoring URI.

| # | Test Scenario | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| 1 | Submit a known **legitimate** transaction to the scoring endpoint | Model returns `0` (not fraud) | `0` returned | ✅ Pass |
| 2 | Submit a known **fraudulent** transaction to the scoring endpoint | Model returns `1` (fraud) | `1` returned | ✅ Pass |
| 3 | Endpoint responds over HTTPS with key-based authentication | Request rejected without valid key | Confirmed - key required to invoke endpoint | ✅ Pass |
| 4 | Endpoint returns a response within an acceptable latency for a synchronous, real-time call | Sub-second response | Confirmed responsive on manual test | ✅ Pass |
| 5 | Provisioning state of the endpoint is healthy before testing begins | `Succeeded` | `Succeeded` | ✅ Pass |
| 6 | Response format is machine-readable and matches what a downstream system would parse | Structured prediction output | Confirmed (byte-encoded array response) | ✅ Pass |

## Sign-Off

| Role | Name | Outcome |
|---|---|---|
| AI Project Manager | Jaswant Singh | Approved - endpoint functions as specified against test scenarios |
| Business Stakeholder (simulated: Fraud Ops) | - | Would require live business sign-off before production use; not substituted by this UAT |

## Evidence

See `notebooks/endpoint_test.ipynb` and `screenshots/10_endpoint_test_legit_txn.png` / `screenshots/11_endpoint_test_fraud_txn.png` for the raw test execution and output.

**Note:** this UAT confirms the endpoint is *functionally* correct - it does not substitute for the full production readiness review called out as a condition in the Quality Gate Scorecard (full dataset retraining, time-based holdout, formal model risk sign-off).
