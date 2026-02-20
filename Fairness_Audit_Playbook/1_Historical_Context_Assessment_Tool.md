# Historical Context Assessment Tool

## 1. Introduction

The Historical Context Assessment Tool helps teams identify fairness risks early, before they become embedded in system design, data, or optimization choices. It focuses on understanding historical patterns and structural inequalities that could shape the system.

As the first step in the Fairness Audit Playbook, the tool is applied before data collection and model training. Its findings guide later decisions about fairness metrics, evaluation, and mitigation strategies.

## 2. Objectives

- Translate historical discrimination research into actionable engineering methodology
- Map historical patterns to specific AI system risks
- Communicate societal and historical issues to technical audiences
- Balance analytical rigor with practical usability in business environments

## 3. Tool Overview

The Historical Context Assessment Tool consists of four components:

1. **Structured Questionnaire** - Identifies historically relevant discrimination patterns and their mechanisms.  
2. **Risk Classification Matrix** - Prioritizes risks based on severity, likelihood, and relevance.  
3. **Usage Guide** - Explains when and how to apply the tool within development workflows.  
4. **Applied Example** - Demonstrates how the tool can be implemented in a real system. (Internal loan application system).

## 4. Historical Context Assessment Tool

### 4.1 Structured Historical Context Assessment Questionnaire

This questionnaire should be completed collaboratively by engineers, product owners, and, where possible, domain experts. All responses must be documented.

#### Section 1: Domain and Application Context

**1.1 Application Domain Identification**

- What domain does this system operate in (e.g., lending, hiring, healthcare)
- What specific decision or recommendation will the system produce
- Who benefits from correct predictions, and who is harmed by errors

**1.2 Historical Discrimination in the Domain**

- What documented discrimination patterns exist in this domain
- Explicit patterns such as exclusionary criteria
- Implicit patterns such as disparate impact through neutral policies
- Which groups were historically advantaged or disadvantaged

**1.3 Institutional and Regulatory History**

- How have laws, policies, or industry standards shaped outcomes in this domain
- Which practices were legal but discriminatory, and how might their effects persist

#### Section 2: Data and Representation Analysis

**2.1 Historical Data Sources**

- What historical data will inform this system
- Who generated this data, and under what institutional conditions
- Which populations may be underrepresented or over-surveilled

**2.2 Category Formation**

- How have key categories been historically defined
- Have these definitions changed, and if so, why
- Do current categories reflect historical power structures

**2.3 Measurement and Proxies**

- How were key variables historically measured
- Do any features function as proxies for protected attributes
- Does the meaning of these variables differ across demographic groups

**2.4 Missing Data and Structural Gaps**

- Which groups have systematically less data
- Are data gaps random or shaped by institutional barriers
- How might missingness encode historical bias

#### Section 3: Technology Transition and Amplification

**3.1 Prior Technological Systems**

- What non-AI systems previously served this function
- How did those systems reinforce or mitigate inequities

**3.2 Automation and Scale Effects**

- How might automation amplify historical bias
- Does this system reduce discretion or conceal value judgments behind technical abstraction

**3.3 Feedback Loop Risks**

- Will system outputs influence future data collection
- Could disparities compound over time through self-reinforcing cycles

#### Section 4: Intersectionality and Differential Impact

**4.1 Intersectional Risk Identification**

- Which groups experience compounded marginalization
- Would single-attribute analysis miss these risks

**4.2 Representation at Intersections**

- Are intersectional groups sufficiently represented in data
- How confident are we in performance estimates for these groups

### 5.2 Historical Context Risk Classification Matrix

Each identified historical pattern is evaluated using three dimensions:

**Matrix Dimensions**  
**Severity (1–3)**

- 3 (High): Impacts fundamental rights or major life outcomes
- 2 (Medium): Produces significant opportunity or resource disparities
- 1 (Low): Produces limited material harm

**Likelihood (1–3)**

- 3 (High): Frequently appears in similar systems
- 2 (Medium): Occasionally appears
- 1 (Low): Rarely appears

**Relevance (1–3)**

- 3 (High): Directly applies to system’s core function
- 2 (Medium): Applies to specific components
- 1 (Low): Indirect or contextual relevance

**Priority Score = Severity × Likelihood × Relevance**

**Priority Interpretation**

- 7–9 – Critical: Requires immediate mitigation before deployment
- 5–6 – High: Requires mitigation before or shortly after launch
- 3–4 – Medium: Requires monitoring and periodic review
- 1–2 – Low: Documented for awareness. No immediate action required.

Methodology Example Matrix

| Historical Pattern                             | Severity (1–3) | Likelihood (1–3) | Relevance (1–3) | Priority Score | Priority Level |
|------------------------------------------------|----------|------------|------------|----------------|----------------|
| Geographic exclusion in service allocation     | 3        | 3          | 3          | 9              | Critical       |
| Proxy discrimination via location data         | 3        | 3          | 3          | 9              | Critical       |
| Bias against non-traditional employment types  | 2        | 2          | 2          | 8              | High           |
| Underrepresentation in training data           | 2        | 2          | 3          | 12             | Critical       |
| Language-based exclusion in user interface     | 2        | 2          | 1          | 4              | Medium         |


### 5.3 Usage Guide

**Step 1: Domain Research (1–2 hours)**

- Review historical discrimination research relevant to the domain.
- Focus on mechanisms, not just outcomes.

**Step 2: Questionnaire Completion (1–2 hours)**

- Complete collaboratively.
- Explicitly document uncertainty and information gaps.

**Step 3: Risk Classification (30–60 minutes)**

- Score each historical pattern.
- Identify Critical (7–9) and High (5–6) risks.

**Step 4: Integration into Development**

- Translate high-priority risks into:
  - Feature selection constraints
  - Fairness metric selection
  - Evaluation design
  - Monitoring plans  

Historical Context Assessment Tool outputs become inputs to later fairness audits.  


# Appendix A: Applied Example
### Internal Loan Application System

## A.1 Context

An engineering team scoped an AI system to predict eligibility and repayment risk for installment purchases. Lending systems are historically sensitive, making early fairness analysis essential.

## A.2 System Overview

**Domain:** Consumer lending
**System Function:** Predict loan eligibility and repayment risk for installment purchases
**Primary Output:** Approval decision and repayment risk score

## A.3 Completed Historical Context Assessment Questionnaire
### Section 1: Domain and Application Context

#### 1.1 Application Domain Identification
- The system operates in consumer lending and credit allocation.
- It produces eligibility decisions and repayment risk scores.
- Correct predictions benefit both the company and applicants.
- Errors may deny access to credit or expose vulnerable users to financial harm.

---

#### 1.2 Historical Discrimination in the Domain
Documented patterns include:  
- Redlining and geographic exclusion from credit markets
- Exclusionary lending criteria tied to race and class
- Disparate impact through income and employment stability requirements
- Credit invisibility affecting young and marginalized groups  

Historically disadvantaged groups include racial minorities, low-income individuals, migrants, and women.

---

#### 1.3 Institutional and Regulatory History
- Discriminatory lending practices were historically legal.
- Credit scoring systems evolved within unequal access structures.
- Wealth accumulation disparities continue to shape credit outcomes.  

Historical effects may persist through legacy data and institutional definitions of risk.


### Section 2: Data and Representation Analysis

#### 2.1 Historical Data Sources
- Repayment history from prior loans
- Credit bureau data
- Internal transaction data

These datasets reflect unequal historical access to credit. Populations historically denied credit may be underrepresented.

---

#### 2.2 Category Formation
Key categories such as “creditworthiness” and “risk” have historically relied on:
- Stable employment
- Formal income documentation
- Existing credit history

These definitions may disadvantage gig workers, informal workers, migrants, and younger applicants.

---

#### 2.3 Measurement and Proxies
Potential proxy features include:
- ZIP code as a proxy for race and socioeconomic status
- Device type as a proxy for income
- Employment type as a proxy for gender or immigration status

The meaning of income stability may differ across demographic groups.

---

#### 2.4 Missing Data and Structural Gaps
- Credit-invisible applicants have limited historical records.
- Young applicants lack repayment history.
- Informal workers may lack formal documentation.

Missingness is likely structured rather than random. 

### Section 3: Technology Transition and Amplification

#### 3.1 Prior Systems
Previous underwriting involved rule-based systems and human review. Human discretion sometimes mitigated rigid criteria but also introduced inconsistency.

---

#### 3.2 Automation and Scale Effects

Automation may:
- Standardize exclusion
- Scale historical bias
- Conceal value judgments behind technical abstraction

---

#### 3.3 Feedback Loop Risks

- Denied applicants generate no positive repayment data.
- Risk predictions influence future training data.
- Disparities may compound over time.

### Section 4: Intersectionality and Differential Impact

#### 4.1 Intersectional Risk Identification
Compounded marginalization may affect:
- Low-income women
- Migrant workers
- Young minority applicants

Single-attribute fairness analysis may miss these risks.

---

#### 4.2 Representation at Intersections

Intersectional groups may have limited representation in training data, reducing confidence in performance estimates.



## A.3 Applied Risk Classification Matrix


| Historical Pattern                              | Severity | Likelihood | Relevance | Priority Score | Priority Level |
|-------------------------------------------------|----------|------------|------------|----------------|----------------|
| Redlining legacy effects                        | 3        | 3          | 3          | 27             | Critical       |
| Proxy discrimination via ZIP code               | 3        | 3          | 3          | 27             | Critical       |
| Historical repayment data shaped by access bias | 3        | 2          | 3          | 18             | High           |
| Credit invisibility for marginalized users      | 2        | 3          | 3          | 18             | High           |
| Intersectional underrepresentation              | 2        | 2          | 2          | 8              | Medium         |


## A.4 Resulting Design Decisions

Based on the matrix scoring, the team implemented the following changes before model training:
- Removed ZIP code from feature set
- Conducted structured proxy audit
- Redefined target variable to reduce access bias
- Required intersectional performance reporting
- Implemented monitoring for feedback loop dynamics

