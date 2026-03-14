# Post-Processing Fairness Toolkit
A Practical Framework for Improving Fairness in Model Predictions Without Retraining

---

## Introduction

Machine learning models deployed in real-world systems may continue to produce unfair outcomes even after careful dataset preparation and fairness-aware model training.

This occurs because bias can emerge not only from data and model structure but also from **how model predictions are translated into decisions**.

In many operational environments, retraining a model may not be feasible due to:

- regulatory approval requirements
- production stability concerns
- limited engineering resources
- reliance on third-party or legacy models

In these situations, **post-processing fairness interventions** provide an effective alternative.

Post-processing techniques modify **model outputs after training** in order to reduce disparities across demographic groups while preserving the predictive value of the original model.

The **Post-Processing Fairness Toolkit** provides a structured framework for selecting and implementing prediction-level fairness interventions.

The toolkit helps teams:

- Diagnose fairness issues in model predictions  
- Select appropriate post-processing techniques based on fairness goals  
- Adjust decision thresholds or prediction scores  
- Implement calibration and transformation techniques  
- Integrate fairness interventions into production systems  
- Evaluate fairness improvements while maintaining model performance  

Rather than retraining models or modifying training data, the toolkit focuses on **fairness adjustments applied directly to model outputs**.

---

## Relationship to Other Fairness Toolkits

The **Post-Processing Fairness Toolkit** complements earlier fairness interventions within the **Fairness Intervention Playbook**.

Each toolkit addresses fairness at a different stage of the machine learning lifecycle.

| Stage | Toolkit | Purpose |
|------|--------|--------|
| Bias Diagnosis | Causal Fairness Toolkit | Identify causal mechanisms behind disparities |
| Data Intervention | Pre-Processing Fairness Toolkit | Mitigate bias in training datasets |
| Model Intervention | In-Processing Fairness Toolkit | Integrate fairness constraints during training |
| Prediction Intervention | **Post-Processing Fairness Toolkit** | Adjust model outputs after training |

Post-processing interventions are especially useful when:

- the model is already deployed
- retraining would disrupt production systems
- regulatory constraints prevent rapid model modification
- model internals are unavailable

---

## Toolkit Overview

The Post-Processing Fairness Toolkit contains the following components:

### 1️⃣ Threshold Optimization Framework  
- Group-specific decision thresholds  
- Mathematical formulations of fairness definitions  
- Threshold search algorithms  

### 2️⃣ Calibration Implementation Template  
- Probability calibration across demographic groups  
- Calibration error measurement  
- Calibration model implementation  

### 3️⃣ Prediction Transformation System  
- Learned transformation functions  
- Distribution alignment techniques  
- Fair score transformation methods  

### 4️⃣ Rejection Option Classification Framework  
- Confidence-based deferral mechanisms  
- Selective classification strategies  
- Human–AI collaboration models  

### 5️⃣ Integration Workflow Design  
- Production pipeline integration  
- Real-time prediction adjustments  
- monitoring and maintenance strategies  

### 6️⃣ Evaluation Framework  
- Fairness metric evaluation  
- fairness–utility trade-off analysis  
- stability monitoring  

### 7. Implementation Checklist  

### 8. Practical Workflow Summary  

### 9. Core Principles  

---

<a id="threshold"></a>
## 1️⃣ Threshold Optimization Framework
→ Adjust decision thresholds to satisfy fairness criteria.

---

### 1.1 Fairness Definitions for Threshold Optimization
  
Threshold optimization can enforce different fairness definitions by selecting group-specific decision thresholds.  

---

#### Demographic Parity

Find thresholds equalizing selection rates across groups.  

$P(\hat{Y}=1 \mid A=a) = P(\hat{Y}=1 \mid A=b)$ for all groups $a,b$  

This definition ensures that **different demographic groups receive positive predictions at the same overall rate**.   

---

#### Equal Opportunity

Find thresholds equalizing true positive rates.  

$P(\hat{Y}=1 \mid Y=1, A=a) = P(\hat{Y}=1 \mid Y=1, A=b)$ for all groups $a,b$  

This definition ensures that **qualified individuals receive positive predictions at equal rates across demographic groups**.  

---

#### Equalized Odds

Find thresholds equalizing both true positive and false positive rates.    

$P(\hat{Y}=1 \mid Y=y, A=a) = P(\hat{Y}=1 \mid Y=y, A=b)$    

for all $y \in \{0,1\}$ and groups $a,b$  

This definition ensures that **both types of prediction errors are balanced across demographic groups**.  

---

### 1.2 Threshold Search Algorithm 

---

1. Split the validation dataset by protected attribute groups.  

2. For each group:  
   - Compute ROC curve points  
   - For each fairness definition:   
      - Identify valid thresholds
      - Select threshold maximizing utility

4. Validate the selected thresholds on held-out test data.  

5. Document selected thresholds and resulting fairness–performance trade-offs.   


---

### 1.3 Practical Threshold Selection Guidelines

---

Use group-specific thresholds when:

- protected attributes are legally available at inference time
- fairness definitions require group-aware decisions

Use score transformations when:

- protected attributes cannot be used during decision making

Use rejection classification when:

- uncertainty near the threshold creates fairness risks

---

<a id="calibration"></a>
## 2️⃣ Calibration Implementation Template
→ Ensure probability predictions have consistent meaning across groups.

Calibration ensures predicted probabilities correspond to **actual observed outcomes**.

Example:

If a model predicts **70% default risk**, approximately **70% of those applicants should default**.

Miscalibration across demographic groups leads to inconsistent risk interpretation.

---

## 2.1 Calibration Disparity Assessment

1. Split validation data by demographic groups

2. For each group:
a. Plot reliability diagram
b. Compute Expected Calibration Error (ECE)
c. Compute Maximum Calibration Error (MCE)

3. Compare calibration errors across groups

Example:

| Group | Expected Calibration Error |
|------|-----------------------------|
| Men | 0.03 |
| Women | 0.08 |

Higher ECE indicates greater miscalibration.

---

## 2.2 Calibration Techniques

### Platt Scaling

Transforms prediction scores using logistic regression.  

P(Y=1|s) = 1 / (1 + exp(-(As + B)))  


Parameters A and B are fitted on validation data.

---

### Isotonic Regression

A non-parametric calibration technique that preserves ranking order.

Useful when calibration errors are **non-linear**.

---

### Temperature Scaling

Applies a scaling parameter to neural network logits.  

P(Y=1|s) = 1 / (1 + exp(-s/T))  


Where **T** is a learned temperature parameter.

---

## 2.3 Calibration Implementation Workflow

1. Divide validation data into calibration set and test set
2. Fit calibration models separately for each group
3. Apply calibration transformation to model outputs
4. Verify calibration improvement using reliability diagrams


---

<a id="transformation"></a>
## 3️⃣ Prediction Transformation System
→ Modify prediction scores to satisfy fairness constraints.

Prediction transformations adjust model outputs while preserving useful predictive information.

They are especially useful when:

- threshold adjustments are insufficient
- complex fairness patterns exist
- ranking information must be preserved

---

### 3.1 Learned Transformation Functions

Learned transformations discover mappings from original predictions to fair outputs.

Optimization objective:    

Minimize prediction distortion  
Subject to fairness constraints  


These mappings are trained using validation data.

---

### 3.2 Distribution Alignment Techniques

Align prediction score distributions across demographic groups.

Common approaches include:

- quantile mapping
- optimal transport
- distribution matching

Example:

| Group | Mean Score |
|------|-------------|
| Men | 0.41 |
| Women | 0.36 |

Transformation aligns distributions so scores become comparable.

---

### 3.3 Fair Score Transformations

Fair score transformations modify prediction scores while preserving ordering within groups.

Examples:

- monotonic transformations
- score normalization
- constrained re-ranking

This is useful in ranking systems such as:

- credit scoring
- recommendation systems
- risk prioritization models

---

<a id="rejection"></a>
## 4️⃣ Rejection Option Classification Framework
→ Defer uncertain predictions to human review.

Some predictions occur in **high-uncertainty regions** where automated decisions risk unfair outcomes.

Rejection option classification introduces a third decision path:

| Decision | Description |
|--------|-------------|
| Automated approval | High-confidence positive prediction |
| Automated rejection | High-confidence negative prediction |
| Human review | Low-confidence prediction |

---

### 4.1 Confidence-Based Rejection Thresholds

Low-confidence predictions are deferred to human reviewers.

Example:  

if confidence > 0.85 → automated decision  
if 0.45 < confidence < 0.85 → human review  


---

### 4.2 Selective Classification Strategy

Selective classification optimizes the trade-off between:

- automation coverage
- fairness improvement

Example:

| Automation Coverage | Fairness Gap |
|---------------------|--------------|
| 100% | 6% |
| 90% | 3% |
| 80% | 1.5% |

Reducing automation coverage often improves fairness.

---

### 4.3 Human–AI Collaboration Design

Effective rejection systems require structured human review.

Best practices include:

- presenting decision context without bias-triggering cues
- requiring reviewers to document decision reasoning
- monitoring human decisions for fairness consistency

---

<a id="integration"></a>
## 5️⃣ Integration Workflow Design
→ Deploy fairness interventions within production systems.

Post-processing fairness techniques operate between **model prediction and final decision**.

Typical pipeline:  

Model Prediction  
↓  
Calibration Layer  
↓  
Score Transformation  
↓  
Threshold Decision  
↓  
Rejection Option Check  
↓  
Final Decision  

---

### Example Production Pipeline  

Raw Model Output  
↓  
Calibration Adjustment  
↓  
Score Transformation  
↓  
Fairness-Aware Threshold  
↓  
Human Review if Required  
↓  
Final Decision  


---

<a id="evaluation"></a>
## 6️⃣ Evaluation Framework
→ Measure fairness intervention effectiveness.

---

### 6.1 Fairness Metrics

Evaluate fairness across groups using:

- demographic parity
- equal opportunity
- equalized odds
- calibration error

---

### 6.2 Utility Preservation

Measure predictive performance:

- accuracy
- AUC
- F1 score

Fairness improvements should not excessively degrade predictive performance.

---

### 6.3 Fairness–Utility Trade-off Analysis

Generate Pareto curves comparing fairness and performance.

Example:

| Intervention | Fairness Gap | AUC |
|--------------|-------------|-----|
| Baseline | 6% | 0.82 |
| Threshold optimization | 3% | 0.81 |
| Calibration | 2% | 0.81 |
| Transformation | 1% | 0.80 |

---

### 6.4 Stability Monitoring

Evaluate robustness under:

- new data distributions
- parameter changes
- temporal shifts

---

<a id="checklist"></a>
## 7. Implementation Checklist

Before deploying post-processing fairness interventions:

**Fairness Diagnosis**

- [ ] Identify fairness metrics showing disparities  
- [ ] Determine fairness objective  

**Technique Selection**

- [ ] Choose threshold optimization, calibration, transformation, or rejection classification  

**Implementation**

- [ ] Fit transformation or calibration models  
- [ ] Apply fairness-aware thresholds  

**Evaluation**

- [ ] Measure fairness improvements  
- [ ] Validate performance impact  

**Deployment**

- [ ] Integrate with prediction pipeline  
- [ ] Establish monitoring system  

---

<a id="summary"></a>
## 8. Practical Workflow Summary

1. Identify prediction disparities across demographic groups  
2. Select fairness objective  
3. Choose post-processing intervention  
4. Apply threshold adjustment or prediction transformation  
5. Evaluate fairness improvements  
6. Integrate intervention into production pipeline  
7. Monitor fairness over time  

---

<a id="principles"></a>
## 9. Core Principles

Effective post-processing fairness interventions should:

- Preserve predictive information whenever possible  
- Target specific fairness definitions  
- Address intersectional disparities  
- Maintain operational compatibility with deployed systems  
- Document fairness decisions and trade-offs  
- Support continuous fairness monitoring

---

For sources that informed this toolkit, see the [0_References](https://github.com/monikase/AI_Ethics/blob/main/Fairness_Intervention_Playbook/0_References.md)

