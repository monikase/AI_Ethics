# Historical Context Assessment Tool

## 1. Introduction

The Historical Context Assessment Tool helps **identify fairness risks early, before they become embedded in system design**, data, or optimization choices. It focuses on understanding historical patterns and structural inequalities that could shape the system.

As the **first step in the Fairness Audit Playbook, the tool is applied before data collection and model training**.   
Findings guide later decisions about fairness metrics, evaluation, and mitigation strategies.

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
4. **Appendix Applied Example** - Demonstrates how the tool can be implemented in a real system. (Internal loan application system).

## 4. Historical Context Assessment Tool

### 4.1 Structured Historical Context Assessment Questionnaire

This questionnaire should be completed collaboratively by engineers, product owners, and, where possible, domain experts.   
All responses must be documented.

---

### Section 1: Domain and Application Context

**1.1 Application Domain Identification**

- What domain does this system operate in (e.g., lending, hiring, healthcare)
- What specific decision or recommendation will the system produce
- Who benefits from correct predictions, and who is harmed by errors

**1.2 Historical Discrimination in the Domain**

- What documented discrimination patterns exist in this domain
- Explicit patterns such as exclusionary criteria  
  *(Explicit discrimination refers to direct and intentional exclusion of certain groups. These practices clearly state or enforce different treatment based on characteristics such as race, gender, religion, or nationality)*
- Implicit patterns such as disparate impact through neutral policies  
  *(Implicit discrimination refers to policies or practices that appear neutral but disproportionately disadvantage certain groups in practice. The unequal outcome may result from historical inequalities rather than explicit intent)*
- Which groups were historically advantaged or disadvantaged

**1.3 Institutional and Regulatory History**

- How have laws, policies, or industry standards shaped outcomes in this domain
- Which practices were legal but discriminatory, and how might their effects persist

----

### Section 2: Data and Representation Analysis

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
  *(Whether seemingly neutral variables may still encode sensitive or historically disadvantaged group information)*
- Does the meaning of these variables differ across demographic groups

**2.4 Missing Data and Structural Gaps**

- Which groups have systematically less data
- Are data gaps random or shaped by institutional barriers
- How might missingness encode historical bias

---

### Section 3: Technology Transition and Amplification

**3.1 Prior Technological Systems**

- What non-AI systems previously served this function
- How did those systems reinforce or mitigate inequities

**3.2 Automation and Scale Effects**

- How might automation amplify historical bias
- Does this system reduce discretion or conceal value judgments behind technical abstraction  
  *(Whether the system makes decisions appear purely technical and objective, even though they are based on human choices about what to measure, how to define success, and what counts as risk, and whether automation removes flexibility to consider individual circumstances)*

**3.3 Feedback Loop Risks**

- Will system outputs influence future data collection
- Could disparities compound over time through self-reinforcing cycles

---

### Section 4: Intersectionality and Differential Impact

**4.1 Intersectional Risk Identification**

- Which groups experience compounded marginalization  
  *(Which groups face overlapping forms of disadvantage, such as discrimination based on more than one characteristic at the same time, for example gender and race or age and disability, which together may create greater barriers than any single factor alone)*
- Would single-attribute analysis miss these risks

**4.2 Representation at Intersections**

- Are intersectional groups sufficiently represented in data
- How confident are we in performance estimates for these groups

---

### 4.2 Historical Context Risk Classification Matrix

Each identified historical pattern is evaluated using three dimensions:
 
- **Severity: Impact of this bias if perpetuated (1–3)**
  - 3 (High): Directly impacts fundamental rights or life outcomes.
  - 2 (Medium): Creates significant disparities in opportunities or resources.
  - 1 (Low): Creates differential experiences but with limited material impact.

- **Likelihood: Probability of this pattern manifesting in AI systems (1–3)**
  - 3 (High): Frequently appears in similar systems.
  - 2 (Medium): Occasionally appears.
  - 1 (Low): Rarely appears.

- **Relevance: Applicability to the specific AI system being developed (1–3)**
  - 3 (High): Direct applicability to system's domain/purpose.
  - 2 (Medium): Partial applicability to certain system components.
  - 1 (Low): Limited applicability but potential for manifestation.

- **Priority Score = Severity + Likelihood + Relevance**

- **Priority Level:**
  - 7–9 – Critical: Requires immediate mitigation before deployment
  - 5–6 – High: Requires mitigation before or shortly after launch
  - 3–4 – Medium: Requires monitoring and periodic review
  - 1–2 – Low: Documented for awareness. No immediate action required.

---

### \* *Methodology Example Matrix*

| Historical Pattern                             | Severity (1–3) | Likelihood (1–3) | Relevance (1–3) | Priority Score | Priority Level |
|------------------------------------------------|----------|------------|------------|----------------|----------------|
| Geographic exclusion in service allocation     | 3        | 3          | 3          | 9              | Critical       |
| Proxy discrimination via location data         | 3        | 3          | 3          | 9              | Critical       |
| Bias against non-traditional employment types  | 2        | 2          | 2          | 8              | High           |
| Underrepresentation in training data           | 2        | 2          | 3          | 12             | Critical       |
| Language-based exclusion in user interface     | 2        | 2          | 1          | 4              | Medium         |

---

### 4.3 Usage Guide

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

Historical Context Assessment Tool **outputs become inputs to later fairness audits**.  

---

### [Appendix 1_HCAT_Applied_Example: Internal Loan Application System](https://github.com/monikase/AI_Ethics/blob/main/Fairness_Audit_Playbook/1_HCAT_Applied_Example.md)

