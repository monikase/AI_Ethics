# Historical Context Assessment Tool: Applied Example

### Internal Loan Application System

## 1. Context

An engineering team scoped an AI system to predict eligibility and repayment risk for installment purchases.  
Lending systems are historically sensitive, making early fairness analysis essential.

## 2. System Overview

**Domain:** Consumer lending  
**System Function:** Predict loan eligibility and repayment risk for installment purchases  
**Primary Output:** Approval decision and repayment risk score  

## 3. Completed Historical Context Assessment Questionnaire
### Section 1: Domain and Application Context

#### 1.1 Application Domain Identification
- The system operates in consumer lending and credit allocation.
- It produces eligibility decisions and repayment risk scores.
- Correct predictions benefit both the company and applicants.
- Errors may deny access to credit or expose vulnerable users to financial harm.

#### 1.2 Historical Discrimination in the Domain
Documented patterns include:  
- Redlining and geographic exclusion from credit markets
- Exclusionary lending criteria tied to race and class
- Disparate impact through income and employment stability requirements
- Credit invisibility affecting young and marginalized groups  

Historically disadvantaged groups include racial minorities, low-income individuals, migrants, and women.

#### 1.3 Institutional and Regulatory History
- Discriminatory lending practices were historically legal.
- Credit scoring systems evolved within unequal access structures.
- Wealth accumulation disparities continue to shape credit outcomes.  

Historical effects may persist through legacy data and institutional definitions of risk.

---

### Section 2: Data and Representation Analysis

#### 2.1 Historical Data Sources
- Repayment history from prior loans
- Credit bureau data
- Internal transaction data

These datasets reflect unequal historical access to credit. Populations historically denied credit may be underrepresented.

#### 2.2 Category Formation
Key categories such as “creditworthiness” and “risk” have historically relied on:
- Stable employment
- Formal income documentation
- Existing credit history

These definitions may disadvantage self-employed individuals, freelance or platform-based workers, informal workers, migrants, and younger applicants.

#### 2.3 Measurement and Proxies
Potential proxy features include:
- ZIP code as a proxy for race and socioeconomic status
- Device type as a proxy for income
- Employment type as a proxy for gender or immigration status

The meaning of income stability may differ across demographic groups.

#### 2.4 Missing Data and Structural Gaps
- Credit-invisible applicants have limited historical records.
- Young applicants lack repayment history.
- Informal workers may lack formal documentation.

Missingness is likely structured rather than random. 

---

### Section 3: Technology Transition and Amplification

#### 3.1 Prior Systems
Previous underwriting involved rule-based systems and human review. Human discretion sometimes mitigated rigid criteria but also introduced inconsistency.

#### 3.2 Automation and Scale Effects

Automation may:
- Standardize exclusion
- Scale historical bias
- Conceal value judgments behind technical abstraction

#### 3.3 Feedback Loop Risks

- Denied applicants generate no positive repayment data.
- Risk predictions influence future training data.
- Disparities may compound over time.

---

### Section 4: Intersectionality and Differential Impact

#### 4.1 Intersectional Risk Identification
Compounded marginalization may affect:
- Low-income women
- Migrant workers
- Young minority applicants

Single-attribute fairness analysis may miss these risks.

#### 4.2 Representation at Intersections

Intersectional groups may have limited representation in training data, reducing confidence in performance estimates.

---

## 4. Applied Risk Classification Matrix


| Historical Pattern                              | Severity | Likelihood | Relevance | Priority Score | Priority Level |
|-------------------------------------------------|----------|------------|------------|----------------|----------------|
| Redlining legacy effects                        | 3        | 3          | 3          | 9             | Critical       |
| Proxy discrimination via ZIP code               | 3        | 3          | 3          | 9             | Critical       |
| Historical repayment data shaped by access bias | 3        | 2          | 3          | 8             | High           |
| Credit invisibility for marginalized users      | 2        | 3          | 3          | 8             | High           |
| Intersectional underrepresentation              | 2        | 2          | 2          | 6              | Medium         |

---

## 5. Resulting Design Decisions

Based on the matrix scoring, the team implemented the following changes before model training:
- Removed ZIP code from feature set
- Conducted structured proxy audit
- Redefined target variable to reduce access bias
- Required intersectional performance reporting
- Implemented monitoring for feedback loop dynamics
