# Appendix 3_BSIT_Applied_Example
## Bias Source Identification – Loan Application System

---

## 1. System Context

- System: Installment Lending Risk Model
- Output: Approval decision + risk score
- Fairness Definitions Selected:
  - Equal Opportunity (primary)
  - Calibration
  - Demographic Parity (monitoring)
  - Individual Fairness
  - Counterfactual Fairness

Historical Context identified:
- Financial redlining
- Under-lending to minority communities
- Proxy discrimination via geography and employment patterns

---

## 2. Identified Bias Sources

### 1. Historical Bias in Default Labels

Type: Historical Bias  
Evidence:
- Past lending restricted in minority neighborhoods
- Lower approval rates independent of repayment capacity

Impact:
- Undermines Equal Opportunity
- Reinforces structural exclusion

---

### 2. Representation Imbalance

Type: Representation Bias  
Evidence:
- Sparse samples for recent immigrants and applicants under 25
- Intersectional sparsity (young minority women)

Impact:
- Reduces model stability for minority groups
- Affects Individual Fairness

---

### 3. Zip Code as Proxy Variable

Type: Measurement Bias  
Evidence:
- 0.81 correlation between zip code embeddings and neighborhood demographics
- High SHAP importance score

Impact:
- Violates Counterfactual Fairness
- Reinforces historical redlining patterns

---

### 4. Aggregate Accuracy Optimization

Type: Optimization Bias  
Evidence:
- False negative rate 18% higher for minority applicants
- Gap increased during late training epochs

Impact:
- Direct violation of Equal Opportunity

---

### 5. Threshold Uniformity

Type: Evaluation Bias  
Evidence:
- Single approval threshold produces unequal true positive rates

Impact:
- Conflicts with Equal Opportunity prioritization

---

### 6. Feedback Risk: Credit Building Loop

Type: Direct Feedback Bias  
Evidence:
- Rejected applicants less likely to build credit history
- Reduces future approval probability

Impact:
- High persistence risk
- Amplifies disparities over time

---

## 3. Prioritization

| Bias Source | Sev | Scope | Persist | Hist Align | Feas | Score |
|-------------|-----|-------|--------|------------|------|-------|
| Historical Label Bias | 5 | 5 | 4 | 5 | 2 | 4.5 |
| Optimization Bias | 5 | 4 | 3 | 4 | 4 | 4.1 |
| Threshold Bias | 4 | 5 | 4 | 5 | 5 | 4.5 |
| Zip Code Proxy | 4 | 4 | 4 | 5 | 3 | 4.0 |
| Representation Imbalance | 4 | 4 | 3 | 4 | 3 | 3.7 |
| Feedback Loop Risk | 5 | 3 | 5 | 5 | 2 | 4.3 |

---

## 4. Mitigation Actions

High Priority:
- Label bias correction via reweighting and fairness-aware retraining
- Threshold adjustment aligned with Equal Opportunity
- Remove or transform zip code features
- Implement feedback monitoring dashboard

Medium Priority:
- Intersectional data augmentation
- Adaptive loss weighting

---

## 5. Monitoring Plan

Metrics:
- True positive rate gap
- Calibration by group
- Approval rate disparity
- Disparity growth rate (quarterly)

Escalation Trigger:
- >5% increase in TPR gap
- Exponential disparity growth trend

---

## Summary

BSIT revealed that:
- Primary risks stem from historical labels and optimization dynamics.
- Feedback amplification presents long-term systemic risk.
- Deployment monitoring is required to prevent progressive exclusion.

Bias mitigation was prioritized according to documented severity, historical alignment, and fairness definition impact.

All decisions were documented for governance review.
