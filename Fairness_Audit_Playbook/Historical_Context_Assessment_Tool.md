# Historical Context Assessment Tool

## 1. Introduction

The Historical Context Assessment Tool helps **identify historically rooted fairness risks early—before they are embedded in system design, data pipelines, or optimization goals**. By focusing on root causes such as historical power structures, institutional practices, and representational choices, it shifts fairness assessment from a post-hoc check to a foundational design practice.

As the first component of the Fairness Audit Playbook, the tool is used prior to finalizing data collection and model training, and its outputs guide later decisions on fairness definitions, metrics, data audits, and mitigation strategies.

## 2. Assignment Context

I work as a staff engineer at a technology company deploying AI systems across multiple products. An engineering team is scoping an AI-powered internal loan application system that enables users to purchase products and pay in installments.

The team recognizes that lending-related systems are historically sensitive and has requested support in identifying fairness risks early in development. Initial discussions reveal that a purely technical audit would be insufficient without understanding the historical context of financial discrimination.

I propose developing a structured tool that:
- Guides teams through historically informed analysis
- Translates social and historical insights into concrete technical risks
- Fits within standard engineering workflows.  

Recognizing that this challenge applies broadly across teams and domains, I formalized this approach as the Historical Context Assessment Tool (HCAT).

## 3. Objectives

- Translating historical discrimination research into actionable engineering methodology
- Mapping historical patterns to specific AI system risks
- Communicating societal and historical issues to technical audiences
- Balancing analytical rigor with practical usability in business environments

## 4. Requirements Overview

The Historical Context Assessment Tool includes four components:

1. **Structured Questionnaire** - Identifies historically relevant discrimination patterns and their mechanisms.  
2. **Risk Classification Matrix** - Prioritizes risks based on severity, likelihood, and relevance.  
3. **User Documentation** - Guides teams on when and how to apply the tool.  
4. **Applied Case Study** - Demonstrates use of the tool for an internal loan application system.

## 5. Historical Context Assessment Tool

### 5.1 Structured Historical Context Assessment Questionnaire

This questionnaire should be completed collaboratively by engineers, product owners, and (where possible) domain experts. Answers must be documented.

#### Section 1: Domain and Application Context

**1.1 Application Domain Identification**

- What domain does this system operate in (e.g., lending, hiring, healthcare)?
- What specific decision or recommendation will the system produce?
- Who benefits from correct predictions, and who is harmed by errors?

**1.2 Historical Discrimination in the Domain**

- What documented discrimination patterns exist in this domain?
- Explicit (e.g., redlining, exclusionary lending criteria)
- Implicit (e.g., disparate impact through “neutral” policies)
- Which groups were historically advantaged or disadvantaged?

**1.3 Institutional and Regulatory History**

- How have laws, policies, or industry standards shaped outcomes in this domain?
- Which practices were legal but discriminatory, and how might their effects persist?

#### Section 2: Data and Representation Analysis

**2.1 Historical Data Sources**

- What historical data will inform this system (e.g., repayment data, defaults, transaction history)?
- Who generated this data, and under what institutional conditions?
- Which populations may be underrepresented or over-surveilled?

**2.2 Category Formation**

- How have key categories (e.g., creditworthiness, risk, default) been historically defined?
- Have these definitions changed, and if so, why?
- Do current categories reflect historical power structures?

**2.3 Measurement and Proxies**

- How were key variables historically measured?
- Do any features function as proxies for protected attributes (e.g., ZIP code, device type)?
- Does the meaning of these variables differ across demographic groups?

**2.4 Missing Data and Strategic Ignorance**

- Which groups have systematically less data?
- Are data gaps random, or shaped by access barriers and institutional neglect?
- How might missingness itself encode historical bias?

#### Section 3: Technology Transition and Amplification

**3.1 Prior Technological Systems**

- What non-AI systems previously served this function?
- How did those systems reinforce or mitigate inequities?

**3.2 Automation and Scale Effects**

- How might automation amplify historical bias compared to human decision-making?
- Does this system reduce discretion or conceal it behind technical abstraction?

**3.3 Feedback Loop Risks**

- Will system outputs influence future data collection?
- Could disparities compound over time through self-reinforcing cycles?

#### Section 4: Intersectionality and Differential Impact

**4.1 Intersectional Risk Identification**

- Which groups experience compounded marginalization in this domain?
- Would single-attribute analysis miss these risks?

**4.2 Representation at Intersections**

- Are intersectional groups sufficiently represented in data?
- How confident are we in performance estimates for these groups?

### 5.2 Historical Context Risk Classification Matrix

Each identified historical pattern is evaluated using the following dimensions:

**Matrix Dimensions**  
**Severity (1–3)**

- 3 (High): Impacts fundamental rights, access to credit, liberty, or life outcomes
- 2 (Medium): Produces significant opportunity or resource disparities
- 1 (Low): Produces differential experience with limited material harm

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

- 7–9 – Critical: Requires immediate mitigation before deployment.
- 5–6 – High: Requires mitigation before or shortly after launch.
- 3–4 – Medium: Requires monitoring and periodic review.
- 1–2 – Low: Documented for awareness; no immediate action required.


Example Historical Pattern Risk Classification Table

| Historical Pattern                               | Severity (1–3) | Likelihood (1–3) | Relevance (1–3) | Priority Score | Priority Level |
|------------------------------------------------|---------------|------------------|------------------|----------------|----------------|
| Redlining in financial services                | 3             | 3                | 3                | 9              | Critical       |
| Proxy discrimination via ZIP code              | 3             | 3                | 3                | 9              | Critical       |
| Income bias against non-traditional workers    | 2             | 3                | 3                | 6              | High           |
| Gender bias in income measurement               | 2             | 2                | 2                | 4              | Medium         |
| Age-based exclusion in lending products        | 2             | 2                | 1                | 4              | Medium         |
| Linguistic bias against non-native speakers    | 2             | 2                | 1                | 4              | Medium         |
| Religious bias in financial risk profiling     | 2             | 1                | 1                | 2              | Low            |

### 5.3 Usage Guide

**Step 1: Domain Research (1–2 hours)**

- Review historical discrimination literature relevant to the domain.
- Focus on mechanisms, not just outcomes.

**Step 2: Questionnaire Completion (1–2 hours)**

- Complete collaboratively.
- Explicitly document uncertainty and information gaps.

**Step 3: Risk Classification (30–60 minutes)**

- Score each historical pattern.
- Identify Critical (7–9) and High (5–6) risks.

**Step 4: Integration into Development**

- Feed high-priority risks into:
  - Feature selection constraints
  - Fairness metric choice
  - Evaluation design
  - Monitoring plans  

HCAT outputs become inputs to later fairness audits, not a standalone artifact.  


## 6. Case Study: Internal Loan Application System

**Context**

The system predicts eligibility and repayment risk for installment-based purchases.

**Key Findings Using HCAT**

**Identified Historical Patterns**

- Redlining and geographic exclusion in credit markets
- Income-based bias against non-traditional workers
- Credit invisibility for young and marginalized users

**High-Risk Mechanisms**

- ZIP code as racial and class proxy
- Historical repayment data shaped by unequal access to credit
- Feedback loops excluding denied users from future training data

**Priority Risks**

- Proxy discrimination via location (Critical)
- Outcome definition tied to historical access (High)
- Intersectional exclusion of low-income women and minorities (High)

**Resulting Actions**

- Redefined target variable to reduce access bias
- Replaced location features with direct affordability indicators
- Required intersectional evaluation before launch


