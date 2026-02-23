# Bias Source Identification Tool (BSIT)

## 1. Purpose

The Bias Source Identification Tool (BSIT) provides a structured methodology for identifying, classifying, and prioritizing bias entry points throughout the machine learning lifecycle.

The tool ensures that fairness assessments address root causes rather than observable symptoms by systematically mapping bias sources across:

- Data Collection and Representation
- Algorithm Design and Optimization
- Feedback Loops and Dynamic Effects
- System Interaction and Deployment Contexts

BSIT is applied after:
- Historical Context Assessment
- Fairness Definition Selection

It operationalizes fairness goals into bias-source diagnostics.

---

## 2. Bias Taxonomy

Bias sources are classified into four lifecycle domains.

---

### A. Data-Level Biases

#### 1. Historical Bias
**Definition:** Data reflects pre-existing societal inequities.

**Indicators:**
- Target variable aligned with discriminatory past decisions
- Outcome disparities mirroring historical exclusion
- Strong correlation between protected attributes and labels

**Detection Methods:**
- Compare outcomes to documented historical discrimination patterns
- Conduct counterfactual label analysis
- Perform disparity testing on ground truth labels

---

#### 2. Representation Bias
**Definition:** Systematic under- or overrepresentation of groups in training data.

**Indicators:**
- Demographic imbalance vs population benchmarks
- Sparse representation at demographic intersections
- Data quality disparities across groups

**Detection Methods:**
- Demographic distribution audit
- Representation ratio calculation
- Intersectional sample size analysis
- Missingness pattern comparison

---

#### 3. Measurement Bias
**Definition:** Proxy variables or operationalization choices disadvantage certain groups.

**Indicators:**
- Proxy variables correlated with protected attributes
- Label validity differs across groups
- Different measurement error rates

**Detection Methods:**
- Proxy correlation testing
- Differential validity analysis
- Cross-group feature performance testing

---

#### 4. Encoding & Transformation Bias
**Definition:** Feature encoding, normalization, or imputation disproportionately affects groups.

**Indicators:**
- Categorical embeddings encoding demographic clusters
- Imputation error higher for specific groups
- Normalization compresses minority variance

**Detection Methods:**
- Distribution comparison pre/post transformation
- Feature importance disparity analysis
- Group-level transformation impact testing

---

### B. Algorithm-Level Biases

#### 5. Inductive Bias / Architecture Bias
**Definition:** Model architecture favors majority patterns.

**Indicators:**
- Performance shifts across architectures
- Minority group performance improves with increased capacity

**Detection Methods:**
- Architecture comparison under identical data
- Capacity sensitivity testing
- Learning curve analysis by group

---

#### 6. Optimization & Loss Function Bias
**Definition:** Objective functions prioritize aggregate accuracy over minority performance.

**Indicators:**
- Disparities increase during training
- Minority convergence occurs later
- Loss reduction concentrated in majority groups

**Detection Methods:**
- Group-level convergence tracking
- Fairness-aware loss comparison
- Error decomposition analysis

---

#### 7. Regularization & Hyperparameter Bias
**Definition:** Regularization eliminates features predictive for minority groups.

**Indicators:**
- Feature importance loss for minority patterns
- Early stopping freezes unequal convergence

**Detection Methods:**
- Regularization strength sweep analysis
- Feature elimination tracking
- Performance gap sensitivity testing

---

### C. Feedback & Dynamic Biases

#### 8. Direct Feedback Loop Bias
**Definition:** Model outputs directly influence future inputs.

**Indicators:**
- Disparity growth over time
- Reinforcement of initial allocation patterns

**Detection Methods:**
- Disparity growth rate analysis
- Time-series fairness tracking
- Counterfactual simulation

---

#### 9. Indirect / System-Driven Feedback Bias
**Definition:** Outputs shape future data through intermediate mechanisms.

**Indicators:**
- Distribution drift correlated with model decisions
- Long-term divergence from baseline patterns

**Detection Methods:**
- Distribution shift monitoring
- Causal pathway mapping
- Simulation under varied deployment conditions

---

### D. Deployment & Interaction Biases

#### 10. Human-AI Interaction Bias
**Definition:** Different groups interact with the system differently.

**Indicators:**
- Different override rates
- Different abandonment rates
- Trust disparity signals

**Detection Methods:**
- Interaction logging disaggregation
- Behavioral pattern comparison
- Appeal and override audits

---

#### 11. Infrastructure & Accessibility Bias
**Definition:** Deployment environment limits access or performance.

**Indicators:**
- Performance varies by device type or region
- Language barriers
- Resource constraints

**Detection Methods:**
- Environment performance testing
- Accessibility audits
- Geographic performance comparison

---

#### 12. Organizational Implementation Bias
**Definition:** Institutional workflows distort fairness properties.

**Indicators:**
- Inconsistent decision overrides
- Incentive misalignment
- Region-specific disparities

**Detection Methods:**
- Workflow analysis
- Decision audit comparison
- Policy variance tracking

---

## 3. Prioritization Framework

Each identified bias source is scored on five dimensions:

| Dimension | Description |
|-----------|-------------|
| Severity | Harm magnitude if unaddressed |
| Scope | Proportion of population affected |
| Persistence | Likelihood of amplification over time |
| Historical Alignment | Connection to documented historical discrimination |
| Intervention Feasibility | Practical difficulty of mitigation |

### Priority Score Formula

Priority Score =  
(Severity × 0.30) +  
(Scope × 0.20) +  
(Persistence × 0.20) +  
(Historical Alignment × 0.20) +  
(Intervention Feasibility × 0.10)

### Categories

- **High Priority:** ≥ 4.0  
- **Medium Priority:** 3.0 – 3.99  
- **Low Priority:** < 3.0  

All high-priority bias sources require documented mitigation plans.

---

## 4. Integration With Other Tools

BSIT must be used alongside:

- Historical Context Assessment  
- Fairness Definition Selection Tool  

Bias detection must reference:
- Historical risk patterns
- Selected fairness definitions
- Known trade-offs and impossibility constraints

---

## 5. Documentation Requirement

For each bias source, teams must document:

- Evidence  
- Impacted fairness definitions  
- Historical alignment  
- Risk score  
- Mitigation plan  
- Monitoring plan  

Bias assessment is incomplete without documentation.
