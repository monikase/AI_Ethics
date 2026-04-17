# Advanced Architecture Cookbook  

Fairness fails in practice when **interventions ignore architecture.** This cookbook turns fairness into an **architecture‑aware engineering discipline** with actionable recipes for **LLMs, Recommendation Systems, Vision Models, and Multi‑Modal systems.** It complements team‑level (Scrum) and org‑level (governance) toolkits by focusing on **how systems work**, not just what they output.

## Business Value

Embedding fairness at the architecture level enables:

- **Robustness:** Stable performance across groups and real‑world conditions
- **Prevention over patching:** Fix bias at representation, dynamics, and fusion layers
- **Reuse at scale:** Proven patterns instead of bespoke fixes
- **Risk reduction:** Fewer hidden failures in advanced architectures
- **Better Product Quality:** Fairness often improves generalization

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

This cookbook ensures fairness is implemented **correctly at the system level**.  

## Cookbook Map  

### 1️⃣ [How to Use This Cookbook](#usage)  
### 2️⃣ [Large Language Models (LLM) Suite](#llm)  
### 3️⃣ [Recommendation Systems Suite](#recsys)  
### 4️⃣ [Vision Models Suite](#vision)  
### 5️⃣ [Multi-Modal Systems Suite](#multimodal)  
### 6️⃣ [Cross-Architecture Primitives](#cross)  
### 7️⃣ [Intersectionality Layer](#intersectionality)  
### 8️⃣ [Implementation Workflow](#workflow)  
### 9️⃣ [Core Principles](#principles)  

---

<a id="usage"></a>
## 1️⃣ How to Use This Cookbook  
→ Apply the right fairness strategy for the right architecture  

---

### 1.1 Identify Architecture  

Determine which system you are working with:

- **LLM** → generates open‑ended text  
- **Recommendation System (RecSys)** → ranks or suggests items over time
- **Vision Model** → images/video perception 
- **Multi-Modal System** → combines multiple data types (text + vision + audio (or more)) 

### 1.2 Diagnose Where Bias Originates 

- **Data** (imbalance, environment)  
- **Representation** (latent features)  
- **System Dynamics** (feedback loops)  
- **Interaction** (prompts, users, modalities)  

### 1.3 Select Interventions (Architecture‑Aligned)

- **LLM** → prompting, fine‑tuning, decoding, guardrails 
- **RecSys** → exposure control, feedback management 
- **Vision** → environment, representation probing 
- **Multi-modal** → fusion balance, routing

### 1.4 Validate

Evaluate fairness using:

- **Architecture-specific metrics**  
- **Intersectional analysis**  
- **Real-world scenario testing**

### 1.5. Minimum Viable Use (Time‑Constrained Teams)

1. Identify architecture
2. Scan common issues
3. Pick **one recipe** 
4. Validate with **one metric**
5. Log assumptions and risks

### 1.6 Who Uses What

- **ML Engineers** → Implementation + Evaluation
- **Product** → Trade‑offs + Risk
- **QA/Risk** → Validation + Monitoring


> **Key Principle:** Target **how the system works**, not just outputs.

### 1.7 How to Use Recipe Cards  
Recipe cards are designed as **decision guides for engineering teams**. Each card answers _when_ a technique should be used, _where_ it fits in the system pipeline, _how_ to apply it safely, and _what to monitor_ afterward. Teams should select recipe cards based on their system’s architecture and observed failure modes, adapt parameters within the suggested ranges, and only combine multiple cards after validating each intervention independently.

> These recipe cards illustrate common architectural fairness
> patterns and are not exhaustive; teams should adapt or extend
> them as new failure modes emerge.

---

<a id="llm"></a>
## 2️⃣ Large Language Models (LLM) Suite  
→ Fairness in generative systems  

---

### 2.1 When to Use

- Text generation/analysis
- Context‑dependent bias
- Tone/framing disparities

### 2.2 Common Fairness Issues  

|  | Category | Symptom | Impact |
|---|--------|--------|--------|
| 1 | Stylistic Stereotyping | Biased associations (Supportive tone for women, directive tone for men) | Harmful narratives, Reinforces social norms |
| 2 | Association Bias | Different tone per group (Certain skills linked to demographics) | Skewed evaluations |
| 3 | Prompt Sensitivity | Fairness varies by phrasing (Small phrasing changes alter fairness) | Inconsistent outcomes |
| 4 | Sycophancy | Model agrees with biased input | Bias amplification |
| 5 | Hallucination Bias | False biased outputs (Fabricated demographic-skewed facts) | Harm/Misinformation |

### 2.3 Frequent Mistakes

1. Relying on classification fairness metrics for generative outputs
2. Auditing only one prompt template
3. Treating RLHF as sufficient without prompt controls
4. Ignoring decode‑time bias emergence
5. Assuming neutrality from "professional" tone

### 2.4 Why LLMs Are Special

- Generative freedom creates infinite surface area for bias
- Prompt‑conditioned behavior makes fairness contextual
- Emergent properties appear only at scale
- Decoding choices shape fairness as much as training

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

### 2.6 Selected Recipe Cards

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

### 2.7 Example (Resume Summaries)

- **Before:** Male → “strong leader”; Female → “collaborative communicator”
- **After:** Vocabulary parity via counterfactual prompting + rerank

---

<a id="recsys"></a>
## 3️⃣ Recommendation Systems Suite  
→ Fairness in dynamic systems with feedback loops  

---

### 3.1 When to Use

- Ranking/personalization with user feedback

### 3.2 Core Fairness Challenge  

Recommendation systems:
- **shape user behavior over time**  
- create **feedback loops**  
- control **visibility and exposure**  

→ **Exposure allocation** + **feedback loops** amplify historical bias over time

### 3.3 Where Bias Enters

1) Retrieval → 2) **Ranking (exposure)** → 3) Interaction → 4) Retraining


### 3.4 Common Fairness Issues  

|  | Category | Symptom | Impact |
|---|--------|--------|--------|
| 1 | Exposure Bias | Same items dominate rankings | Unequal opportunity |
| 2 | Feedback Loops | Popularity reinforces itself | Structural segregation |
| 3 | Filter Bubbles | Narrow content paths | Limited opportunities |
| 4 | Provider Bias | Unequal visibility (Some providers rarely shown) | Economic harm |

### 3.5 Frequent Mistakes

- Auditing CTR instead of exposure distribution
- Ignoring long‑term feedback loops
- Treating users as the only stakeholder
- Applying static constraints to dynamic systems

### 3.6 Why Recommendation Systems Are Special

- **They actively shape user behavior**
- **Fairness unfolds over time**, not per decision
- **Multiple stakeholders** have competing fairness claims

### 3.7 Recipe Summary

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


### 3.8 Selected Recipe Cards

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

---

<a id="vision"></a>
## 4️⃣ Vision Models Suite  
→ Fairness in perception systems  

---

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

### 4.6 Recipe Summary

|  | Stage | Primitive | Purpose | Typical Parameter Range |
|---|--------|--------|--------|--------|
| 1 | Augment | Style‑transfer equalizer | Balance lighting/textures | 0.2–0.4 |
| 2 | Audit | Prototype leak probe | Quantify leakage | Leak < 0.02 |
| 3 | Remediate | Layer reinitialization | Remove leaking block | n/a |

#### Validation Targets
  
- Accuracy gap < 5%
- Leak AUC ≤ 0.52
- Robustness variance ≤ 10%


### 4.7 Selected Recipe Cards
 
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

---

<a id="multimodal"></a>
## 5️⃣ Multi-Modal Systems Suite  
→ Fairness in systems combining modalities  

---

### 5.1 When to Use

- Text/vision/audio combined

### 5.2 Core Fairness Challenge  

Multi-modal systems:
- combine multiple biased sources  
- create **new bias through interaction**  

→ Bias is **emergent at fusion**; modalities fail differently.

### 5.3 Coordination Rule

**Never debias modalities in isolation.** Order: Fix weakest modality → validate → adjust fusion → end‑to‑end check.

### 5.4 Common Fairness Issues  

|  | Category | Symptom | Impact |
|---|--------|--------|--------|
| 1 | Bias Transfer | One bias infects others (e.g. Vision bias misleads text) | Compounded harm |
| 2 | Missing Modality Fallback | Failure when input missing; Model fails when one stream unavailable (e.g., low-light video) | Unequal performance |
| 3 | Inconsistent Predictions | Conflicting signals | User confusion |  
| 4 | Dominant Modality | One input dominates | Narrow representations |

### 5.5 Frequent Mistakes

- Neglecting confidence‑based routing
- Skipping recalibration after modality dropout
- Debiasing modalities independently

### 5.6 Why Multi‑Modal Systems Are Special

- Shared latent space amplifies hidden bias
- Each modality fails differently
- Unequal data availability creates unequal treatment

### 5.7 Recipe Summary

|  | Stage | Primitive | Purpose | Typical Parameter Range |
|---|--------|--------|--------|--------|
| 1 | Fusion | Cross‑modal consistency loss | Align modalities | 1.0–2.0 |
| 2 | Runtime | Failure‑route router | Skip unreliable modality | Conf ≥ 0.65 |

#### Validation Targets  

- Agreement ≥ 0.92
- Bias migration ≤ 1%

### 5.8 Selected Recipe Cards

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

---

<a id="cross"></a>
## 6️⃣ Cross-Architecture Reusable Primitives  
→ Shared fairness techniques  

---

- **Group-Aware Reweighting** - equalizes sample influence
- **Counterfactual Synthesis** - swap protected attributes
- **Slice-Wise Evaluation Harness** - systematic subgroup audits
- **Bias‑sensitive Early Stopping** - halt when fairness regresses
- Fairness Monitoring Pipelines  

---

<a id="intersectionality"></a>
## 7. Intersectionality Integration Layer  
→ Address real-world complexity  

---

Bias is strongest at **intersections of identities**, not single attributes.

### Implementation  

- Evaluate across **intersections**, not single attributes  
- Prioritize **high-risk slices**  
- Design **intersection‑aware metrics**

---

<a id="workflow"></a>
## 8. Implementation Workflow  

---

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

---

- Fairness must be architecture-specific 
- Fix root causes  
- Layer interventions 
- Monitor continuously 
- Evaluate intersectionally 
- Balance fairness and performance  

---



---
