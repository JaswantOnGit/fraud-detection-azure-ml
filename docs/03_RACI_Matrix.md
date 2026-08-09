# 🔁 RACI Matrix — Credit Card Fraud Detection

**R** = Responsible · **A** = Accountable · **C** = Consulted · **I** = Informed

| Activity | AI Project Manager | Data Science / ML Engineering | Risk & Compliance | Business Stakeholder (Fraud Ops) | IT / Cloud Ops |
|---|---|---|---|---|---|
| Define project scope & success criteria | **A/R** | C | C | C | I |
| Provision Azure ML workspace & compute | R | C | I | I | **A** |
| Source & register training dataset | C | **A/R** | C | I | I |
| Configure & submit AutoML job | I | **A/R** | I | I | I |
| Select primary evaluation metric (AUC vs. accuracy) | C | **A/R** | C | I | I |
| Review candidate models against quality gate | **A** | R | C | I | I |
| Approve model promotion to deployment | **A** | R | **C (sign-off required)** | C | I |
| Deploy model to real-time endpoint | I | **A/R** | I | I | C |
| Validate endpoint against test transactions (UAT) | **A** | R | I | **R (business sign-off)** | I |
| Define post-deployment monitoring plan | **A/R** | C | C | I | C |
| Own cost governance for ongoing endpoint hosting | **A/R** | I | I | I | C |
| Own decommission / teardown of lab resources | **A/R** | I | I | I | C |

## Notes

- **Risk & Compliance** sign-off is called out explicitly at model promotion — in a real financial-services environment, a model touching fraud decisions does not go to production without this checkpoint, regardless of how strong the AUC score looks.
- **Business Stakeholder** ownership of UAT reflects that a technically correct model is not the same as a business-approved one — the fraud operations team validating real transaction scenarios is what actually de-risks go-live.
- This matrix reflects how the project *would* be staffed and governed in a production financial-services setting. For this individual build, the AI Project Manager role executed the Data Science / ML Engineering and IT / Cloud Ops activities directly, with the RACI structure applied as the operating discipline.
