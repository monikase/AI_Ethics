# Case Study: Fairness Implementation in AI-Based Recruitment System  
### EquiHire Resume Screening, Interviewing, and Matching Platform

---

## 1. System Context

This case study demonstrates the application of the **Fairness Implementation Playbook** to a multi-team AI recruitment platform at EquiHire.  
  
EquiHire operates a multi-stage AI recruitment platform consisting of three integrated systems:  

#### **Resume Screening System (Sunshine Regiment)**  
- **Type:** LLM-assisted ranking pipeline
- **Input:** Candidate CVs, structured profiles
- **Output:** Ranked shortlist + generated candidate summaries
- **Decision Impact:** Determines which candidates proceed to interview

#### **AI Interviewing System (Chaos Legion)**  
- **Type:** Multi-modal evaluation system
- **Input:** Video, audio, transcript
- **Output:** Candidate scores across competencies
- **Decision Impact:** Influences hiring decisions directly

#### **Candidate-Job Matching System (Dragon Army)** 
- **Type:** Recommendation system
- **Input:** Candidate profiles + job postings
- **Output:** Ranked job recommendations
- **Decision Impact:** Shapes candidate visibility and opportunity access

The objective is to ensure **consistent, scalable, and auditable fairness** across all systems while maintaining performance and usability.

---

## 2. Trigger Event

Despite having:
- a Fairness Audit Playbook  
- a Fairness Intervention Playbook  

Fairness implementation was not initiated proactively.  

It was triggered by three independent signals:  

- **Legal escalation:** EU AI Act classification flagged recruitment systems as high-risk
- **User complaints:** Recruiters reported inconsistent candidate quality across demographics
- **Metric anomaly:** Internal audit revealed a 12% lower selection rate for candidates aged 50+

These signals exposed:

- Inconsistent fairness definitions across teams
- Lack of traceability between decisions and implementation
- Absence of fairness validation in sprint workflows

---

## 3. Applying the Fairness Implementation Playbook

The organization adopted a structured approach aligned with the lifecycle defined in the playbook:  

**Risk → Decision → Implementation → Mitigation → Validation → Monitoring**

---

## 4. Step 1: Risk Classification (RCG) 

### 4.1 Execution Process

The **Fairness Program Manager** initiated TRS calculation during planning phase.  
  
Each system owner completed a structured assessment in Jira using the RCG scoring model:  
  
TRS = (Probability × Severity) + Exposure – Mitigation Readiness

### 4.2 Results

| System | P | S | E | M | TRS | Tier |
|--------|---|---|---|---|-----|------|
| Resume Screening | 4 | 4 | 2 | 2 | 20 | High (Tier 2) |
| Interviewing AI | 5 | 4 | 3 | 1 | 22 | Critical (Tier 1) |
| Matching System | 4 | 3 | 3 | 2 | 17 | High (Tier 2) |

### 4.3 Operational Impact

TRS classification trigerred:

- Mandatory governance gate approval before development
- Required artifacts:
    - Fairness Decision Records (FDRs)
    - Model Cards
    - Bias Reports
- Deployment blocked until:
    - fairness thresholds defined
    - validation plan approved

All TRS records were stored in Jira and linked to system IDs.

---


## 5. Step 2: Fairness Decision-Making (OIT)  

### 5.1 Governance Trigger

Following TRS classification, all three systems were placed under **Tier 1–2 governance gates**, requiring:  

- formal fairness definition
- documented trade-offs
- approved validation metrics

The **Fairness Program Manager** initiated a cross-system governance process to establish consistent but **system-appropriate fairness decisions**.  

#### 5.2 Governance Structure & Participants

A Fairness Guild session was convened with:

- Product Owners (all three systems)
- Data Science Leads
- Legal Counsel
- Fairness Program Manager (facilitator)
- Technical Fairness Lead

#### 5.3 Decision: System-Specific Fairness via Multiple FDRs

The Fairness Guild established a key principle:  

Fairness must be defined per system and decision type, not globally.  

As a result, three separate Fairness Decision Records (FDRs) were created.  

#### I. FDR-012 — Resume Screening System

```
System: Resume Screening (LLM Ranking)
  
Decision: Equal Opportunity
  
Metric: True Positive Rate (TPR) difference  
Threshold: ≤ 0.03 across gender and age  
  
Trade-off: Accept ≤ 2% recall reduction
  
Rationale: System filters candidates → fairness must ensure equal chance of selection for qualified individuals  
  
Rejected Alternatives:  
- Demographic parity → misaligned with hiring utility  
- Equalized odds → unstable under class imbalance  
  
Stakeholders:  
- Product Owner (Responsible)  
- Fairness Guild (Accountable)  
- Legal (Consulted)
```

#### II. FDR-013 — Interviewing System

```
System: AI Interviewing (Multi-Modal Scoring)
  
Decision: Error Rate Parity
  
Metric: Absolute scoring error difference across groups  
Threshold: ≤ 0.05  
  
Trade-off: Allow minor variance in score calibration
  
Rationale: All candidates are evaluated → fairness must ensure equal scoring accuracy rather than selection parity    
  
Rejected Alternatives:  
- Equal Opportunity → not applicable (no filtering stage)  
- Demographic parity → irrelevant to scoring systems  
  
Stakeholders:  
- Product Owner (Responsible)  
- Fairness Guild (Accountable)  
- Legal + UX Research (Consulted)  
```

#### III. FDR-014 — Matching System

```
System: Candidate-Job Matching (Recommendation System)
  
Decision: Exposure Parity  
  
Metric: Exposure distribution difference  
Threshold: ≤ ±15% across demographic groups  
  
Trade-off: Accept minor CTR reduction  
  
Rationale: System influences visibility → fairness must ensure equal opportunity of exposure over time     
  
Rejected Alternatives:  
- Equal Opportunity → not applicable (no binary selection)  
- Accuracy-only optimization → amplifies feedback loops  
  
Stakeholders:  
- Product Owner (Responsible)  
- Fairness Guild (Accountable)  
- Data Science Lead (Consulted)   
```

### 5.4 Traceability Setup (Cross-System)

All FDRs were:

- stored in a **version-controlled repository**
- assigned unique IDs (FDR-012, FDR-013, FDR-014)
- linked to:
    - Jira epics and FAIR tasks
    - model experiments (MLflow)
    - validation reports
    - audit logs

---

## 6. Step 3: Team-Level Implementation (FAST)

### 6.1 Sprint Context

Following governance decisions (FDR-012, FDR-013, FDR-014), fairness implementation was executed during initial Sprint 1, involving three parallel teams:

- Resume Screening Team
- Interviewing System Team
- Matching System Team

Each team operated independently but followed the same FAST framework, **using their respective FDRs** as the single source of truth.


### 6.2 Sprint Planning (Cross-Team)
#### 6.2.1 Joint Fairness Planning Session

A cross-team planning session was conducted with:

- Product Owners (3 systems)
- Data Science Leads
- ML Engineers
- QA Engineers
- Fairness Program Manager

#### 6.2.2 Fairness Risk Identification

Each team evaluated its feature backlog against its assigned FDR:

| System        | Feature                 | Key Fairness Risk                          |
|--------------|------------------------|--------------------------------------------|
| Screening    | Candidate Ranking v2   | Selection bias from historical labels      |
| Interviewing | Interview Scoring v3   | Inconsistent scoring across demographics   |
| Matching     | Job Recommendation v5  | Unequal exposure and feedback loops        |

---

### 6.2.3 Capacity Allocation

Based on risk tiers:

- **Screening (Tier 2):** 20% fairness capacity  
- **Interviewing (Tier 1):** 30% fairness capacity  
- **Matching (Tier 2):** 20% fairness capacity  

---

### 6.2.4 Backlog Creation (Per System)

#### I. Resume Screening (FDR-012)

```
- FAIR-SCR-101: Compute TPR by gender  
- FAIR-SCR-102: Compute TPR by age  
- FAIR-SCR-103: Intersectional analysis (gender × age)  
- FAIR-SCR-104: Apply sample reweighting  
- FAIR-SCR-105: Validate fairness thresholds
```

#### II. Interviewing System (FDR-013)

```
- FAIR-INT-201: Compute scoring error by group  
- FAIR-INT-202: Evaluate cross-modal bias (audio vs video vs text)  
- FAIR-INT-203: Intersectional error analysis  
- FAIR-INT-204: Adjust scoring calibration  
- FAIR-INT-205: Validate error parity threshold  
```

#### III. Matching System (FDR-014)

```
- FAIR-MAT-301: Measure exposure distribution across groups  
- FAIR-MAT-302: Analyze feedback loop amplification  
- FAIR-MAT-303: Intersectional exposure analysis  
- FAIR-MAT-304: Implement exposure-aware ranking  
- FAIR-MAT-305: Validate exposure parity threshold  
````

**All backlog items were tagged:**

```
FAIRNESS | HIGH-RISK | FDR-linked
```

---

### 6.3 SAFE User Stories (Per System)

#### I. Resume Screening

```
As a recruiter,  

I want candidates ranked by relevance,  

so that I can shortlist efficiently,  

while ensuring equal opportunity across gender, age, and their intersections.  
```

#### II. Interviewing System

```
As a hiring manager,  

I want interview scores to reflect candidate ability,  

so that I can make fair hiring decisions,  

while ensuring consistent scoring accuracy across demographic groups.  
```

#### III. Matching System

```
As a job seeker,  

I want to receive relevant job recommendations,  

so that I can find suitable opportunities,  

while ensuring fair exposure across demographic groups over time.  
```

### 6.4 FAIR Acceptance Criteria (Per System)

#### I. Screening (FDR-012)

- TPR difference ≤ 0.03  
- Intersectional evaluation completed  
- Bias report linked to FDR-012  

#### II. Interviewing (FDR-013)

- Error rate difference ≤ 0.05  
- Cross-modal consistency validated  
- Intersectional scoring analysis completed  

#### III. Matching (FDR-014)

- Exposure difference ≤ ±15%  
- Longitudinal exposure evaluated  
- Diversity gain ≥ 30%  

---

### 6.5 Mid-Sprint Fairness Checkpoints

#### Screening Results
- TPR gap (age 50+) = **0.08 → FAIL**

#### Interviewing Results
- Error variance across groups = **0.07 → FAIL**

#### Matching Results
- Exposure gap = **28% → FAIL**

---

### 6.6 Blockers & Escalation

All three systems failed fairness thresholds mid-sprint.

**Actions:**

- Flagged as **DoD violations**  
- Escalated to:
  - Product Owners  
  - Fairness Guild  

**Decision:**

> Continue mitigation within sprint, block release for all three systems  

---

### 6.7 Mitigation Execution

#### Screening
- Sample reweighting  
- Counterfactual data augmentation  

#### Interviewing
- Recalibration of scoring function  
- Modality weighting adjustments  

#### Matching
- Exposure-aware ranking  
- Controlled exploration (ε = 0.1)  

---

### 6.8 Final Validation (End of Sprint)

| System        | Metric        | Before | After | Status |
|--------------|--------------|--------|-------|--------|
| Screening    | TPR gap      | 0.08   | 0.02  | PASS   |
| Interviewing | Error gap    | 0.07   | 0.04  | PASS   |
| Matching     | Exposure gap | 28%    | 12%   | PASS   |

---

### 6.9 Definition of Done Enforcement

A unified rule applied across teams:

> **A feature is NOT complete unless fairness criteria are satisfied.**

All three systems:

- Failed initial validation  
- Required mitigation  
- Passed only after re-evaluation  

No system was allowed to deploy prematurely.

---

### 6.10 Daily Execution Dynamics (Observed)

During the sprint:

- Fairness blockers were raised in daily standups  
- Progress tracked via fairness dashboards  
- Mid-sprint checkpoints prevented late-stage surprises  

**Example blocker:**

> “Exposure metrics unstable due to feedback loop — requires ranking redesign”

---

### 6.11 Cross-Team Coordination Insight

Despite different systems:

- All teams followed identical **process structure (FAST)**  
- But implemented **different fairness definitions and techniques**  

This enabled:

- Consistency in execution  
- Flexibility in implementation  

---

### 6.12 Key Outcome

FAST enabled fairness to become:

- Visible in backlog  
- Measurable in acceptance criteria  
- Enforceable through Definition of Done  

Across all systems simultaneously.

---

## 7. Step 4: Technical Mitigation (AAC)  

Following mid-sprint validation failures (Section 4), each team applied **architecture-specific mitigation strategies** from the Advanced Architecture Cookbook (AAC).

All interventions were:

- triggered by FAIR validation failures  
- guided by system-specific FDRs  
- implemented at the appropriate pipeline stage  

---

## 7.1 Resume Screening System (LLM Pipeline)

**FDR Reference:** FDR-012 (Equal Opportunity)

---

### 7.1.1 Failure Diagnosis

Bias was detected in generated candidate summaries:

- Male candidates → “leader”, “driven”  
- Female candidates → “supportive”, “collaborative”  

**Root Cause (AAC Diagnosis):**

- Prompt-conditioned generation bias  
- Latent association bias in training data  
- Decode-time amplification of stereotypes  

---

### 7.1.2 Intervention (AAC Recipes Applied)

- Counterfactual prompting  
- Self-critique + reranking  

---

### 7.1.3 Pipeline Integration

```
Input CV  
→ Prompt construction  
→ Generate summary  
→ Counterfactual swap (gender attributes)  
→ Compare outputs  
→ Fairness scoring  
→ Re-rank or regenerate if inconsistent  
→ Final output  
```

---

### 7.1.4 Validation

- Counterfactual consistency: **91%** (target ≥ 90%)  
- Tone variance reduced across gender groups  
- TPR fairness (FDR-012) satisfied after mitigation  

---

## 7.2 Interviewing System (Multi-Modal Scoring)

**FDR Reference:** FDR-013 (Error Rate Parity)

---

### 7.2.1 Failure Diagnosis

Bias observed in scoring consistency:

- Higher error rates for specific demographic groups  
- Inconsistent weighting across modalities (audio vs video vs text)  

**Root Cause (AAC Diagnosis):**

- Modality imbalance (audio more influential than text)  
- Representation bias in embeddings  
- Noise sensitivity in speech signals  

---

### 7.2.2 Intervention (AAC Recipes Applied)

- Cross-modal calibration  
- Modality weighting adjustment  
- Bias-aware loss rebalancing  

---

### 7.2.3 Pipeline Integration

```
Input (video, audio, transcript)  
→ Feature extraction per modality  
→ Modality weighting layer (adjusted)  
→ Scoring model  
→ Error calibration layer  
→ Final score output  
```

---

### 7.2.4 Validation

- Error gap reduced: **0.07 → 0.04** (threshold ≤ 0.05)  
- Cross-modal consistency improved  
- Intersectional error variance reduced  

---

## 7.3 Matching System (Recommendation Engine)

**FDR Reference:** FDR-014 (Exposure Parity)

---

### 7.3.1 Failure Diagnosis

Bias detected in recommendation exposure:

- Certain groups underrepresented in top-ranked results  
- Reinforcement of historical popularity  

**Root Cause (AAC Diagnosis):**

- Feedback loop amplification  
- Position bias in ranking  
- Lack of exploration  

---

### 7.3.2 Intervention (AAC Recipes Applied)

- Exposure-aware ranking  
- Controlled exploration (ε = 0.1)  

---

### 7.3.3 Pipeline Integration

```
Candidate pool  
→ Initial relevance ranking  
→ Exposure adjustment layer  
→ Exploration injection (ε-greedy)  
→ Final ranked recommendations  
```

---

### 7.3.4 Validation

- Exposure gap reduced: **28% → 12%** (threshold ≤ ±15%)  
- Diversity increased: **+34%**  
- Longitudinal exposure distribution stabilized  

---

## 7.4 Cross-System Insight

Although each system required different interventions:

- LLM → generation-level bias control  
- Multi-modal → representation and calibration correction  
- Recommendation → ranking and exposure adjustment  

All mitigations followed the same AAC logic:

1. Identify architecture  
2. Diagnose bias source  
3. Apply targeted intervention  
4. Validate against FDR-defined metrics  

---

---

## 8. Step 5: Validation & Compliance (RCG + FAST)

Following technical mitigation across all three systems (Section 5), validation outputs were transformed into compliance artifacts and enforced through automated regulatory integration.

All validation and compliance activities were explicitly derived from:

- **FDR-012** (Resume Screening — Equal Opportunity)  
- **FDR-013** (Interviewing — Error Rate Parity)  
- **FDR-014** (Matching — Exposure Parity)  

This ensured alignment between governance (OIT), implementation (FAST), technical mitigation (AAC), and regulatory compliance (RCG).

---

### 8.1 Regulatory Mapping Integration

Using the Regulatory Mapping Framework, each SDLC phase was aligned with EU AI Act requirements and translated into concrete engineering tasks.

All mappings were tied to system-specific FDRs, ensuring that regulatory compliance reflected **context-specific fairness definitions**.

#### Planning Phase
- **Art 9(1)** → TRS calculated for all three systems before development  
- **Art 9(2)** → mitigation controls mapped to risk tiers (Tier 1–2)  
- **GDPR Art 35** → DPIA completed for Screening, Interviewing, and Matching  

#### Data Ingestion
- Dataset representativeness validated across all systems  
- Bias detection pipelines generated subgroup reports:
  - Screening → label imbalance  
  - Interviewing → modality bias  
  - Matching → exposure distribution  

#### Model Training
- Model cards generated per system:
  - Screening → TPR metrics  
  - Interviewing → error parity metrics  
  - Matching → exposure metrics  
- Training artifacts stored in immutable compliance storage  

#### Logging & Traceability
- All systems emitted:
  - prediction logs  
  - fairness metrics  
  - override actions  
- Unique IDs enabled traceability across systems  

#### Pre-Deployment Controls
- Human-in-the-loop enforced for hiring decisions  
- Override mechanisms implemented across systems  
- Deployment blocked until fairness thresholds satisfied  

#### Post-Deployment Monitoring
- Continuous fairness monitoring deployed:
  - Screening → TPR drift  
  - Interviewing → error variance  
  - Matching → exposure dynamics  

---

### 8.2 Validation-to-Compliance Transformation

Fairness validation outputs generated during FAST execution were automatically converted into compliance artifacts:

- Screening → TPR evaluation → bias report + model card (FDR-012)  
- Interviewing → error parity evaluation → calibration report (FDR-013)  
- Matching → exposure evaluation → ranking fairness report (FDR-014)  

This ensured compliance evidence was generated **continuously during development**, not after deployment.

---

### 8.3 Governance Gate Enforcement

Deployment across all systems was blocked unless:

- FDR-defined fairness thresholds were satisfied  
- required artifacts (model cards, bias reports, DPIA) were complete  
- traceability links across systems were verified  

This created a **unified compliance gate across all three systems**.

---

### 8.4 Documentation & Evidence Automation

Compliance artifacts were generated per system:

| System        | Key Artifacts                                      |
|--------------|---------------------------------------------------|
| Screening    | Model Card (TPR), Bias Report, Dataset Audit      |
| Interviewing | Model Card (Error Parity), Calibration Report     |
| Matching     | Model Card (Exposure), Ranking Fairness Report    |

All artifacts were:

- version-controlled  
- linked to FDRs  
- stored in centralized compliance repository  

---

### 8.5 Audit-Trail & Evidence Graph

A unified **Audit-Trail and Evidence Graph system** was implemented across all systems.

---

#### Audit-Trail Architecture

Each system emitted structured events:

- **Screening** → ranking outputs, TPR metrics  
- **Interviewing** → scoring outputs, modality metrics  
- **Matching** → recommendation exposure logs  

All events included:

- model version  
- dataset version  
- fairness metrics  
- linked FDR  

Each event was assigned a **trace ID** enabling cross-system linkage.

---

#### Evidence Graph Design

All events were connected into a unified graph:

```
Decision → Screening → Interviewing → Matching → Human Action
         ↓           ↓             ↓
       Model        Model         Model
         ↓           ↓             ↓
       Dataset      Dataset       Dataset
         ↓           ↓             ↓
     Fairness     Fairness     Fairness
      Metrics      Metrics      Metrics
```

---

#### Cross-System Traceability

The Evidence Graph captured dependencies:

- Screening outputs → feed Matching recommendations  
- Interviewing scores → influence hiring decisions  
- Shared FDRs → ensure consistent fairness objectives  

---

#### Example Decision Trace

```
Decision ID: HIRE-8472

├─ Screening System (Sunshine)
│   ├─ Model v1.3
│   ├─ TPR gap = 0.02 (FDR-012)
│   └─ Dataset version: DS-02

├─ Interviewing System (Chaos)
│   ├─ Model v2.1
│   ├─ Error gap = 0.04 (FDR-013)
│   └─ Cross-modal agreement = 0.94

├─ Matching System (Dragon)
│   ├─ Model v3.0
│   ├─ Exposure gap = 0.12 (FDR-014)
│   └─ Diversity gain = +34%

└─ Human Decision
    ├─ Recruiter: Approved
    └─ Reason: "Strong domain expertise"
```

---

#### Operational Use

The Evidence Graph supported:

- audit reconstruction  
- incident root cause analysis  
- cross-system fairness evaluation  
- verification of human oversight  

---

### 8.6 Continuous Compliance Review

Periodic validation cycles ensured sustained compliance:

- re-evaluation of TRS risk classification  
- verification of documentation completeness  
- audit-trail integrity validation  
- monitoring of fairness drift across all systems  

---

### 8.7 Operational Impact

- Compliance embedded across all systems simultaneously  
- Fairness validation aligned with system-specific definitions  
- Full cross-system traceability achieved  
- Regulatory readiness maintained continuously  

---

## 9. Step 6 — Monitoring & Incident Response

Continuous monitoring was deployed across all systems:

- Screening → TPR drift monitoring  
- Interviewing → error parity monitoring  
- Matching → exposure monitoring  

---

### Example Incident (Screening System)

- TPR for age 50+ increased from 0.02 → 0.06  
- Threshold violation detected automatically  

---

### Response Timeline

- Detection (< 15 min)  
- Triage (P2 classification, < 2 hours)  
- Containment (model rollback, < 24 hours)  
- Remediation (retraining, < 5 days)  

---

### Outcome

- Metric restored within threshold  
- Root cause (data drift) identified  
- FDR updated with additional monitoring constraints  
- Preventive alert added  

---

## 10. Results

### Before Implementation

- inconsistent fairness definitions  
- fragmented system behavior  
- reactive bias mitigation  

### After Implementation

- system-specific fairness definitions (FDRs)  
- unified implementation workflow (FAST)  
- architecture-aware mitigation (AAC)  
- audit-ready compliance (RCG)  

---

### Key Metrics Improvement

| Metric                          | Before | After |
|---------------------------------|--------|-------|
| TPR gap (Screening)             | 0.08   | 0.02  |
| Error gap (Interviewing)        | 0.07   | 0.04  |
| Exposure gap (Matching)         | 28%    | 12%   |
| Bias incident resolution time   | 18 days| 5 days|
| Audit readiness                 | Low    | High  |
| Cross-system consistency        | Low    | High  |

---

## 11. Key Insights

#### 1. Fairness must be operational, not conceptual
Embedding fairness into Scrum (FAST) was critical.

#### 2. Governance prevents fragmentation
FDRs ensured consistent decisions across teams.

#### 3. Architecture matters
Generic fairness methods failed without AAC.

#### 4. Compliance must be built-in
RCG ensured fairness was auditable, not assumed.

---

## 12. Conclusion

This case study demonstrates that fairness can be:

- systematically implemented  
- scaled across teams  
- validated and audited  

when integrated across:

- FAST (execution)  
- OIT (governance)  
- AAC (technical implementation)  
- RCG (compliance)  

---
