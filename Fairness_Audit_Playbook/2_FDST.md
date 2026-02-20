# Fairness Definition Selection Tool

## 1. Introduction

The Fairness Definition Selection Tool helps teams **select appropriate fairness definitions for AI systems** based on application context, stakeholder priorities, legal requirements, and technical constraints.

Because fairness definitions reflect different values and are often mathematically incompatible, choosing one is not purely a technical decision.  
The tool ensures that fairness metric selection is explicit, justified, and documented.

As the second component of the Fairness Audit Playbook, it is **applied after the Historical Context Assessment and before model optimization**.

## 2. Objectives
- Translate abstract fairness definitions into practical selection criteria
- Map application characteristics to appropriate fairness definitions
- Make fairness trade-offs explicit and documented
- Align fairness metric selection with legal and ethical constraints
- Provide a structured method for navigating incompatibilities

## 3. Tool Overview
The Fairness Definition Selection Tool consists of four components:
1. **Fairness Definition Catalog**  
A concise reference of key fairness definitions, their mathematical formulations, philosophical foundations, and appropriate use cases.

2. **Definition Selection Decision Tree**  
A structured process for mapping application context to fairness definitions.

3. **Trade-Off Analysis Template**  
A documentation framework for recording selection rationale and acknowledging incompatibilities.

4. **Applied Example**  
Demonstrates how the tool can be implemented in a real system. (Internal loan application system).

## 4. Fairness Definition Selection Tool

### 4.1 Fairness Definition Catalog
### Demographic Parity

**Definition**  
The probability of receiving a positive outcome is equal across protected groups.

**Mathematical Form**  
P(Ŷ = 1 | A = a) = P(Ŷ = 1 | A = b)

**Philosophical Alignment**  
Egalitarian fairness, equal outcomes.

**When Appropriate**  
- Historical exclusion from access
- Representation is a primary concern
- Base rates reflect structural disadvantage

**Limitations**  
- May conflict with accuracy
- Ignores qualification differences
- Often incompatible with calibration

---


