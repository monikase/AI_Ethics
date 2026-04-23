# Case Study: Applying the Fair AI Scrum Toolkit (FAST)  
## AI Resume Screening System – EquiHire (Sunshine Regiment)

## 1. Context

This case study demonstrates how the **Fair AI Scrum Toolkit (FAST)** was applied by the Sunshine Regiment team to develop an AI-based resume screening system at EquiHire.

The objective was to ensure that fairness is:

- embedded in daily development workflows  
- consistently implemented across features  
- validated before deployment  

## 2. Initial Problem

Before FAST implementation, the team:

- completed a fairness audit  
- identified bias risks  
- reviewed mitigation strategies  

However, they failed to execute effectively due to:

- unclear responsibilities  
- lack of integration into Scrum  
- no clear timing for fairness tasks  
- no enforcement mechanisms  

Result:

- fairness work was delayed  
- inconsistent decisions were made  
- bias risks remained unresolved  

## 3. Applying Fair AI Scrum Toolkit

FAST was introduced to embed fairness directly into Scrum workflows.

The implementation followed four key changes:

1. Redesigning user stories  
2. Adding fairness validation criteria  
3. Enforcing Definition of Done  
4. Modifying Scrum ceremonies  

---

## 4. Step 1: SAFE User Stories

Fairness was integrated into user stories using the SAFE template.

---

### User Story Enhanced:

> As a hiring manager,
> I want to filter candidates by experience level  
> so that I can focus on qualified applicants, 
> while ensuring equivalent filtering accuracy across gender and age groups.

**SAFE** Applied:

S - Protected attributes (Gender, Age)  
A - Equal Opportunity  
F - Model training and feature selection
E - Bias report generated per sprint

---

## 5. Step 2: FAIR Acceptance Criteria

Each story included explicit fairness validation requirements.

### Example Criteria

- TPR difference ≤ 0.03 across gender and age groups  
- Intersectional analysis completed  
- Results documented in model card  
- Fairness report generated  

---

## 6. Step 3: Backlog Integration

Fairness tasks were explicitly included in sprint backlog:

- subgroup fairness evaluation  
- bias mitigation tasks  
- documentation and reporting  

Each item was linked to:

- FDR (decision)  
- risk tier (RCG)  

---

## 7. Step 4: Definition of Done (DoD)

Fairness validation was required before any feature could be completed.

---

### Example DoD Conditions

- fairness metrics meet thresholds  
- intersectional evaluation completed  
- mitigation applied if necessary  
- model card updated  
- audit evidence generated  

---

### Impact

- biased features could not reach production  
- fairness became enforceable  
- compliance was built into development  

---

## 8. Step 5: Ceremony Adaptations

---

### Sprint Planning

- reviewed fairness risks for each story  
- assigned fairness responsibilities  
- aligned with FDR  

---

### Daily Standups

- tracked fairness blockers  
- monitored validation progress  

---

### Sprint Review

- presented fairness metrics  
- demonstrated subgroup performance  
- discussed mitigation outcomes  

---

### Retrospective

- identified missed bias risks  
- improved fairness processes  
- addressed knowledge gaps  

---

### Impact

- fairness became part of team discussions  
- issues surfaced early  
- continuous improvement enabled  

---

## 9. Role-Based Responsibilities

---

### Product Owner

- ensured all stories included fairness requirements  
- prioritized fairness tasks  

---

### Scrum Master

- enforced fairness in ceremonies  
- escalated unresolved issues  

---

### Developers / Data Scientists

- implemented bias testing  
- applied mitigation strategies (AAC)  
- validated fairness metrics  
- documented results  

---

### Impact

- clear ownership established  
- accountability distributed  
- no gaps in responsibility  

---

## 10. Results

---

### Before FAST

- fairness not integrated into workflow  
- unclear responsibilities  
- inconsistent implementation  

---

### After FAST

- fairness embedded in Scrum  
- clear roles and responsibilities  
- measurable validation  
- consistent implementation  

---

### Key Improvements

| Metric | Before | After |
|------|--------|------|
| Fairness integration | Low | High |
| Task clarity | Low | High |
| Validation coverage | Inconsistent | Systematic |
| Bias resolution | Reactive | Proactive |

---

## 11. Key Insights

---

### 1. Fairness must be part of requirements
SAFE stories ensured fairness is defined upfront.

---

### 2. Validation must be mandatory
FAIR criteria and DoD enforced measurable fairness.

---

### 3. Visibility drives execution
Backlog integration ensured fairness work is not ignored.

---

### 4. Responsibility must be explicit
Role definition prevented gaps and confusion.

---

## 12. Conclusion

The Fair AI Scrum Toolkit successfully transformed fairness from:

❌ a separate, unclear process  
➡️  
✅ a structured, enforceable part of daily development  

FAST enabled the Sunshine Regiment team to:

- implement fairness consistently  
- validate outcomes systematically  
- deliver a fair and compliant AI system  

---

## Final Statement

FAST ensures that fairness is not just designed, but:

👉 **planned, executed, validated, and enforced within everyday development workflows**
