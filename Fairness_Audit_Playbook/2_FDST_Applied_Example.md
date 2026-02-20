# Fairness Definition Selection Tool: Applied Example  
### Internal Loan Application System

---

## 1. Application Context

- **System Name:** Installment Lending Risk Model  
- **Decision Domain:** Consumer lending  
- **Primary Output:** Loan approval decision and repayment risk score  
- **Stakeholders:**  
  - Loan applicants  
  - Lending institution  
  - Compliance and legal teams  
- **Protected Attributes Evaluated:**  
  - Gender  
  - Ethnicity  
  - Age  

---

## 2. Historical Context Summary

The Historical Context Assessment identified:

- Legacy redlining and geographic exclusion  
- Income-based bias against non-traditional workers  
- Credit invisibility affecting young and marginalized applicants  

**Systemic exclusion identified:** ☑ Yes  

Because historical under-lending patterns were identified, **Demographic Parity was included as a baseline fairness consideration** to address structural exclusion risks.

---

## 3. Selected Fairness Definitions

### Primary Fairness Definition  
**Equal Opportunity**

**Rationale:**  
False negatives (wrongly rejecting qualified applicants) were determined to cause greater long-term harm than false positives. Denying credit to individuals who would repay perpetuates historical exclusion and reduces wealth-building opportunities.

The model therefore prioritizes equal true positive rates across protected groups.

---

### Secondary Fairness Definitions

☑ Demographic Parity  
☑ Calibration / Predictive Parity  
☑ Individual Fairness  
☑ Counterfactual Fairness  

---

### Rationale for Secondary Definitions

- **Demographic Parity** was included to monitor representation-level disparities due to historical under-lending.
- **Calibration** was required because risk scores are exposed to downstream financial systems.
- **Individual Fairness** was included to ensure procedural consistency between similar applicants.
- **Counterfactual Fairness review** was triggered due to concerns that protected attributes may influence income, employment type, and credit history through structural pathways.

---

## 4. Error Harm Analysis

- **False Negatives (FN):** Deny qualified applicants access to credit and reinforce structural inequality.
- **False Positives (FP):** Create financial risk for the lender but can be partially mitigated through pricing and credit limits.

**Conclusion:** False negatives create greater long-term societal harm.

This justified prioritizing **Equal Opportunity** over Predictive Equality.

---

## 5. Trade-Off Documentation

### Known Mathematical Tensions Identified

- Equal Opportunity vs Calibration  
- Equal Opportunity vs Demographic Parity (when base rates differ)

### Impossibility Constraints Identified  
☑ Yes  

Due to differing historical repayment base rates across groups, it was not possible to simultaneously satisfy Equalized Odds, Demographic Parity, and Calibration.

The team explicitly prioritized:

1. Equal Opportunity  
2. Calibration  
3. Monitoring Demographic Parity as a secondary metric  

---

### Definitions Not Selected and Why

**Equalized Odds**  
- Not selected as primary because equalizing false positives was not considered equally harmful in this domain.

**Predictive Equality (equal FP rates)**  
- Deprioritized due to greater concern about false negative harm.

---

### Expected Performance Impact

- **Accuracy Impact:** Slight reduction in overall predictive accuracy due to constraint optimization.
- **Operational Impact:** Additional model evaluation complexity.
- **Stakeholder Impact:** Improved access equity for historically excluded groups.

---

## 6. Legal and Regulatory Alignment

Relevant regulations included:

- Anti-discrimination and equal credit opportunity laws  
- Financial risk disclosure requirements  

Selected fairness definitions were reviewed for compliance with protected attribute obligations.

☑ Legal alignment confirmed.

---

## 7. Individual-Level and Causal Review

**Individual-level consistency concern:** ☑ Yes  
Loan decisions are high-impact and require procedural fairness.

**Structural or causal bias identified:** ☑ Yes  
Income stability and employment type were influenced by historical labor market inequalities.

Mitigation actions:
- Conducted proxy feature audit  
- Modeled alternative income stability measures  
- Evaluated causal pathways before feature inclusion  

---

## 8. Intersectional Evaluation

Intersectional groups evaluated:

- Young women  
- Migrant applicants  
- Low-income minority applicants  

Disparities were more pronounced at intersections than single-attribute levels.

Mitigation:
- Required subgroup-level performance reporting  
- Set monitoring thresholds for intersectional disparities  

---

## 9. Monitoring Plan

**Metrics Tracked:**
- True positive rates by group  
- Calibration curves by group  
- Approval rate distribution  
- Intersectional performance gaps  

**Review Frequency:** Quarterly  

**Responsible Team:**  
- Model Risk Management  
- Compliance and Fairness Review Board  

**Re-evaluation Trigger Conditions:**
- Significant drift in base rates  
- Emerging regulatory changes  
- Persistent subgroup disparity exceeding threshold  

---

## Summary

The Fairness Definition Selection Tool enabled structured prioritization of fairness definitions under known impossibility constraints.  

Trade-offs were explicitly documented, legal compliance was verified, and intersectional impacts were evaluated prior to model deployment.

Fairness decisions were treated as governance choices requiring justification rather than default technical settings.
