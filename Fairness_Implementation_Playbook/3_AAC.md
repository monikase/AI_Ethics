# Advanced Architecture Cookbook  
_(Part 3 of the Fairness Implementation Playbook)_

## Purpose
Fairness failures in modern AI systems rarely stem from lack of awareness. **They occur when fairness strategies ignore system architecture.**  
  
This Advanced Architecture Cookbook transforms fairness into an **architecture‑aware, system‑level engineering practice.** It provides actionable implementation guidance for:  

- Large Language Models (LLMs)
- Recommendation Systems
- Vision Models
- Multi‑Modal Systems

The cookbook complements:  

- team‑level execution (Fair AI Scrum Toolkit)
- organizational oversight (Organizational Integration Toolkit)  

by focusing on **how different architectures create distinct fairness failures.**  

---

## System Role in the Playbook

AAC is the **technical implementation layer** of the Fairness Implementation Playbook.

It enables:

- **FAST (execution layer)** → by providing mitigation methods  
- **OIT (governance layer)** → by implementing FDR-defined fairness goals  
- **RCG (compliance layer)** → by ensuring validation meets regulatory requirements  

---

## Inputs & Outputs

### Inputs

- **From OIT (Organizational Integration Toolkit)**  
  - Fairness Decision Records (FDRs)  
  - fairness definitions (e.g., Equal Opportunity)  
  - metrics and thresholds  
  - approved trade-offs  

- **From FAST (Fair AI Scrum Toolkit)**  
  - identified bias issues  
  - SAFE stories requiring mitigation  
  - FAIR validation criteria  

- **From RCG (Regulatory Compliance Guide)**  
  - validation requirements  
  - compliance constraints  
  - required documentation standards  

---

### Outputs

- **To FAST**  
  - implemented mitigation strategies  
  - updated model behavior  
  - validation results  

- **To RCG**  
  - technical validation evidence  
  - explanation of mitigation methods  
  - reproducible results  

- **To OIT**  
  - feedback on feasibility and trade-offs  
  - recommendations for FDR updates  

---

## Core Principle

> **All technical interventions must align with Fairness Decision Records (FDRs) and satisfy RCG validation requirements.**

AAC does not decide fairness — it **implements it correctly per architecture**.

---

## When to Use This Cookbook

AAC is triggered when:

- FAST identifies fairness issues  
- FDR requires mitigation  
- RCG validation thresholds are not met 

---

## Business Value

Embedding fairness at the architecture level enables:

- **Robust systems** across environments and user groups
- **Root‑cause mitigation**, not post‑hoc fixes
- **Reusable engineering patterns** instead of ad‑hoc solutions
- **Reduced risk** in complex AI deployments
- **Improved generalization and product quality**

## What This Cookbook Will Do  

- Provide **architecture-specific fairness strategies**  
- Translate fairness theory into **implementation recipes**  
- Help teams **select appropriate interventions per system type**  
- Define **evaluation and validation standards per architecture**  
- Enable **consistent fairness across heterogeneous AI systems**  

## Connection to Other Playbook Components  

- **Fairness Audit** → identifies architecture-specific risks  
- **Fairness Intervention** → defines mitigation strategies  
- **Fair AI Scrum Toolkit** → operationalizes fairness in teams
- **Organizational Integration Toolkit** → governs fairness decisions 

## Cookbook Overview  

#### 1. [How to Use This Cookbook](#usage)  
#### 2. [Large Language Models (LLM) Suite](#llm)  
#### 3. [Recommendation Systems Suite](#recsys)  
#### 4. [Vision Models Suite](#vision)  
#### 5. [Multi-Modal Systems Suite](#multimodal)  
#### 6. [Cross-Architecture Primitives](#cross)  
#### 7. [Intersectionality Layer](#intersectionality)  
#### 8. [Implementation Workflow](#workflow)  
#### 9. [Core Principles](#principles)  
#### 10. [References](#refs) 

---

<a id="usage"></a>
## 1️⃣ How to Use This Cookbook  

### 1.1 Identify the Architecture  

Determine which system you are working with:

- **LLM** → open‑ended text generation or analysis
- **Recommendation System (RecSys)** → ranking and exposure over time
- **Vision Model** → image or video perception
- **Multi-Modal System** → combines multiple data types (text, vision, audio) 

### 1.2 Diagnose the Bias Source

- **Data** (imbalance, environment)  
- **Representation** (latent features)  
- **System Dynamics** (feedback loops)  
- **Interaction** (prompts, users, modalities)  

### 1.3 Select Interventions (Architecture‑Aligned)


|  | Architecture | Primary Intervention Levers |
|---|--------|--------|
| 1 | LLM | Prompting, fine‑tuning, decoding, guardrails |
| 2 | RecSys | Exposure control, exploration, feedback management |
| 3 | Vision | Capture conditions, representation auditing |
| 4 | Multi‑Modal | Fusion control, routing, coordination |

### 1.4 Validate and Monitor

- Use **architecture‑specific metrics**
- Evaluate **intersectional slices**
- Test **real‑world operating conditions**
- Monitor continuously as systems evolve

### 1.5 Recipe Cards (User Documentation)

Recipe cards are **decision guides for engineering teams**.  
  
Each card specifies:  

- **When** to use an intervention
- **Where** it fits in the pipeline
- **How** to apply it safely
- **What to validate afterward**  

> Recipe cards illustrate common architectural fairness patterns.  
> They are _not exhaustive_ and should be adapted as new failure modes emerge.  


### 1.6. Minimum Viable Use (Time‑Constrained Teams)

1. Identify architecture
2. Scan common issues
3. Pick **one recipe** 
4. Validate with **one metric**
5. Log assumptions and risks

### 1.7 Who Uses What

- **ML Engineers** → Implementation + Evaluation
- **Product** → Trade‑offs + Risk
- **QA/Risk** → Validation + Monitoring

---

<a id="llm"></a>
## 2️⃣ Large Language Models (LLM) Suite  

  
### 2.1 Common Fairness Issues  

|  | Category | Symptom | Impact |
|---|--------|--------|--------|
| 1 | Stylistic Stereotyping | Tone differs by group (e.g. Supportive tone for women, directive tone for men) | Reinforces social norms |
| 2 | Association Bias | Certain skills linked to demographics | Skewed evaluations |
| 3 | Prompt Sensitivity | Fairness varies by phrasing | Inconsistent outcomes |
| 4 | Sycophancy | Model agrees with biased input | Bias amplification |
| 5 | Hallucination Bias | Fabricated biased facts | Misinformation |

### 2.2 Frequent Mistakes

1. Relying on classification fairness metrics for generative outputs
2. Auditing only one prompt template
3. Treating RLHF as sufficient without prompt controls
4. Ignoring decode‑time bias emergence
5. Assuming neutrality from "professional" tone

### 2.3 Why LLMs Are Special

- Generative freedom creates infinite surface area for bias
- Prompt‑conditioned behavior makes fairness contextual
- Emergent properties appear only at scale
- Decoding choices shape fairness as much as training

### 2.4 Selected Recipe Cards

#### Recipe Card LLM-1: Counterfactual Prompting + Self‑Critique

- **Use when** tone or framing differs for similar profiles
- **Apply at** prompt and generation stages
- **How:** Generate → Swap protected attributes → Self‑review → Regenerate if inconsistent
- **Watch out:** Over‑constraining prompts reduces usefulness
- **Validate:** Counterfactual consistency ≥ 90%

#### Recipe Card LLM‑2: Fairness‑Aware Fine‑Tuning (RLHF‑F)

- **Use when** bias persists across diverse prompts
- **Apply at** fine‑tuning
- **How:** Balanced data → Counterfactual augmentation → Fairness‑weighted rewards
- **Watch out:** Mode collapse from excessive reward strength
- **Monitor:** Stereotype rate ↓, Perplexity Δ ≤ 5%

#### Recipe Card LLM‑3: Decode‑Time Self‑Rerank

- **Use when** residual bias remains after training
- **Apply at** decoding
- **How:** Sample k outputs → Score → Select fairest acceptable output
- **Watch out:** Latency and reduced diversity
- **Validate:** Bias ↓ with fluency preserved


### 2.5 Recipe Summary

|  | Stage | Primitive | Purpose | Typical Parameter Range |
|---|--------|--------|--------|--------|
| 1 | Corpus | Dynamic thematic balancing | Equal topic‑demographic density | 0.08 – 0.12 |
| 2 | Pre‑train | Opposite‑corpus blending | Inject counter‑stereotypes | 10–20% |
| 3 | Fine‑tune | RLHF‑F | Equal topic‑demographic density | Threshold ≥ 0.8 |
| 4 | Decode | Self‑rerank diversity | Equal topic‑demographic density | Weight 0.3–0.6 |
| 5 | Post | Bias filter | Catch residual harms | n/a |   

#### Validation Targets

- Counterfactual consistency ≥ 90%
- Toxicity ≤ 0.5%
- Perplexity Δ ≤ 5%

---

<a id="recsys"></a>
## 3️⃣ Recommendation Systems Suite  

  
### 3.1 Core Challenge  

Recommendation systems **shape behavior over time**. Exposure and feedback loops amplify historical bias even when accuracy appears fair.

### 3.2 Common Fairness Issues  

|  | Category | Symptom | Impact |
|---|--------|--------|--------|
| 1 | Exposure Bias | Same items dominate rankings | Unequal opportunity |
| 2 | Feedback Loops | Popularity reinforces itself | Structural segregation |
| 3 | Filter Bubbles | Narrow content paths | Limited opportunities |
| 4 | Provider Bias | Unequal visibility (Some providers rarely shown) | Economic harm |

### 3.3 Frequent Mistakes

- Auditing CTR instead of exposure distribution
- Ignoring long‑term feedback loops
- Treating users as the only stakeholder
- Applying static constraints to dynamic systems

### 3.4 Why Recommendation Systems Are Special

- **They actively shape user behavior**
- **Fairness unfolds over time**, not per decision
- **Multiple stakeholders** have competing fairness claims

### 3.5 Selected Recipe Cards

#### Recipe Card RS‑1: Exposure‑Aware Ranking

- **Use when** equal CTR hides disadvantaged visibility
- **Apply at** ranking layer
- **How:** Measure exposure → apply position‑aware constraints → track over time
- **Watch out:** Over‑correction harming relevance
- **Validate:** Exposure gap ≤ ±15

#### Recipe Card RS‑2: Exploration Guardrails

- **Use when** filter bubbles tighten over time
- **Apply at** exploration strategy
- **How:** Controlled exploration + popularity discounting
- **Watch out:** Excess exploration reduces satisfaction
- **Validate:** Diversity gain ≥ 30%


#### Recipe Card RS‑3: Multi‑Stakeholder Optimization

- **Use when** provider groups face systematic disadvantage
- **Apply at** objective definition
- **How:** Explicit stakeholder weights → governance review
- **Watch out:** Hidden value judgments
- **Validate:** Provider exposure parity

### 3.6 Recipe Summary

|  | Stage | Primitive | Purpose | Typical Parameter Range |
|---|--------|--------|--------|--------|
| 1 | Rank | Exposure‑aware ranking | Balance visibility | Gap ≤ ±15% |
| 2 | Learn | Popularity discounting | Prevent feedback loops | Decay 0.8–0.95 |
| 3 | Explore | Controlled exploration | Break bubbles | ε = 0.05–0.15 |
| 4 | Optimize | Multi‑stakeholder loss | Balance interests | Weight tuned |

#### Validation Targets
  
- Exposure gaps within ±15% of representation
- Longitudinal exposure parity
- Long‑term diversity gain ≥ 30%
- Relevance retention ≥ 90%

---

<a id="vision"></a>
## 4️⃣ Vision Models Suite  

  
### 4.1 When to Use

- Images/video sensitive to environment and representation

### 4.2 Core Fairness Challenge  

Vision systems:
- depend on **environment (lighting, camera)**  
- learn **visual representations**  
- encode **demographic features implicitly**  

→ Bias is **data-driven and context-dependent**


### 4.3 Common Fairness Issues  

|  | Category | Symptom | Impact |
|---|--------|--------|--------|
| 1 | Skin-tone Accuracy Gap | Lower accuracy (Darker skin misdetected) | Safety & compliance risk/Discrimination risk |
| 2 | Context Bias (Background Leakage) | Background used as proxy | Systematic stereotyping |
| 3 | Attribute Leakage | Demographics (Gender/ethnicity) encoded | Hidden bias, Privacy Violation |
| 4 | Environment Sensitivity | Lighting affects results (Camera favors certain tones) | Unequal performance, Exclusion |

### 4.4 Frequent Mistakes

- Reporting only overall accuracy
- Oversaturated synthetic augmentation
- Single global decision threshold
- Ignoring lighting and lens variability

### 4.5 Why Vision Models Are Special

- **Bias enters before ML** through capture pipelines
- **Visual saliency can mislead audits**
- **Demographics hide deep in embeddings**

### 4.6 Selected Recipe Cards
 
#### Recipe Card V‑1: Environment Equalization

- **Use when** lab accuracy fails in real‑world conditions
- **Apply at** data augmentation
- **How:** Style transfer + domain randomization
- **Watch out:** Visual artifacts from over‑augmentation
- **Validate:** Robustness variance ≤ 10%

#### Recipe Card V‑2: Representation Leakage Probe

- **Use when** demographic encoding is suspected
- **Apply at** audit stage
- **How:** Probe embeddings → identify leaking layers
- **Watch out:** Detection ≠ mitigation
- **Validate:** Leak AUC ≤ 0.52

#### Recipe Card V‑3: Layer Reinitialization

- **Use when** specific layers encode protected attributes
- **Apply at** remediation
- **How:** Reinitialize leaking layers → retrain downstream
- **Watch out:** Performance regression if overused
- **Validate:** mIoU gap ≤ 2%

### 4.7 Recipe Summary

|  | Stage | Primitive | Purpose | Typical Parameter Range |
|---|--------|--------|--------|--------|
| 1 | Augment | Style‑transfer equalizer | Balance lighting/textures | 0.2–0.4 |
| 2 | Audit | Prototype leak probe | Quantify leakage | Leak < 0.02 |
| 3 | Remediate | Layer reinitialization | Remove leaking block | n/a |

#### Validation Targets
  
- Accuracy gap < 5%
- Leak AUC ≤ 0.52
- Robustness variance ≤ 10%

---

<a id="multimodal"></a>
## 5️⃣ Multi-Modal Systems Suite  

  
### 5.1 Core Fairness Challenge  

Multi-modal systems:
- combine multiple biased sources  
- create **new bias through interaction**  

→ Bias is **emergent at fusion**; modalities fail differently.

### 5.2 Coordination Rule

**Never debias modalities in isolation.** Order: Fix weakest modality → validate → adjust fusion → end‑to‑end check.

### 5.3 Common Fairness Issues  

|  | Category | Symptom | Impact |
|---|--------|--------|--------|
| 1 | Bias Transfer | One bias infects others (e.g. Vision bias misleads text) | Compounded harm |
| 2 | Missing Modality Fallback | Failure when input missing; Model fails when one stream unavailable (e.g., low-light video) | Unequal performance |
| 3 | Inconsistent Predictions | Conflicting signals | User confusion |  
| 4 | Dominant Modality | One input dominates | Narrow representations |

### 5.4 Frequent Mistakes

- Neglecting confidence‑based routing
- Skipping recalibration after modality dropout
- Debiasing modalities independently

### 5.5 Why Multi‑Modal Systems Are Special

- Shared latent space amplifies hidden bias
- Each modality fails differently
- Unequal data availability creates unequal treatment

### 5.6 Selected Recipe Cards

#### Recipe Card MM‑1: Cross‑Modal Consistency Loss

- **Use when** modality disagreement correlates with demographics
- **Apply at** fusion during training
- **How:** Penalize cross‑modal divergence
- **Watch out:** Over‑alignment suppresses useful variation
- **Validate:** Agreement ≥ 0.92

#### Recipe Card MM‑2: Failure‑Route Router

- **Use when** one modality degrades under conditions
- **Apply at** runtime inference
- **How:** Confidence‑based routing + dynamic fusion weights
- **Watch out:** Requires calibration
- **Validate:** Bias migration ≤ 1%

#### Recipe Card MM‑3: Modality Dropout Training

- **Use when** input availability varies by user group
- **Apply at** training
- **How:** Random modality dropout → robust fusion
- **Watch out:** Excess dropout reduces accuracy
- **Validate:** Parity across modality subsets

### 5.7 Recipe Summary

|  | Stage | Primitive | Purpose | Typical Parameter Range |
|---|--------|--------|--------|--------|
| 1 | Fusion | Cross‑modal consistency loss | Align modalities | 1.0–2.0 |
| 2 | Runtime | Failure‑route router | Skip unreliable modality | Conf ≥ 0.65 |

#### Validation Targets  

- Agreement ≥ 0.92
- Bias migration ≤ 1%

---

<a id="cross"></a>
## 6️⃣ Cross-Architecture Reusable Primitives  

- **Group-Aware Reweighting** - equalizes sample influence
- **Counterfactual Synthesis** - swap protected attributes
- **Slice-Wise Evaluation Harness** - systematic subgroup audits
- **Bias‑sensitive Early Stopping** - halt when fairness regresses
- Fairness Monitoring Pipelines  

---

<a id="intersectionality"></a>
## 7. Intersectionality Integration Layer    

Bias is strongest at **intersections of identities**, not single attributes.

### Implementation  

- Evaluate across **intersections**, not single attributes  
- Prioritize **high-risk slices**  
- Design **intersection‑aware metrics**

---

<a id="workflow"></a>
## 8. Implementation Workflow  

#### Step 1: Identify Architecture  
→ determine system type  

#### Step 2: Diagnose Bias Source
→ representation / data / dynamics  

#### Step 3: Apply Recipes  
→ architecture-specific interventions  

#### Step 4: Validate  
→ metrics + real-world scenarios

#### Step 5: Monitor   
→ continuous fairness tracking  

#### Step 6: Iterate  
→ adapt to new bias patterns  

---

<a id="principles"></a>
## 9. Core Principles  

- Fairness must be architecture-specific 
- Fix root causes  
- Layer interventions 
- Monitor continuously 
- Evaluate intersectionally 
- Balance fairness and performance  

---

<a id="refs"></a>
## 10. References

### General Fairness in Machine Learning

- Barocas, S., Hardt, M., & Narayanan, A. (2019).  
  *Fairness and Machine Learning: Limitations and Opportunities.*  
  https://fairmlbook.org  

- Mehrabi, N., Morstatter, F., Saxena, N., Lerman, K., & Galstyan, A. (2021).  
  *A Survey on Bias and Fairness in Machine Learning.*  
  ACM Computing Surveys.  

- Verma, S., & Rubin, J. (2018).  
  *Fairness Definitions Explained.*  
  IEEE/ACM Workshop on Software Fairness.  

---

### Large Language Models (LLMs)

- Bender, E. M., Gebru, T., McMillan-Major, A., & Shmitchell, S. (2021).  
  *On the Dangers of Stochastic Parrots: Can Language Models Be Too Big?*  
  FAccT Conference.  

- Sheng, E., Chang, K. W., Natarajan, P., & Peng, N. (2019).  
  *The Woman Worked as a Babysitter: On Biases in Language Generation.*  
  EMNLP.  

- Schick, T., Udupa, S., & Schütze, H. (2021).  
  *Self-Diagnosis and Self-Debiasing for Language Models.*  
  arXiv.  

---

### Recommendation Systems

- Ekstrand, M. D., Burke, R., & Diaz, F. (2022).  
  *Fairness in Recommendation Systems.*  
  Foundations and Trends in Information Retrieval.  

- Abdollahpouri, H., Burke, R., & Mobasher, B. (2020).  
  *Managing Popularity Bias in Recommender Systems with Personalized Re-ranking.*  
  AAAI Conference.  

- Burke, R. (2017).  
  *Multisided Fairness for Recommendation.*  
  FATREC Workshop.  

---

### Vision Models

- Buolamwini, J., & Gebru, T. (2018).  
  *Gender Shades: Intersectional Accuracy Disparities in Commercial Gender Classification.*  
  FAT Conference.  

- Wilson, B., Hoffman, J., & Morgenstern, J. (2019).  
  *Predictive Inequity in Object Detection.*  
  arXiv.  

- Zhao, J., Wang, T., Yatskar, M., Ordonez, V., & Chang, K. W. (2017).  
  *Men Also Like Shopping: Reducing Gender Bias Amplification in Image Recognition.*  
  ICCV.  

---

### Multi-Modal Systems

- Baltrušaitis, T., Ahuja, C., & Morency, L. P. (2019).  
  *Multimodal Machine Learning: A Survey and Taxonomy.*  
  IEEE TPAMI.  

- Liang, P. P., Wu, Y., Morency, L. P., & Salakhutdinov, R. (2022).  
  *Towards Robust and Fair Multimodal Learning.*  
  ICML.  

---

### Evaluation, Monitoring, and ML Systems

- Sculley, D. et al. (2015).  
  *Hidden Technical Debt in Machine Learning Systems.*  
  NeurIPS.  

- Breck, E. et al. (2017).  
  *The ML Test Score: A Rubric for ML Production Readiness.*  
  IEEE Big Data.  

- Mitchell, M. et al. (2019).  
  *Model Cards for Model Reporting.*  
  arXiv.  

---

### Practical & Industry Approaches

- Google AI.  
  *Responsible AI Practices.*  
  https://ai.google/responsibilities/responsible-ai-practices/  

- Microsoft.  
  *Responsible AI Standard v2.*  

---

### Additional Concepts Referenced

- Counterfactual Fairness (Kusner et al., 2017)  
- Exposure Fairness in Ranking Systems  
- Intersectional Fairness (Crenshaw, 1989 – conceptual foundation)  

---

---
