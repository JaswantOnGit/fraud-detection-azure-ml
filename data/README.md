# Data

`creditcard_sample.csv` - a small, PCA-anonymized sample of credit card transactions used to train and validate the model in this build.

- Columns `V1`–`V28` are principal components from a PCA transformation of the original features (no raw personal or account data is present).
- `Time` and `Amount` are the only non-transformed features.
- `Class` is the label: `0` = legitimate, `1` = fraud.

**This is a lab-scale sample, not the full production-representative dataset.** See the conditional note in [`../docs/04_Quality_Gate_Scorecard.md`](../docs/04_Quality_Gate_Scorecard.md) - any real production use of this model would require retraining against full transaction volume with a time-based holdout set.
