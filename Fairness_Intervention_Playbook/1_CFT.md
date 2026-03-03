# Causal Fairness Toolkit
A Practical Methodology for Identifying and Fixing Algorithmic Bias

## 1. Introduction

Machine learning systems sometimes produce different outcomes for different groups of people. But seeing a difference does not automatically tell us whether the system is unfair - or what is causing the difference.  

Disparities can happen for many reasons. A model might directly use a protected attribute _(like gender)_, rely on variables that indirectly reflect it _(such as job type or part-time status)_, reflect patterns from historical inequality, or use legitimate risk factors. Without understanding the real cause, fairness fixes may only treat the symptoms instead of solving the problem.  

The **Causal Fairness Toolkit provides a practical step-by-step method to help teams understand where unfairness comes from and how to address it properly**. It helps teams:   

- Map how protected attributes may influence predictions
- Check whether a decision would change **if only a protected attribute were different, while everything else stayed the same**.
- Separate legitimate prediction factors from discriminatory ones
- Choose the right place in the system to intervene
- Make thoughtful decisions even when information is incomplete

Instead of applying simple statistical adjustments, this toolkit focuses on understanding the reasons behind disparities so that interventions are more precise, transparent, and effective.  

## 2. Toolkit Overview 

The toolkit consists of four components:

1. **Causal Modeling Template**   
2. **Counterfactual Analysis Framework**   
3. **Intervention Point Identification Method**   
4. **Limited Information Adaptation Guidelines**    

Each step builds on the previous one.

***

## 1️⃣ Causal Modeling Template  
→ Map how protected attributes influence predictions.

---

### Variable Identification Guide

---

### A. Protected Attributes Identification
1. **Primary protected attributes:**  
[List legally protected characteristics relevant to this application]  
_[(e.g., gender, race, age)]_    
2. **Intersectional categories:**  
[List relevant combinations of protected attributes]  
 _[(e.g., gender × age)]_     

Document why each attribute is relevant in this context.  

***

### B. Mediator Variable Identification
Mediators are variables that are influenced by protected attributes and also influence the outcome.  
These variables may transmit structural inequalities.  
1. **Variables directly influenced by protected attributes:**  
[List variables]  
_[(e.g., employment history, income level)]_   
3. **Evidence for causal relationship:**    
[Provide brief justification for each variable - domain expertise, research findings, or data patterns]    
_[(e.g., research on wage gaps, observed career breaks)]_        

For each mediator, consider:  
- Does this variable reflect historical or structural inequality?
- Should its influence on the outcome be preserved or adjusted?

***

### C. Confounding Variable Identification
Confounders are variables that influence both protected attributes and outcomes, potentially creating misleading associations.  
1. **Variables that may affect both protected attributes and outcomes:**  
[List variables]  
_[(e.g., socioeconomic background, neighborhood economic conditions)]_  
3. **Evidence for confounding role:**  
[List evidences]  
_[(e.g., research linking socioeconomic status to both education and loan approval)]_  

For each potential confounder, consider:
- Does this variable create a spurious relationship?
- Is it measured in the data?
- Could omitting it bias fairness conclusions?

---

### D. Proxy Variable Identification
Proxy variables are correlated with protected attributes and may indirectly encode them.  
1. **Variables correlated with protected attributes:**  
[List variables]  
_[(e.g., part-time employment status, zip code)]_  
3. **Evidence for correlation:**  
[Brief justification per variable]  
_[(e.g., statistical correlation, labor market patterns)]_   
5. **Common causes explaining correlation:**   
[Explanation per variable]  
_[(e.g., occupational segregation, residential segregation)]_  

---

### E. Outcome Variable Identification
Define the system’s decision or prediction.  
1. **Decisions or predictions made by the system:**  
[List outcomes]  
_[(e.g., loan approval decision, risk score)]_  
3. **Evaluation metrics used:**  
[List metrics]  
_[(e.g., approval rate, default rate, accuracy)]_    

---

### F. Legitimate Predictor Identification  
Variables that should influence the outcome because they are directly related to the task.  

1. **Variables that should influence outcomes:**  
[List variables]  
_[(e.g., debt-to-income ratio, savings history, payment history)]_  
3. **Justification for legitimacy:**  
[Brief justification per variable]  
_[(e.g., directly measures repayment ability)]_  

Document justification for each variable.  

---

### Causal Graph Construction

---

After identifying variables, construct a **Directed Acyclic Graph (DAG)** to visually represent how variables influence one another.  

- **Use directed arrows to represent causal relationships.**    
> _Example:_   
> **Gender → Employment History → Default Risk → Loan Approval**   
> _(Gender may influence employment history, which affects default risk.)_  

- **Use bidirectional dashed arrows to represent correlations without direct causation.**   
> _Example:_  
> **Gender ↔ Part-Time Status**  
> _(Part-time work may correlate with gender, but gender does not directly “cause” part-time status in a strict biological sense — both may reflect broader social patterns.)_  

- **Distinguish node types visually (when drawing the graph):**
  - **Protected attributes:** _[e.g., Gender]_
  - **Mediators:** _[e.g., Income Level, Employment History]_
  - **Proxy variables:** _[e.g., Industry Sector]_
  - **Confounders:** _[e.g., Socioeconomic Background]_
  - **Outcomes:** _[e.g., Loan Approval Decision]_

- **Document causal assumptions with justification for each arrow.**  
> _Example justification:_   
> - "Gender → Income" based on documented wage gap research.  
> - "Income → Default Risk" based on financial risk modeling evidence.  

- **Identify critical paths that may transmit discrimination.**  
> _Example critical paths:_  
> - Gender → Income → Debt-to-Income Ratio → Approval  
> - Gender → Employment Gap → Risk Score → Approval  

These paths should later be evaluated through counterfactual analysis to determine whether they represent legitimate influence or discrimination.

#### DAG Example (using mermaid)  

```mermaid
flowchart LR

%% ===== Nodes (keep original structure) =====
Socioeconomic[Socioeconomic Background]
Gender[Gender]
Income[Income]
Employment[Employment History]
PartTime[Part-Time Status]
DefaultRisk[Default Risk]
Loan[Loan Approval]

%% ===== Causal Relationships (solid arrows) =====
Socioeconomic --> Income
Gender --> Income
Gender --> Employment
Income --> DefaultRisk
Employment --> DefaultRisk
DefaultRisk --> Loan

%% ===== Correlation / Proxy Relationships (dashed arrows) =====
Gender -.-> PartTime

%% Optional: bidirectional correlation (no direct causation)
Socioeconomic -.-> Gender
Gender -.-> Socioeconomic

%% ===== Styling Classes =====
classDef protected fill:#ffe6f0,stroke:#cc0066,stroke-width:2px;
classDef mediator fill:#e6f2ff,stroke:#0066cc,stroke-width:2px;
classDef proxy fill:#fff5e6,stroke:#ff9900,stroke-dasharray:5 5;
classDef confounder fill:#f2f2f2,stroke:#666666,stroke-width:2px;
classDef outcome fill:#e6ffe6,stroke:#009933,stroke-width:3px;

%% ===== Assign Classes =====
class Gender protected;
class Income,Employment mediator;
class PartTime proxy;
class Socioeconomic confounder;
class Loan outcome;
```

**Legend:**  
- Pink → Protected attributes  
- Blue → Mediators  
- Orange dashed border → Proxy variables  
- Grey → Confounders  
- Green → Outcomes  

Solid arrow (→) — Causal relationship  
Dashed arrow (-.-→) — Correlation / proxy relationship  

---

## 2️⃣ Counterfactual Analysis Framework

→ Test whether predictions would change if only the protected attribute changed.  

---

### Counterfactual Query Formulation  

---

### 1. **Base case description**   
Describe the **real individual and the model’s actual decision**.  
- **Individual characteristics:**  
[Relevant non-protected attributes]   
_Example: [Credit score: 720, Income: €45,000, Debt-to-income ratio: 28%, Savings: €12,000, 2-year employment gap]_
- **Protected attribute value:**  
[Current value]   
_[Gender: Female]_   
- **System prediction:**  
[Current prediction/decision]  
_[Loan Denied – predicted default risk: 18%]_  

---

### 2. **Counterfactual scenario:**  
Create the **“what if” version of the same person**.

- **Modified protected attribute:**  
[Counterfactual value]  
_[Gender: Male]_       
> Ask: If this exact same applicant were male instead of female, what would happen?  

- **Variables that should remain constant:**   
[List causally independent variables]  
  
> Characteristics that should not change just because gender changes (they are not caused by gender in our model):  
> - _[Credit score: 720]_   
> - _[Savings: €12,000]_  
> - _[Debt-to-income ratio: 28%]_  
>
> These stay fixed. 


- **Variables that should change:**  
[List descendants of protected attributes]  

> These are variables that could be influenced by gender in the real world (based on our causal model):  
> - _[Employment history interpretation]_
> - _[Income assessment weight]_
> - _[Income stability scoring]_  
>
>_Because our causal model shows gender can influence how employment gaps or income stability are evaluated._  

---

### 3. **Fairness evaluation:**
Compare the outcomes.  

- **Expected outcome under counterfactual:**  
[Prediction if fair]

> _Example:_ If the model does not unfairly use gender, then:  
>
> The prediction should remain Loan Denied (18%)  
> or  
> The risk score should stay essentially the same.  


- **Actual model behavior:**  
[What model actually does]

> When we simulate the counterfactual:
> - Predicted default risk becomes 13%
> - Loan decision becomes Approved


- **Discrepancy analysis:**  
[Compare expected vs. actual]   

  - Did prediction change?  
  - If yes → potential counterfactual unfairness

> _Example:_ 
> | Scenario                 | Predicted Risk | Decision |
> |--------------------------|---------------|----------|
> | Female (real case)       | 18%           | Denied   |
> | Male (counterfactual)    | 13%           | Approved |
>
> This means:
> - The decision changes only because gender changed.
> - Therefore, the model is counterfactually unfair for this individual.

---

### **Path-Specific Effect Analysis**  
Counterfactual fairness tells us whether discrimination exists.  
Path-specific analysis helps us understand **where it comes from**. 

---

### 1. **Identify specific causal pathways** from protected attributes to outcomes  
Start by mapping all paths from the protected attribute _(e.g., gender)_ to the outcome _(e.g.,loan approval)_.  

> _Example paths in the loan system:_
>   
> **1. Gender → Employment History → Default Risk → Approval**  
> **2. Gender → Income Level → Debt-to-Income Ratio → Default Risk → Approval**  
> **3. Gender → Part-Time Status → Income Stability → Default Risk → Approval**  
> **4. Gender → Approval (direct path)**  
>  
> Each of these is a separate mechanism through which disparity may occur.  

---

### 2. **Classify paths** as legitimate or problematic based on domain knowledge.
This step requires **normative judgment** - not just technical analysis.  

You must decide:  
- Does this pathway reflect legitimate risk?
- Or does it reflect structural or historical bias?

> | Path                                                  | Possible Classification       | Why?                                                                 |
> |-------------------------------------------------------|------------------------------|----------------------------------------------------------------------|
> | Gender → Employment History → Default Risk            | ⚠ Potentially Problematic    | Career breaks may reflect caregiving responsibilities, not actual repayment ability |
> | Gender → Income → Debt Ratio → Default Risk           | ⚠ Partially Problematic      | Income differences may reflect systemic wage gaps                   |
> | Gender → Part-Time Status → Default Risk              | ❌ Problematic               | Part-time status may act as a gender proxy                          |
> | Gender → Approval (direct)                            | ❌ Clearly Unfair            | No legitimate reason for direct gender influence                    |
 
This step must involve:  
- Legal review
- Domain experts
- Business stakeholders

It cannot be decided by code alone.  

---

### 3. Quantify the contribution of each path to observed disparities.  
Measure how much each path contributes to the overall disparity.

> _Example findings:_
>   
> - _Employment history pathway → 40% of disparity_
> - _Income pathway → 25%_
> - _Part-time proxy pathway → 20%_
> - _Direct discrimination → 15%_

This tells you which mechanisms matter most.  
Without this step, you might overcorrect small effects and ignore major ones.  

---

### 4. Focus interventions on problematic paths while preserving legitimate paths.
The goal is **surgical intervention**, not destroying model performance.  

Instead of forcing demographic parity, you:  
- Remove or adjust problematic paths
- Preserve legitimate predictive information

> _Example Interventions_  
> | Problematic Path        | Intervention                                      |
> |-------------------------|---------------------------------------------------|
> | Employment gap penalty  | Replace with "total relevant experience"          |
> | Raw income weight       | Normalize income relative to loan size            |
> | Part-time status proxy  | Replace with direct income stability metric       |

---

## 3️⃣ **Intervention Point Identification Method**
The Intervention Point Identification Method helps teams decide where to make changes in the ML pipeline based on the results of the causal analysis. It connects different types of bias to the right kind of intervention.

---

### Causal Pattern Decision Tree

---

#### Intervention Selection Decision Tree

1. If **direct discrimination is present** (direct path from protected attribute to outcome):  
   a. Is the protected attribute explicitly used as a feature?
      - Yes → Apply in-processing constraints or remove the attribute
      - No → Investigate implicit direct discrimination through model architecture

2. If **proxy discrimination is present** (path through correlated but not causally related variables):  
   a. Can the proxy variables be identified?  
      - Yes → Consider pre-processing approaches to transform these variables
      - No → Apply in-processing regularization to minimize proxy use

3. If **mediator discrimination is present** (path through variables causally influenced by protected attributes):  
   a. Are the mediator variables legitimate predictors for the task?  
      - Yes → Consider using multi-objective optimization to balance fairness with prediction
      - No → Apply pre-processing to remove the influence of protected attributes on these variables

4. If **outcome discrimination is present** (disparities in model outputs):  
   a. Are the disparities consistent across subgroups?  
      - Yes → Consider post-processing approaches like threshold optimization
      - No → Apply more targeted interventions based on causal structure


---

```mermaid
flowchart TD

A[Start] --> B{Direct discrimination?}
B -->|Yes| C{Protected attribute explicitly used?}
C -->|Yes| D[Remove attribute or apply in-processing constraints]
C -->|No| E[Investigate implicit discrimination in model architecture]

B -->|No| F{Proxy discrimination present?}
F -->|Yes| G{Proxy variables identifiable?}
G -->|Yes| H[Apply pre-processing transformation]
G -->|No| I[Use in-processing regularization]

F -->|No| J{Mediator discrimination present?}
J -->|Yes| K{Are mediators legitimate predictors?}
K -->|Yes| L[Use multi-objective optimization]
K -->|No| M[Adjust or remove mediator influence]

J -->|No| N{Outcome discrimination present?}
N -->|Yes| O{Disparities consistent across subgroups?}
O -->|Yes| P[Apply post-processing such as threshold adjustment]
O -->|No| Q[Apply targeted intervention based on causal structure]

N -->|No| R[No fairness intervention required]
```

---

### 4️⃣ Limited Information Adaptation

Real-world data is incomplete.  

Apply:  

#### 1. Test Multiple Plausible Models
Test fairness under different causal assumptions when causal structure is uncertain.

#### 2. Sensitivity Analysis
Perform sensitivity analysis to identify robust intervention decisions.  
- How strong must hidden confounding be to eliminate the observed effect?
- Use E-values or bounding methods.

#### 3 Intersectional Modeling
Prioritize resolving uncertainties that would change intervention recommendations.  
- Use hierarchical models when subgroup data is sparse.
- Quantify uncertainty explicitly.

#### 4 Transparent Documentation
Document assumptions explicitly to enable future refinement.  
Always document:  
- Assumptions
- Uncertainties
- Rationale for intervention choices

---

## 7. Practical Workflow Summary

1. Identify variables
2. Build causal graph
3. Run counterfactual queries
4. Decompose pathways
5. Select targeted interventions
6. Quantify uncertainty
7. Re-evaluate after intervention

---

## 8. Core Principle

Fairness interventions should:

- Address root causes
- Preserve legitimate prediction
- Be transparent about uncertainty
- Be guided by causal reasoning, not correlation alone





