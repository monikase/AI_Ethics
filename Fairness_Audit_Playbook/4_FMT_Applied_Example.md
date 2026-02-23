# Appendix: Fairness Metrics Tool Applied Example
## Internal Loan Approval Risk Model

---

## 1. System Context

System Type: Classification  
Output: Approve / Reject  
Risk Score: Default probability  

Selected Fairness Definitions:

- Equal Opportunity (Primary)
- Predictive Parity
- Demographic Parity (Monitoring)
- Counterfactual Fairness

Historical Context Identified:
- Lending discrimination
- Geographic proxy risk
- Under-lending to minority applicants

---

## 2. Step 1: Metric Selection

Based on system type and selected definitions:

Primary Metric:
→ Equal Opportunity Difference (TPR Difference)

Secondary Metrics:
→ False Negative Rate Difference
→ Predictive Parity Difference
→ Statistical Parity Difference

Intersectional:
→ Intersectional Equal Opportunity

Counterfactual:
→ Counterfactual Prediction Gap

---

## 3. Step 2: Baseline Results

Equal Opportunity Difference: 0.08  
95% CI: [0.03 – 0.13]  
p = 0.004 (significant)

False Negative Rate Difference: 0.09  
95% CI: [0.04 – 0.14]

Predictive Parity Difference: 0.03  
95% CI: [-0.02 – 0.08]  
Not statistically significant

Statistical Parity Difference: 0.07  
95% CI: [0.01 – 0.12]  
Significant

---

## 4. Intersectional Findings

Black Women Subgroup:

Equal Opportunity Difference: 0.15  
Bootstrap CI: [0.05 – 0.23]  
Sample Size: 94 (Bayesian estimate used)

Simpson’s Paradox Observed:
Gender parity appears acceptable in aggregate,
but race-gender intersection shows amplified disparity.

---

## 5. Counterfactual Analysis

Zip code feature perturbed (proxy for race).

18% of minority applicants experienced
prediction shift > 0.10 probability.

Indicates causal sensitivity risk.

---

## 6. Robustness Testing

5-fold Cross-validation:
EOD range: 0.06 – 0.10

Temporal split (2023 vs 2024 data):
Disparity consistent.

Result: Disparity robust.

---

## 7. Governance Summary

| Metric | Disparity | Significant | Robust | Action |
|--------|-----------|------------|--------|--------|
| EOD | 0.08 | Yes | Yes | Mitigate |
| SPD | 0.07 | Yes | Yes | Monitor |
| PPD | 0.03 | No | Stable | No Action |
| Intersectional EOD | 0.15 | Yes | Moderate | Targeted Review |

---

## 8. Intervention Plan

- Apply fairness-constrained retraining.
- Adjust decision thresholds.
- Review geographic proxy features.
- Implement quarterly monitoring.
- Require intersectional reporting in governance review.

---

## 9. Monitoring Plan

Metrics monitored quarterly:

- Equal Opportunity Difference
- Intersectional EOD
- Predictive Parity
- Counterfactual Sensitivity

Escalation Trigger:
- >5% increase in disparity
- Loss of robustness
- Emergence of new intersectional gaps
