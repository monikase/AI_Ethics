# Causal Fairness Toolkit
A Practical Methodology for Identifying and Fixing Algorithmic Bias

## 1. Introduction

Machine learning systems sometimes produce different outcomes for different groups of people. But seeing a difference does not automatically tell us whether the system is unfair - or what is causing the difference.  

Disparities can happen for many reasons. A model might directly use a protected attribute (like gender), rely on variables that indirectly reflect it (such as job type or part-time status), reflect patterns from historical inequality, or use legitimate risk factors. Without understanding the real cause, fairness fixes may only treat the symptoms instead of solving the problem.  

The **Causal Fairness Toolkit provides a practical step-by-step method to help teams understand where unfairness comes from and how to address it properly**. It helps teams:   

- Map how protected attributes may influence predictions
- Check whether a decision would change **if only a protected attribute were different, while everything else stayed the same**.
- Separate legitimate prediction factors from discriminatory ones
- Choose the right place in the system to intervene
- Make thoughtful decisions even when information is incomplete

Instead of applying simple statistical adjustments, this toolkit focuses on understanding the reasons behind disparities so that interventions are more precise, transparent, and effective.  

## 2. Toolkit Overview 

The toolkit consists of four components:

1. Causal Modeling Template  
2. Counterfactual Analysis Framework  
3. Intervention Point Identification Method  
4. Limited Information Adaptation Guidelines  

Each step builds on the previous one.

## 3. Causal Fairness Toolkit

## Step 1. Causal Modeling Template

### Goal
Map how protected attributes influence predictions.

## 3.1 Variable Identification Template

### A. Protected Attributes
- List legally protected attributes (e.g., gender, race, age).
- Include intersectional groups where relevant (e.g., gender × age).

Example:
- Gender
- Age
- Gender × Age

---

### B. Outcome Variables
- What decision does the system make?
- What prediction drives that decision?

Example:
- Default risk score
- Loan approval decision

---

### C. Mediators
Variables influenced by protected attributes that also influence outcomes.

Example:
- Gender → Employment history
- Gender → Income level

Ask:
> Does this variable partly reflect structural inequality?

---

### D. Proxy Variables
Variables correlated with protected attributes but not causally necessary for prediction.

Example:
- Zip code
- Part-time employment status

Ask:
> Is this variable functioning as a proxy for a protected attribute?

---

### E. Legitimate Predictors
Variables that genuinely reflect task-relevant ability or risk.

Example:
- Debt-to-income ratio
- Payment history
- Verified savings

Document justification for each variable.

---

## 3.2 Causal Graph Construction

Create a Directed Acyclic Graph (DAG):

- Nodes = variables
- Arrows = causal relationships
- Highlight:
  - Direct paths
  - Proxy paths
  - Mediator paths

Document assumptions behind each arrow.

---

# 4. Step 2 — Counterfactual Analysis Framework

## Goal
Test whether predictions would change if only the protected attribute changed.

---

## 4.1 Counterfactual Query Template

### Base Case
- Individual attributes (non-protected)
- Protected attribute value
- Model prediction

### Counterfactual Scenario
- Change protected attribute
- Keep causally independent variables constant
- Allow descendants to change (if appropriate)

### Evaluation
- Did prediction change?
- If yes → potential counterfactual unfairness

---

## Example

Question:
> Would this applicant be approved if they were male instead of female, keeping debt-to-income ratio and savings constant?

If approval changes → causal discrimination likely exists.

---

## 4.2 Path-Specific Analysis

Break total effect into pathways:

Example:
- Gender → Income → Approval
- Gender → Employment history → Approval

Classify each pathway:
- Legitimate
- Unfair
- Contested

Quantify contribution of each path when possible.

---

# 5. Step 3 — Intervention Point Identification

Use this decision structure:

---

## A. Direct Discrimination
Protected attribute directly affects outcome.

Action:
- Remove attribute
- Add fairness constraints during training

---

## B. Proxy Discrimination
Protected attribute influences outcome via correlated but irrelevant variable.

Action:
- Transform or remove proxy variable (pre-processing)
- Apply adversarial debiasing (in-processing)

---

## C. Mediator Discrimination
Protected attribute affects intermediate variables.

If mediator is:
- Legitimate → consider path-specific fairness
- Not legitimate → adjust or remove influence

---

## D. Output Disparity Only
No clear causal path but group disparity exists.

Action:
- Post-processing (threshold optimization)
- Calibration adjustments

---

# 6. Step 4 — Limited Information Adaptation

Real-world data is incomplete.

Apply:

## 6.1 Multiple Plausible Models
Test fairness under different causal assumptions.

## 6.2 Sensitivity Analysis
- How strong must hidden confounding be to eliminate the observed effect?
- Use E-values or bounding methods.

## 6.3 Intersectional Modeling
- Use hierarchical models when subgroup data is sparse.
- Quantify uncertainty explicitly.

## 6.4 Transparent Documentation
Always document:
- Assumptions
- Uncertainties
- Rationale for intervention choices

---

# 7. Practical Workflow Summary

1. Identify variables
2. Build causal graph
3. Run counterfactual queries
4. Decompose pathways
5. Select targeted interventions
6. Quantify uncertainty
7. Re-evaluate after intervention

---

# 8. Core Principle

Fairness interventions should:

- Address root causes
- Preserve legitimate prediction
- Be transparent about uncertainty
- Be guided by causal reasoning, not correlation alone





