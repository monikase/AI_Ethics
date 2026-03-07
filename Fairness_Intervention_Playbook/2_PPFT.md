# Pre-Processing Fairness Toolkit
A Practical Framework for Selecting Data-Level Fairness Interventions

## 1. Introduction

Machine learning systems can inherit bias from the data used to train them. Even when protected attributes such as gender or race are not explicitly included in a model, historical inequalities, representation imbalances, and proxy variables may still produce discriminatory outcomes.

Bias in training data can arise through several mechanisms:

- **Representation disparities** where certain demographic groups are underrepresented
- **Proxy discrimination** where seemingly neutral variables indirectly encode protected attributes
- **Label bias** where historical decisions reflect discriminatory practices
- **Structural correlations** between protected attributes and predictive features

If these issues are not addressed before training, machine learning models may reproduce and amplify existing inequalities.

The **Pre-Processing Fairness Toolkit** provides a structured framework for diagnosing and mitigating bias at the data level before model training begins.

The toolkit helps teams:

- Identify bias patterns through systematic data auditing  
- Select appropriate pre-processing techniques based on bias mechanisms  
- Configure interventions for specific fairness goals  
- Evaluate fairness improvements while preserving predictive performance  
- Document fairness decisions transparently  

Rather than applying fairness interventions blindly, the toolkit focuses on **matching specific bias patterns to appropriate data-level interventions**.

---

## 2. Relationship to the Causal Fairness Toolkit

The **Pre-Processing Fairness Toolkit** is designed to work in conjunction with the **Causal Fairness Toolkit** developed in Sprint 1.

While the Causal Fairness Toolkit focuses on identifying **why disparities occur** by analyzing causal pathways between protected attributes and outcomes, the Pre-Processing Toolkit focuses on **how to intervene at the data level to mitigate those disparities**.

Together, the two toolkits form a complementary workflow:

| Stage | Toolkit | Purpose |
|------|--------|--------|
| Bias Diagnosis | Causal Fairness Toolkit | Identify causal pathways that create disparities |
| Bias Pattern Identification | Data Auditing | Detect representation gaps, proxy variables, and label bias |
| Intervention Selection | Pre-Processing Fairness Toolkit | Select appropriate data-level interventions |
| Model Training | ML Pipeline | Train models using fairness-aware datasets |
| Monitoring | Both Toolkits | Evaluate fairness and performance over time |

### Example Integration

For example, causal analysis may reveal the pathway:  
Gender → Employment History → Default Risk → Loan Approval  

This suggests that **employment history acts as a mediator influenced by gender**, potentially penalizing applicants with career breaks.

The Pre-Processing Toolkit then translates this insight into a **specific intervention**, such as:

- transforming employment history into a **relevant experience metric**
- reweighting samples with employment gaps
- generating counterfactual examples that remove gender-based employment penalties

By linking causal diagnosis with targeted data-level interventions, the combined toolkit enables teams to address fairness issues **at their root cause rather than through purely statistical adjustments**.

---

## 3. Toolkit Overview

The toolkit consists of the following components:

### 1️⃣ [Comprehensive Data Auditing Framework](#auditing)
- 1.1 Representation Analysis  
- 1.2 Correlation and Proxy Detection  
- 1.3 Label Quality Assessment  
- 1.4 Fairness Baseline Calculation  
- 1.5 Intersectional Bias Analysis  

### 2️⃣ [Technique Catalog](#catalog)
- 2.1 Reweighting Techniques  
- 2.2 Sampling Methods  
- 2.3 Distribution Transformation Methods  
- 2.4 Fairness-Aware Data Generation  

### 3️⃣ [Intervention Selection Framework](#selection)
- 3.1 Bias Pattern Identification  
- 3.2 Technique Selection Decision Tree  
- 3.3 Combined Intervention Strategies  
- 3.4 Intersectional Intervention Considerations  

### 4️⃣ [Configuration Guidelines](#configuration)
- 4.1 Reweighting Configuration  
- 4.2 Transformation Configuration  
- 4.3 Synthetic Data Generation Configuration  
- 4.4 Fairness–Utility Trade-off Management  

### 5️⃣ [Evaluation Framework](#evaluation)
- 5.1 Fairness Metrics  
- 5.2 Information Preservation  
- 5.3 Computational Efficiency  
- 5.4 Robustness and Stability  

### 6. [Deployment & Monitoring](#deployment)

### 7. [Implementation Checklist](#checklist)

### 8. [Practical Workflow Summary](#summary)

### 9. [Core Principles](#core-prin)

---

<a id="auditing"></a>
## 1️⃣ Comprehensive Data Auditing Framework
→ Diagnose bias patterns before selecting fairness interventions.

Before applying fairness interventions, teams must first identify **how bias manifests in the dataset**. Data auditing serves as the diagnostic step that determines which interventions are appropriate.

Without systematic auditing, fairness interventions may address symptoms rather than underlying causes.

---

### 1.1 Representation Analysis

Representation analysis examines whether demographic groups are adequately represented in the dataset.

Steps include:

**Compare dataset demographics with reference populations**

Possible references include:

- census data
- industry benchmarks
- application-specific populations

**Identify representation gaps**

Example:

| Group | Dataset Share | Expected Share |
|------|---------------|---------------|
| Women | 48% | 50% |
| Women of color | 9% | 14% |

**Analyze representation across outcomes**

Example:

| Group | Loan Approval Rate |
|------|--------------------|
| Male applicants | 76% |
| Female applicants | 58% |

**Temporal analysis**

Representation patterns should also be analyzed across time to detect shifts or structural trends.

---

### 1.2 Correlation and Proxy Detection

Protected attributes may influence predictions indirectly through correlated variables.

Audit techniques include:

- correlation matrices
- mutual information analysis
- conditional independence testing

Example proxy variables:

| Feature | Possible Proxy For |
|--------|--------------------|
| ZIP code | race |
| part-time status | gender |
| school prestige | socioeconomic status |

These proxies may enable **indirect discrimination even when protected attributes are removed from the model**.

---

### 1.3 Label Quality Assessment

Training labels may reflect **historical discrimination or annotation bias**.

Audit procedures should evaluate:

- disparities in label distribution across demographic groups
- annotation processes and subjective evaluation criteria
- external validation against trusted benchmarks

Example:

Historical hiring decisions may reflect biased evaluation practices rather than actual job performance.

---

### 1.4 Fairness Baseline Calculation

Before applying interventions, baseline fairness metrics should be calculated.

Common metrics include:

- demographic parity
- equal opportunity
- equalized odds

Example baseline metrics:

| Metric | Value |
|------|------|
| Demographic parity difference | 0.18 |
| Equal opportunity gap | 0.15 |

These values serve as **reference points for evaluating fairness improvements**.

---

### 1.5 Intersectional Bias Analysis

Bias may affect combinations of protected attributes rather than individual attributes.

Example intersections include:

- gender × race
- gender × age
- race × socioeconomic status

Intersectional analysis ensures fairness interventions do not improve aggregate metrics while leaving specific subgroups disadvantaged.

---

<a id="catalog"></a>
## 2️⃣ Technique Catalog
→ Document available data-level fairness interventions.

---

### 2.1 Reweighting Techniques

Reweighting methods modify the **influence of training samples during model learning**.

#### Instance Weighting

Assigns higher importance to underrepresented or disadvantaged samples.

Example weight calculation:  
weight = 1 / frequency(group)  


Use cases:

- representation disparities
- outcome imbalances

Strengths:

- retains all original data
- flexible adjustment strength

Limitations:

- requires model support for instance weights
- extreme weights may increase variance

---

### 2.2 Sampling Methods

Sampling methods modify the **dataset composition**.

#### Oversampling

Increase representation of minority groups by duplicating or generating new samples.

Strengths:

- improves representation balance

Limitations:

- may cause overfitting

---

#### Undersampling

Reduce samples from majority groups.

Strengths:

- simple implementation

Limitations:

- loss of potentially valuable information

---

### 2.3 Distribution Transformation Methods

These methods modify **feature distributions** to reduce correlations with protected attributes.

---

#### Disparate Impact Removal

Transforms features so distributions become independent of protected attributes while preserving rank ordering.

Use cases:

- proxy discrimination
- continuous features correlated with protected attributes

---

#### Fair Representation Learning

Creates new feature representations that mask protected attributes while preserving predictive information.

Strengths:

- handles non-linear relationships
- addresses complex bias patterns

Limitations:

- reduced interpretability
- higher computational complexity

---

### 2.4 Fairness-Aware Data Generation

Generative models create synthetic data to address representation gaps.

Examples:

- SMOTE
- GAN-based approaches
- Variational autoencoders

Strengths:

- generates new samples for underrepresented groups
- improves intersectional representation

Limitations:

- requires strong validation
- risk of unrealistic data artifacts

---

<a id="selection"></a>
## 3️⃣ Intervention Selection Framework
→ Match bias patterns to appropriate interventions.

---

### 3.1 Bias Pattern Identification

Bias patterns detected during auditing determine the appropriate intervention strategy.

Common patterns include:

| Bias Pattern | Description |
|---|---|
| Representation disparity | Unequal group representation |
| Proxy discrimination | Correlations between features and protected attributes |
| Label bias | Historical discrimination in outcome labels |
| Multiple mechanisms | Several bias sources interact |

---

### 3.2 Technique Selection Decision Tree
Start  
│  
├ Representation disparity?  
│ ├ Model supports weights → Reweighting  
│ ├ Sufficient minority samples → Resampling  
│ └ Severe imbalance → Synthetic data generation  
│  
├ Proxy discrimination?  
│ ├ Proxy features identifiable → Distribution transformation  
│ └ Complex correlations → Fair representation learning  
│  
├ Label bias?  
│ ├ Historical discrimination → Outcome-aware reweighting  
│ └ Measurement error → Data relabeling  
│  
└ Multiple bias types?  
→ Combined intervention strategy  


---

### 3.3 Combined Intervention Strategies

Many datasets contain multiple bias mechanisms.

Example combined strategy:

| Bias Type | Intervention |
|---|---|
| Representation imbalance | Reweighting |
| Proxy discrimination | Feature transformation |
| Severe data gaps | Synthetic data generation |

---

### 3.4 Intersectional Intervention Considerations

Small intersectional groups may require specialized approaches:

- targeted oversampling
- synthetic data generation
- hierarchical modeling

---

<a id="configuration"></a>
## 4️⃣ Configuration Guidelines
→ Configure fairness interventions for specific datasets.

---

### 4.1 Reweighting Configuration

Steps:

1. Define fairness objective
2. Select weighting formula
3. Set maximum weight thresholds
4. Monitor model stability

Best practice:

Start with moderate weights and adjust gradually.

---

### 4.2 Transformation Configuration

Steps:

1. Identify correlated features
2. Evaluate legitimate predictive value
3. Apply transformations selectively

Avoid transforming features that directly measure task-relevant risk.

---

### 4.3 Synthetic Data Generation Configuration

Generation pipeline:

1. Define fairness constraints
2. Train generative model
3. Validate synthetic data
4. Integrate with original dataset

Typical dataset composition:
70% original data  
30% synthetic data  


---

### 4.4 Fairness–Utility Trade-off Management

Fairness interventions may affect predictive performance.

Trade-offs include:

| Objective | Possible Impact |
|---|---|
| Fairness improvement | Reduced bias |
| Predictive accuracy | Slight decrease |
| Computational cost | Increased preprocessing time |

---

<a id="evaluation"></a>
## 5️⃣ Evaluation Framework
→ Measure fairness intervention impact.

---

### 5.1 Fairness Metrics

Evaluate fairness using:

- demographic parity
- equal opportunity
- equalized odds

Metrics should be evaluated across:

- demographic groups
- intersectional subgroups

---

### 5.2 Information Preservation

Measure predictive performance:

- accuracy
- AUC
- F1 score

Ensure fairness improvements do not excessively reduce model performance.

---

### 5.3 Computational Efficiency

Assess:

- preprocessing runtime
- memory usage
- training time

---

### 5.4 Robustness and Stability

Test interventions under:

- different training splits
- parameter variations
- new incoming data

---

<a id="deployment"></a>
## 6. Deployment & Monitoring

Fairness interventions must remain effective after deployment.

Monitoring should include:

- periodic fairness audits
- detection of data distribution shifts
- retraining pipelines when disparities reappear

---

<a id="checklist"></a>
## 7. Implementation Checklist

Before deploying fairness interventions:

**Data Auditing**

- [ ] Representation analysis performed  
- [ ] Proxy variables identified  
- [ ] Label bias evaluated  

**Intervention Selection**

- [ ] Bias patterns classified  
- [ ] Appropriate technique selected  

**Configuration**

- [ ] Parameters tuned  
- [ ] Fairness–utility trade-offs documented  

**Evaluation**

- [ ] Fairness metrics measured  
- [ ] Model performance evaluated  

---

<a id="summary"></a>
## 8. Practical Workflow Summary

1. Conduct data auditing  
2. Identify bias mechanisms  
3. Select appropriate interventions  
4. Configure intervention parameters  
5. Evaluate fairness and performance  
6. Deploy preprocessing pipeline  
7. Monitor fairness over time  

---

<a id="core-prin"></a>
## 9. Core Principles

Effective pre-processing fairness interventions should:

- Address **specific bias mechanisms**
- Preserve legitimate predictive information
- Consider **intersectional fairness**
- Document assumptions and trade-offs
- Integrate smoothly with ML pipelines
- Support continuous monitoring  
