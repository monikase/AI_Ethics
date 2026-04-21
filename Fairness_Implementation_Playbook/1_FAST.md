# Fair AI Scrum Toolkit 
_(Part 1 of the Fairness Implementation Playbook)_

## Purpose

Most teams build AI systems using Agile/Scrum but fairness is usually handled too late (or not at all).  

The **Fair AI Scrum Toolkit (FAST)** solves this by embedding fairness directly into **how teams already work:**

- into user stories
- into sprint planning
- into testing and validation
- into “Definition of Done”
  
**FAST makes fairness part of everyday development, not a separate activity.**  

## System Role in the Playbook

FAST is the **execution layer** of the Fairness Implementation Playbook.

It operationalizes:

- **Governance decisions (OIT)** → via Fairness Decision Records (FDRs)  
- **Technical strategies (AAC)** → via implementation tasks  
- **Regulatory requirements (RCG)** → via validation and evidence generation  

---

## Inputs & Outputs

### Inputs

- **From OIT (Organizational Integration Toolkit)**  
  - Fairness Decision Records (FDRs)  
  - Approved fairness definitions  
  - Metrics and thresholds  
  - Trade-offs and constraints  

- **From RCG (Regulatory Compliance Guide)**  
  - Risk classification (TRS, risk tier)  
  - Required validation rigor  
  - Documentation and audit requirements  

---

### Outputs

- **To AAC (Advanced Architecture Cookbook)**  
  - Identified bias issues requiring technical mitigation  
  - Context for selecting architecture-specific recipes  

- **To OIT**  
  - Fairness metrics and implementation results  
  - Escalations and trade-off feedback  

- **To RCG**  
  - Model cards  
  - Fairness test reports  
  - Audit evidence and logs  

---

## Core Principle

> **No fairness work may be executed without a linked Fairness Decision Record (FDR).**

FAST does not define fairness — it **implements governance-approved decisions**.

---


## Business Value of Integrating Fairness into Scrum 

Embedding fairness within agile development is both a risk‑reduction and value‑creation strategy:  
  
- **Risk Reduction**  
  Early detection of bias prevents costly remediation, regulatory exposure, and reputational harm.  
- **Improved Product Quality**   
  Fairness‑aware systems perform more reliably across diverse populations and operational contexts.  
- **Regulatory Readiness**  
  Fairness validation, documentation, and accountability are built into workflows, aligning with emerging AI regulations (e.g., EU AI Act).  
- **Team Efficiency and Clarity**  
  Clear fairness responsibilities reduce ambiguity and last‑minute rework.  
- **Scalability**  
  A standardized approach ensures fairness practices scale consistently across teams, products, and system types.  

## Connection to Other Playbook Components: 

This toolkit integrates with the broader Fairness Implementation Playbook:  

- **Organizational Integration Toolkit (2_OIT.md)**   
  FAST provides the team‑level execution practices required for organization‑wide fairness governance.
- **Advanced Architecture Cookbook (3_AAC.md)**  
  Architecture‑specific fairness techniques may be reviewed and applied within FAST ceremonies and checkpoints.  
- **Regulatory Compliance Guide (4_RCG.md)**  
  Scrum artifacts and fairness evidence produced using this toolkit directly support governance gates, documentation requirements, and audit trails defined in the RCG.  

## How to Use This Toolkit

For organizations new to fairness:

#### Step 1: Start small
Pick **one feature** with potential fairness risk

#### Step 2: Apply FAST basics
- Rewrite user story with fairness (SAFE)
- Add fairness acceptance criteria (FAIR)

#### Step 3: Add fairness tasks
- Audit  
- Test  
- Mitigation  

#### Step 4: Enforce Definition of Done
Feature is NOT complete without fairness validation

#### Step 5: Iterate
Improve each sprint using retrospectives

## Toolkit Overview

#### [1. Scrum Artifact Modifications](#artifacts)
#### [2. Definition of Done (DoD) Framework](#dod)
#### [3. Sprint Planning & Execution Framework](#planning)
#### [4. Ceremonies & Checkpoints](#ceremonies)
#### [5. Role-Based Responsibilities](#roles)
#### [6. Intersectionality Integration Layer](#intersectionality)
#### [7. Evaluation Metrics](#evaluation)
#### [8. Implementation Workflow](#workflow)
#### [9. Core Principles](#principles)
#### [10. References](#refs)

---

> **Note:** The examples provided throughout this toolkit are illustrative and simplified for clarity.  
> They are designed to demonstrate how fairness concepts can be operationalized within Scrum workflows, rather than representing fully implemented production systems.

---

<a id="artifacts"></a>
## 1️⃣ Scrum Artifact Modifications 

**Objective:** Embed fairness directly into requirements and backlog items.

### 1.1 Fairness-Enhanced User Stories (SAFE Framework)

Traditional user stories capture functionality but ignore differential impacts.    
The SAFE framework extends user stories to make fairness explicit and actionable.  

---

### Template
As a **[user]**,  
  
I want **[functionality]**,  
  
so that **[benefit]**,  
  
while ensuring **[fairness goal]** across **[protected + intersectional groups]**.

---

> #### _Illustrative Example_
>  
> As a **recruiter**,  
> I want **candidates ranked by relevance**,  
> so that I can **shortlist efficiently**,  
> while **ensuring equivalent ranking accuracy across gender, age, and their intersections**.   


### SAFE Breakdown

| Element | Meaning |
|--------|-------------|
| S - Specific Protected Attributes | Who could be affected by bias _(Identify relevant groups (e.g., gender, age, ethnicity))_ |
| A - Actionable Fairness Definition | Define fairness concept _(e.g., equal opportunity)_  |
| F - Feature Integration Point | Where fairness applies in the feature _(Connects intervention techniques to specific product functionality)_ |
| E - Expected Outcome Measures | How fairness will be validated  |

🔗 **Playbook Connection**  
- Fairness Audit findings → requirements    
- Fairness Intervention → measurable outcomes  

---

### 1.2 Fairness Acceptance Criteria (FAIR Framework)

Acceptance criteria define **how fairness is validated**, not just intended. 

### FAIR Breakdown

| Element | Purpose |
|--------|--------|
| F | Fairness Metrics Thresholds |
| A | Auditing Requirements |
| I | Intersectional Analysis |
| R | Reporting and Documentation |

#### Example Criteria

- Metric difference ≤ defined threshold 
- Intersectional evaluation completed where feasible
- Results documented in model card

> #### _Illustrative Example_
>   
> - Demographic parity difference ≤ 0.05  
> - True positive rate difference ≤ 0.03 across groups  
> - Intersectional subgroup evaluation completed  
> - Results documented in model card  

---

### 1.3 Backlog & Documentation Extensions

Make fairness visible in daily work:

- Tag stories: `FAIRNESS`, `HIGH-RISK`, `INTERSECTIONAL`
- Add fairness subtasks:
  - bias audit  
  - subgroup testing  
  - mitigation  
- Include fairness notes:
  - assumptions  
  - risks  
  - affected populations  

---

<a id="dod"></a>
## 2️⃣ Definition of Done (DoD) Framework  

A feature is complete **only when fairness validation is complete**.

**Completion of the DoD is a mandatory** precondition for progression through governance gates. Features failing fairness validation must not advance to deployment.  

### Minimum Requierements

#### Data

- Representation across groups validated  
- Missing data patterns analyzed per group  
- Bias sources documented  

#### Model

- Fairness metrics meet thresholds  
- Performance evaluated across subgroups and intersections  
- Counterfactual or sensitivity analysis conducted (where applicable)  
- Bias mitigation applied if needed  
- Model card includes:
  - fairness metrics  
  - limitations  
  - assumptions  

#### Interface

- Tested with diverse users  
- No usability gaps across groups  
- Explanations understandable across demographics

**Resources & Tools**
- [Model Cards for Model Reporting (Mitchell et al., 2019)](https://arxiv.org/abs/1810.03993)   
- [Datasheets for Datasets (Gebru et al., 2018)](https://arxiv.org/abs/1803.09010) 

---

<a id="planning"></a>
## 3️⃣ Sprint Planning & Execution Framework  

**Objective:** Allocate and deliver fairness work systematically.

### 3.1 Fairness Capacity Allocation

Reserve **15–30% of sprint capacity** for fairness work.  
Capacity allocation should scale with **system risk tier** as defined in governance frameworks.  

### 3.2 Fairness Task Taxonomy

- **Analysis:** audits, subgroup and intersectional evaluation
- **Implementation:** mitigation techniques, feature adjustments
- **Validation:** testing, documentation, evidence generation   

### 3.3 Fairness Backlog Prioritization

Prioritization incorporates:

1. **Fairness Impact**  
   How significantly a feature could affect different demographic groups. 
2. **Bias Risk**  
   The likelihood of undetected bias entering the system.  
3. **Harm Severity**  
   The potential consequences of biased outcomes.  
4. **Regulatory Exposure**    
   Legal or compliance risks from bias issues.    

### 3.4 Sprint Planning Meeting Adaptations
 
Key adaptations include:  

1. **Fairness Risk Assessment**  
   Structured evaluation of each planned feature's bias potential  
2. **Capacity Earmarking**  
   Explicit allocation of sprint capacity to fairness tasks  
3. **Fairness Task Identification**  
   Systematic process for identifying necessary fairness tasks  
4. **Role Assignment**  
   Clear fairness responsibilities for each team member  
5. **Fairness Checkpoint Definition**  
   Explicit points during the sprint for fairness validation   

### 3.5 Daily Execution and Monitoring

Key components include:  

1. **Fairness Standup Prompts**  
   Explicit questions about fairness progress and blockers  
2. **Fairness Progress Visualization**  
   Visible tracking of fairness metrics alongside functional progress   
3. **Fairness Blocker Escalation**    
   Clear protocol for raising and addressing fairness blockers  
4. **Mid-Sprint Fairness Checkpoints**  
   Scheduled review points for fairness validation  


**Resources & Tools**

- [Google Responsible AI Practices](https://ai.google/responsibilities/responsible-ai-practices/)

---

<a id="ceremonies"></a>
## 4️⃣ Ceremonies & Checkpoints  

### 4.1 Sprint Planning

Standard sprint planning covers estimation and capacity.  
**Enhanced planning adds fairness:**

- **Fairness Story Review**  
  Review each story for potential bias risks  

- **Fairness Task Identification**  
  Define required audits, tests, and mitigation steps  

- **Fairness Capacity Allocation**  
  Reserve explicit capacity for fairness work  

- **Fairness Checkpoint Definition**  
  Define when fairness validation will occur during sprint  

### 4.2 Daily Execution

- Explicit fairness prompts
- Visible fairness progress tracking
- Escalation of blockers

Add fairness prompts:

- Are there any fairness blockers?  
- Are fairness tasks progressing as planned? 

### 4.3 Sprint Review / Demo

Include:  

- **Fairness Metric Presentations**  
   Visualizing key fairness metrics across demographic groups  
- **Disaggregated Performance Reports**  
   Showing system performance for different protected attributes and intersections  
- **Bias Mitigation Demonstrations**  
   Explaining implemented fairness interventions and their results  
- **Remaining Fairness Risks or Debt**  
   Transparently discussing unresolved fairness issues    

### 4.4 Sprint Retrospective Techniques

1. **Fairness-Specific Prompts:** Questions focused explicitly on fairness work such as:  
- "What helped us detect bias issues early?"
- "Where did we miss potential fairness problems?"
- "How effectively did we implement fairness acceptance criteria?"

2. **Structured Analysis Exercises:**  
- Fairness Timeline: Mapping when bias issues appeared and why
- Intersectionality Matrix: Examining blind spots across demographic intersections
- Fairness Impediment Analysis: Identifying systemic barriers to equity work

3. **Fairness Process Improvements:**  
- Targeted changes to fairness workflows
- Updates to fairness testing procedures
- Refinements to fairness documentation  

### 4.5 Mid-Sprint Fairness Checkpoints

1. **Pre-Implementation Design Reviews**  
   Evaluating fairness implications before coding begins  
2. **Data Pipeline Validation**  
   Verifying fairness properties of data transformations  
3. **Model Training Reviews**  
   Examining fairness metrics during early training iterations  
4. **Integration Fairness Tests**  
   Testing for bias after component integration   

### 4.6 Fairness Demonstration Techniques

1. **Fairness Dashboards**  
   Interactive visualizations showing performance across demographic groups  
2. **Counterfactual Demonstrations**  
   Showing how the system responds to identical inputs that differ only in protected attributes  
3. **Real-World Impact Scenarios**  
   Illustrating how bias patterns would affect actual users  
4. **Before/After Comparisons**  
   Demonstrating fairness improvements through intervention   

---

<a id="roles"></a>
## 5️⃣ Role-Based Responsibilities  

#### Product Owner
- Define fairness requirements in user stories  
- Prioritize fairness work in backlog  
- Balance fairness with business goals  

#### Scrum Master
- Ensure fairness is included in ceremonies  
- Track fairness blockers  
- Escalate unresolved bias issues to leadership   

#### Developers / Data Scientists
- Implement bias testing within development  
- Research and apply mitigation techniques  
- Follow fairness-enhanced Definition of Done  
- Document testing methodologies and results  
- Report discovered bias issues promptly  
- Participate in fairness skill development  
- Conduct bias audits for model iterations  
- Interpret fairness metrics for non-technical stakeholders  

#### Shared Responsibility

- Fairness is owned by the entire team  
- No single role is solely responsible 

---

<a id="intersectionality"></a>
## 6️⃣ Intersectionality Integration Layer  

Fairness must account for **interacting attributes**, not only single dimensions.

#### Implementation

- Intersectional groups included in stories and acceptance criteria
- Testing prioritizes high‑risk intersections
- Limitations and statistical constraints are explicitly documented

Where intersectional analysis is infeasible, the rationale must be recorded as compliance evidence.

#### Practical Constraints

Due to data limitations:

- Prioritize high-risk intersections  
- Use hierarchical modeling  
- Report uncertainty    
  
---

<a id="evaluation"></a>
## 7️⃣ Evaluation Metrics  

#### Process Metrics

- Percentage of stories with fairness criteria
- Fairness task completion rate
- Fairness artifacts accepted at governance gates without rework  

#### Outcome Metrics

- Disparity reduction
- Bias incidents in production
- Time to resolve fairness issues

#### Target Benchmarks (High-Risk Systems)

- 100% fairness coverage in user stories  
- ≥95% fairness task completion  
- 0 high-severity bias post-deployment  

**Resources & Tools**
- [Holistic AI](https://www.holisticai.com/) – Fairness evaluation and governance platform  
- [OECD AI Metrics Framework](https://oecd.ai/en/catalogue/metrics)  
  
---

<a id="workflow"></a>
## 8️⃣ Implementation Workflow  

1. Assess current practices
2. Introduce fairness‑enhanced artifacts and DoD
3. Pilot on high‑risk features
4. Scale across teams
5. Continuously refine through retrospectives

---

<a id="principles"></a>
## 9️⃣ Core Principles  

- Fairness is embedded, not appended
- Risk determines rigor
- Fairness must be measurable and documented
- Intersectional impacts are evaluated proportionally
- Validation blocks deployment
- Compliance evidence is a by‑product of development
- Continuous improvement is mandatory 

---

This toolkit operationalizes fairness at the team level, ensuring that daily development practices generate the evidence, decisions, and accountability required for trustworthy and compliant AI systems.

---

<a id="refs"></a>
## 10. References

### Fairness in Machine Learning

- Barocas, S., Hardt, M., & Narayanan, A. (2019).  
  *Fairness and Machine Learning: Limitations and Opportunities.*  
  https://fairmlbook.org  

- Mehrabi, N., Morstatter, F., Saxena, N., Lerman, K., & Galstyan, A. (2021).  
  *A Survey on Bias and Fairness in Machine Learning.*  
  ACM Computing Surveys.  

- Verma, S., & Rubin, J. (2018).  
  *Fairness Definitions Explained.*  
  IEEE/ACM International Workshop on Software Fairness.  

---

### Responsible AI & Documentation

- Mitchell, M. et al. (2019).  
  *Model Cards for Model Reporting.*  
  https://arxiv.org/abs/1810.03993  

- Gebru, T. et al. (2018).  
  *Datasheets for Datasets.*  
  https://arxiv.org/abs/1803.09010  

- Google.  
  *Responsible AI Practices.*  
  https://ai.google/responsibilities/responsible-ai-practices/  

---

### Agile & Software Engineering

- Schwaber, K., & Sutherland, J. (2020).  
  *The Scrum Guide.*  
  https://scrumguides.org  

- Beck, K. et al. (2001).  
  *Manifesto for Agile Software Development.*  
  https://agilemanifesto.org  

---

### Governance & Organizational AI

- Floridi, L. et al. (2018).  
  *AI4People—An Ethical Framework for a Good AI Society.*  
  Minds and Machines.  

- Raji, I. D. et al. (2020).  
  *Closing the AI Accountability Gap: Defining an End-to-End Framework for Internal Algorithmic Auditing.*  
  FAT* Conference.  

---

### Regulatory & Compliance

- European Union (2024).  
  *EU Artificial Intelligence Act.*  

- European Union (2016).  
  *General Data Protection Regulation (GDPR).*  

- OECD (2021).  
  *OECD Framework for the Classification of AI Systems.*  
  https://oecd.ai  

---

### Fairness in Specific Architectures

- Bender, E. M. et al. (2021).  
  *On the Dangers of Stochastic Parrots: Can Language Models Be Too Big?*  
  FAccT Conference.  

- Ekstrand, M. D., Burke, R., & Diaz, F. (2022).  
  *Fairness in Recommendation Systems.*  
  Foundations and Trends in Information Retrieval.  

---

### Monitoring, Auditing, and Lifecycle Fairness

- Sculley, D. et al. (2015).  
  *Hidden Technical Debt in Machine Learning Systems.*  
  NeurIPS.  

- Breck, E. et al. (2017).  
  *The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction.*  
  IEEE Big Data.  

---

### Additional Tools & Industry Practices

- Holistic AI.  
  *Fairness Evaluation and Governance Platform.*  
  https://www.holisticai.com  

- OECD AI Metrics Framework  
  https://oecd.ai/en/catalogue/metrics  

---
