# Case Study: Applying the Causal Fairness Toolkit
## Loan Approval System – Mid-Sized Bank

---

# 1. Problem Context

The bank developed a machine learning system to predict loan default risk.

Decision rule:
- If predicted default risk < 15% → Approve
- Otherwise → Reject

Initial fairness check revealed:
- 76% approval rate for men
- 58% approval rate for women

Observed repayment rates were similar across approved groups.

The team needed to determine:
- Direct discrimination?
- Proxy discrimination?
- Legitimate risk differences?

---

# 2. Step 1 — Causal Modeling

## 2.1 Protected Attributes
- Gender (primary)
- Age (secondary)
- Gender × Age intersections

---

## 2.2 Outcome
- Default risk prediction
- Loan approval decision

---

## 2.3 Mediators

Identified:
- Employment history
- Continuous employment years
- Income level

Causal structure:
Gender → Employment history → Default risk → Approval  
Gender → Income → Debt-to-income ratio → Default risk → Approval  

---

## 2.4 Proxy Variables

Identified:
- Part-time employment status
- Industry sector
- Loan purpose category

Example path:
Gender ↔ Part-time status → Income stability → Default risk → Approval  

---

## 2.5 Legitimate Predictors

- Debt-to-income ratio
- Payment-to-income ratio
- Savings history
- Verified income sources

These reflect repayment ability.

---

# 3. Step 2 — Counterfactual Analysis

## Counterfactual Query

> Would a female applicant receive approval if she were male, holding debt-to-income ratio and savings constant?

---

## Findings

- Counterfactual approval often increased when gender changed.
- Effects strongest for:
  - Applicants with career breaks
  - Applicants with part-time work history

---

## Path-Specific Effects

Approximate contribution:

- Employment history pathway → 40%
- Income level pathway → 25%
- Part-time status pathway → 20%

Remaining 15% uncertain (possible unmeasured factors).

---

# 4. Step 3 — Intervention Selection

## A. Employment History Pathway

Problem:
Continuous employment penalizes caregiving-related career breaks.

Intervention:
Pre-processing transformation:
- Replace "continuous employment" with "relevant experience score"

Rationale:
Better reflects financial reliability.

---

## B. Income Level Pathway

Problem:
Raw income reflects systemic wage gaps.

Intervention:
In-processing constraint:
- Reduce direct weight of raw income
- Focus on repayment ratio instead

Rationale:
Shift focus to repayment capacity rather than absolute income.

---

## C. Part-Time Status Pathway

Problem:
Acts as proxy for gender.

Intervention:
Pre-processing:
- Transform into income stability metric
- Remove binary part-time flag

Rationale:
Capture stability without encoding gender proxy.

---

# 5. Limited Information Considerations

- Sensitivity analysis showed hidden confounders would need strong effect to eliminate disparity.
- Intersectional analysis revealed particularly high unfairness for:
  - Younger women
  - Women returning from career breaks

Hierarchical modeling used to stabilize subgroup estimates.

---

# 6. Results After Intervention

- Approval gap reduced significantly.
- Predictive performance maintained.
- Clear documentation created for regulatory compliance.
- Stakeholder alignment improved due to transparent causal reasoning.

---

# 7. Key Lessons

1. Not all disparities are direct discrimination.
2. Path-specific analysis enables targeted fixes.
3. Proxy variables can be subtle but powerful.
4. Fairness can improve without sacrificing performance.
5. Causal modeling improves explainability and governance.

---

# 8. Conclusion

The Causal Fairness Toolkit enabled the bank to:

- Diagnose root causes of disparity
- Apply precise interventions
- Preserve predictive utility
- Improve fairness in a defensible, transparent way

This approach generalizes beyond lending to hiring, healthcare, risk assessment, and other high-stakes AI systems.
